---
title: R チュートリアル:データの機能の作成
titleSuffix: SQL machine learning
description: 全 5 回からなるこのチュートリアル シリーズの第 3 回では、T-SQL 関数を使用し、SQL 機械学習でサンプル データから特徴を作成し、保存します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/15/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||>=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: e498b76d1b7924a4ee4154c35c4e492612b9c801
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92412569"
---
# <a name="r-tutorial-create-data-features"></a>R チュートリアル:データの機能の作成
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

全 5 回からなるこのチュートリアル シリーズの第 3 回では、[!INCLUDE[tsql](../../includes/tsql-md.md)] 関数を使用して生データから特徴を作成する方法について説明します。 その後、その関数を SQL ストアド プロシージャから呼び出し、機能の値を含むテーブルを作成します。

この記事では、次のことを行います。

> [!div class="checklist"]
> + 旅行の距離を計算するカスタム関数を変更する
> + 別のカスタム関数を使用して特徴を保存する

[パート 1 ](r-taxi-classification-introduction.md)では、前提条件をインストールしてサンプル データベースを復元しました。

[第 2 回](r-taxi-classification-explore-data.md) では、サンプル データを確認し、いくつかのプロットを生成しました。

[第 4 回](r-taxi-classification-train-model.md) では、モジュールを読み込み、必要な関数を呼び出して、SQL Server ストアド プロシージャを使用してモデルを作成およびトレーニングします。

[第 5 回](r-taxi-classification-deploy-model.md) では、第 4 回でトレーニングして保存したモデルを運用化する方法について説明します。

[第 5 回](./python-taxi-classification-deploy-model.md) では、第 4 回でトレーニングして保存したモデルを運用化する方法について説明します。

## <a name="about-feature-engineering"></a>機能エンジニアリングについて

データ探索を何度か行うと、データからインサイトが収集されているので、 *機能エンジニアリング* に移ることができます。 生データから意味のある特徴を作成するこのプロセスは、分析モデルを作成するための重要な手順です。

このデータセットでは、距離の値は報告されたメーター距離に基づいており、必ずしも地理的距離や実際の走行距離を示す距離を表しているとは限りません。 そのため、ソースである NYC タクシー データセットの座標を利用し、乗車地点と降車地点の間の直接距離を計算する必要があります。 カスタム [関数で](https://en.wikipedia.org/wiki/Haversine_formula) Haversine 式 [!INCLUDE[tsql](../../includes/tsql-md.md)] を利用し、この計算を実行できます。

1 つ目のカスタム T-SQL 関数、 _fnCalculateDistance_ を利用し、Haversine 式で距離を計算し、2 つ目のカスタム T-SQL 関数、 _fnEngineerFeatures_ を利用し、すべての機能を含むテーブルを作成します。

全体的なプロセスは次のとおりです。

+ 計算を実行する T-SQL 関数を作成する

+ 関数を呼び出して機能データを生成します

+ 機能データをテーブルに保存する

## <a name="calculate-trip-distance-using-fncalculatedistance"></a>fnCalculateDistance を利用して乗車距離を計算する

このチュートリアルの準備の一環として、関数 _fnCalculateDistance_ をダウンロードし、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に登録する必要があります。 少し時間をかけてコードを確認してください。
  
1. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]で、 **[プログラミング]** 、 **[関数]** 、 **[スカラー値関数]** の順に展開します。   

2. _fnCalculateDistance_ を右クリックし、 **[変更]** を選択し、新しいクエリ ウィンドウで [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトを開きます。
  
   ```sql
   CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)  
   -- User-defined function that calculates the direct distance between two geographical coordinates.  
   RETURNS float  
   AS  
   BEGIN  
     DECLARE @distance decimal(28, 10)  
     -- Convert to radians  
     SET @Lat1 = @Lat1 / 57.2958  
     SET @Long1 = @Long1 / 57.2958  
     SET @Lat2 = @Lat2 / 57.2958  
     SET @Long2 = @Long2 / 57.2958  
     -- Calculate distance  
     SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))  
     --Convert to miles  
     IF @distance <> 0  
     BEGIN  
       SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);  
     END  
     RETURN @distance  
   END
   GO
   ```
  
   + この関数はスカラー値関数であり、事前定義されている種類の単一データ値を返します。
  
   + 乗車場所と降車場所から取得した緯度値と経度値を入力値として受け取ります。 Haversine 式は場所をラジアンに変換し、その値を利用して 2 場所間の直接距離をマイルで計算します。

## <a name="generate-the-features-using-_fnengineerfeatures_"></a>_fnEngineerFeatures を使用して機能を生成する_

モデルのトレーニングに使用できるテーブルに計算値を追加するには、別の関数 _fnEngineerFeatures_ を使用します。 この新しい関数は、以前に作成した T-SQL 関数 _fnCalculateDistance_ を呼び出して、乗車場所と降車場所の距離を直接取得します。 

1. カスタム T-SQL 関数、 _fnEngineerFeatures_ のコードを再確認します。この関数は、このチュートリアルの一環として自動的に作成されているはずです。
  
   ```sql
   CREATE FUNCTION [dbo].[fnEngineerFeatures] (  
   @passenger_count int = 0,  
   @trip_distance float = 0,  
   @trip_time_in_secs int = 0,  
   @pickup_latitude float = 0,  
   @pickup_longitude float = 0,  
   @dropoff_latitude float = 0,  
   @dropoff_longitude float = 0)  
   RETURNS TABLE  
   AS
     RETURN
     (
     -- Add the SELECT statement with parameter references here
     SELECT
       @passenger_count AS passenger_count,
       @trip_distance AS trip_distance,
       @trip_time_in_secs AS trip_time_in_secs,
       [dbo].[fnCalculateDistance](@pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude) AS direct_distance
  
     )
   GO
   ```

   + このテーブル値関数は、複数の列を入力値として受け取り、複数の機能列を含むテーブルを出力します。

   + この関数の目的は、モデルの構築に利用する新しい機能を作成することです。

2. この関数が動作することを確認するために、それを利用し、メーター距離が 0 であったが、乗車場所と降車場所が異なっていた乗車の地理的距離を計算できます。
  
   ```sql
       SELECT tipped, fare_amount, passenger_count,(trip_time_in_secs/60) as TripMinutes,
       trip_distance, pickup_datetime, dropoff_datetime,
       dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) AS direct_distance
       FROM nyctaxi_sample
       WHERE pickup_longitude != dropoff_longitude and pickup_latitude != dropoff_latitude and trip_distance = 0
       ORDER BY trip_time_in_secs DESC
   ```
  
   ご覧のとおり、メーターによって報告された距離と地理的距離は常に一致しているわけではありません。 そのため、機能エンジニアリングが重要となります。 これらの改善されたデータ機能を使用して、R を使用して機械学習モデルをトレーニングすることができます。

## <a name="next-steps"></a>次のステップ

この記事では、次の内容について説明します。

> [!div class="checklist"]
> + 旅行の距離を計算するカスタム関数を変更しました
> + 別のカスタム関数を使用して特徴を保存しました

> [!div class="nextstepaction"]
> [R チュートリアル:モデルのトレーニングと保存](r-taxi-classification-train-model.md)