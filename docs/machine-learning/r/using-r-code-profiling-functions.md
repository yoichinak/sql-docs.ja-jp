---
title: R コード プロファイル関数を使用してパフォーマンスを向上させる
description: R プロファイリング関数を使用することで、パフォーマンスを向上させるのに役立つ情報を収集し、SQL Server での R 計算の結果をより速く得られるようにします。 *rprof* 関数は、内部関数呼び出しに関する情報を収集して返します。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/30/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d15f31dc2c289df910b06de8cb1f48647dbde33c
ms.sourcegitcommit: 49ee3d388ddb52ed9cf78d42cff7797ad6d668f2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2020
ms.locfileid: "94384751"
---
# <a name="use-r-code-profiling-functions-to-improve-performance"></a>R コード プロファイル関数を使用してパフォーマンスを向上させる
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

この記事では、内部関数呼び出しに関する情報を取得するために R パッケージによって提供されるパフォーマンス ツールについて説明します。 この情報を使用して、コードのパフォーマンスを向上させることができます。

> [!TIP]
> この記事では、作業を開始するための基本的なリソースについて説明します。 専門家によるガイダンスとしては、[Hadley Wickham 著 "Advanced R"](http://adv-r.had.co.nz) の「*Performance*」の章をお勧めします。

## <a name="using-rprof"></a>rprof の使用

[*rprof*](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/Rprof) は、基本パッケージ [**utils**](https://www.rdocumentation.org/packages/utils/versions/3.5.1) に含まれる関数で、既定で読み込まれます。 

一般に *rprof* 関数は、指定した間隔でファイルに呼び出し履歴を記述することで機能します。 その後、[*summaryRprof*](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/summaryRprof) 関数を使用して、出力ファイルを処理できます。 *rprof* の利点の 1 つは、サンプリングを実行するため、監視によるパフォーマンスの負荷を軽減することです。

コードで R プロファイルを使用するには、この関数を呼び出してパラメーター (書き込まれるログ ファイルの場所の名前など) を指定します。 コードでプロファイルをオンまたはオフにできます。 基本的な使用法を次の構文に示します。 

```R
# Specify profiling output file.
varOutputFile <- "C:/TEMP/run001.log")
Rprof(varOutputFile)

# Turn off profiling
Rprof(NULL)
    
# Restart profiling
Rprof(append=TRUE)
```

> [!NOTE]
> この関数を使用するには、コードを実行するコンピューターに Windows Perl がインストールされている必要があります。 このため、R 環境での開発中にコードをプロファイルし、デバッグ済みのコードを SQL Server に展開することをお勧めします。  


## <a name="r-system-functions"></a>R システム関数

R 言語には、システム変数の内容を返すための多くの基本パッケージ関数が含まれています。 たとえば、R コードの一部として、`Sys.timezone` を使用して現在のタイム ゾーンを取得したり、`Sys.Time` を使用して R からシステム時刻を取得することがあります。 

個別の R システム関数の情報を取得するには、R コマンド プロンプトから、R `help()` 関数の引数として関数名を入力します。

```R
help("Sys.time")
```

## <a name="debugging-and-profiling-in-r"></a>R のデバッグとプロファイル

既定でインストールされる Microsoft R Open のドキュメントには、R 言語の拡張機能の開発に関するマニュアルが含まれており、[プロファイルとデバッグ](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging)の詳細について説明しています。

## <a name="next-steps"></a>次のステップ

+ SQL Server での R スクリプトの最適化の詳細については、[R でのパフォーマンスのチューニングとデータの最適化](r-and-data-optimization-r-services.md)に関する記事を確認してください。
+ SQL Server でのパフォーマンスの調整の詳細については、「[SQL Server データベース エンジンと Azure SQL Database のパフォーマンス センター](/sql/relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database)」を参照してください。
+ utils パッケージの詳細については、「[The R Utils Package (R Utils パッケージ)](https://www.rdocumentation.org/packages/utils/versions/3.5.1)」を参照してください。
+ R のプログラミングの詳細については、「["Advanced R" by Hadley Wickham (Hadley Wickham による "Advanced R")](http://adv-r.had.co.nz)」を参照してください。
