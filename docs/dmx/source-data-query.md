---
description: '&lt;source data query&gt;'
title: '&lt;ソースデータクエリ &gt; |Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9dbceb416cea3e64200708639a771989f900be3e
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726127"
---
# <a name="ltsource-data-querygt"></a>&lt;source data query&gt;
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  データマイニングモデルをトレーニングし、マイニングモデルから予測を作成するには、データベースの外部にあるデータにアクセスする必要があり [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ます。 \<source data query>この外部データを定義するには、データマイニング拡張機能 (DMX) で句を使用します。 [Dmx&#41;に挿入する &#40;](../dmx/insert-into-dmx.md)、 [&#60;モデルから選択して dmx &#40;に&#62; 予測結合を選択](../dmx/select-from-model-prediction-join-dmx.md)し、[すべて[選択] を選択](../dmx/select-from-model-prediction-join-dmx.md)し **\<source data query>** ます。  
  
## <a name="query-types"></a>クエリ型  
 ソース データの指定には、最も一般的な次の 3 つの方法があります。  
  
 [OPENQUERY &#40;DMX&#41;](../dmx/source-data-query-openquery.md)  
 このステートメントは [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 、既存のデータソースを使用して、のインスタンスの外部にあるデータを照会します。  
  
 **Openquery**は関数の**OPENROWSET**に似ていますが、 **openquery**には次のような利点があります。  
  
-   DMX クエリは、 **OPENQUERY**を使用した方がはるかに簡単に記述できます。 クエリを記述するたびに新しい接続文字列を作成するのではなく、データソース内の既存の接続文字列を利用できます。 データ ソース オブジェクトは、各ユーザーのデータ アクセスを制御することもできます。  
  
-   管理者は、サーバー上のデータへのアクセス方法をより細かく制御できます。 たとえば、管理者は、サーバーに読み込まれるプロバイダーや、アクセスできる外部データを管理できます。  
  
 [OPENROWSET &#40;DMX&#41;](../dmx/source-data-query-openrowset.md)  
 このステートメントは [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 、既存のデータソースを使用して、のインスタンスの外部にあるデータを照会します。  
  
 [DMX&#41;&#40;図形 ](../dmx/source-data-query-shape.md)  
 このステートメントは複数のデータ ソースをクエリして、入れ子になったテーブルを作成します。 **SHAPE**を使用すると、複数のソースのデータを1つの階層テーブルに結合できます。 これは、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] の機能を利用して、テーブル内にテーブルを埋め込むことによってテーブルを入れ子にします。  
  
 ソースデータを指定するには、次のオプションを使用することもできます。  
  
-   任意の有効な DMX ステートメント  
  
-   すべての有効な多次元式 (MDX) ステートメント  
  
-   ストアド プロシージャを返すテーブル  
  
-   XML for Analysis (XMLA) 行セット  
  
-   行セットパラメーター  
  
## <a name="see-also"></a>参照  
 [DMX&#41; データ操作ステートメントを &#40;データマイニング拡張機能](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#41; ステートメントリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-statements.md)   
 [入れ子になったテーブル &#40;Analysis Services データマイニング&#41;](/analysis-services/data-mining/nested-tables-analysis-services-data-mining)  
  
