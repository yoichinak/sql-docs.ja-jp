---
title: rxExec を使用したカスタム R 関数
description: シミュレートされたデータを使用し、リモート サーバーで実行されるカスタム R 関数の実行について示します。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b8f03c64dc86e6d23113f3a35ae669f216b66489
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195154"
---
# <a name="run-custom-r-functions-on-sql-server-using-rxexec-sql-server-and-revoscaler-tutorial"></a>SQL Server 上で rxExec を使用してカスタム R 関数を実行する (SQL Server と RevoScaleR のチュートリアル)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

これは、SQL Server で [RevoScaleR 関数](/machine-learning-server/r-reference/revoscaler/revoscaler)を使用する方法についての [RevoScaleR チュートリアル シリーズ](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)のチュートリアル 14 です。

このチュートリアルでは、シミュレートされたデータを使用して、リモート サーバーで実行されるカスタム R 関数の実行について示します。

[rxExec](/machine-learning-server/r-reference/revoscaler/rxexec) を介して関数を渡すことで、SQL Server のコンテキストでカスタム R 関数を実行できます。これはスクリプトで必要なライブラリがサーバーにもインストールされており、これらのライブラリが R の基本ディストリビューションと互換性があることを前提としています。 

**RevoScaleR** の **rxExec** 関数には、必要な R スクリプトを実行するためのメカニズムが用意されています。 さらに、**rxExec** では、1台のサーバーの複数のコアに対して作業を明示的に配布することができます。そのため、スクリプトがネイティブ R エンジンのリソース制約に限定されないように、スケールを増加します。

## <a name="prerequisites"></a>前提条件

+ [SQL Server Machine Learning Services (R 付属)](../install/sql-machine-learning-services-windows-install.md) または [SQL Server 2016 R Services (データベース内)](../install/sql-r-services-windows-install.md)
  
+ [データベース権限](../security/user-permission.md)と SQL Server データベース ユーザー ログイン

+ [RevoScaleR ライブラリを使用した開発ワークステーション](../r/set-up-a-data-science-client.md)

クライアント ワークステーションの R ディストリビューションには、このチュートリアルの R スクリプトを実行するために使用できる組み込みの **Rgui** ツールが用意されています。 RStudio や R Tools for Visual Studio などの IDE を使用することもできます。

## <a name="create-the-remote-compute-context"></a>リモート コンピューティング コンテキストを作成する

クライアント ワークステーション上で次の R コマンドを実行します。 たとえば、**Rgui** を使用している場合は、次の場所から開始します。C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64\.

1. 計算を実行する SQL Server インスタンスの接続文字列を指定します。 サーバーは、R 統合用に構成されている必要があります。 この演習ではデータベース名は使用されませんが、接続文字列には必要です。 テスト データベースまたはサンプル データベースがある場合は、それを使用できます。

    **SQL ログインを使用する**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>; Database=<database-name>;Uid=<SQL-user-name>;Pwd=<password>"
    ```

    **Windows 認証を使用する**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>;Database=<database-name>;Trusted_Connection=True"
    ```

2. 接続文字列で参照されている SQL Server インスタンスへのリモート コンピューティング コンテキストを作成します。

    ```R
    sqlCompute <- RxInSqlServer(connectionString = sqlConnString)
    ```

3. コンピューティング コンテキストをアクティブにし、確認手順としてオブジェクト定義を返します。 コンピューティング コンテキスト オブジェクトのプロパティが表示されます。

    ```R
    rxSetComputeContext(sqlCompute)
    rxGetComputeContext()
    ```

## <a name="create-the-custom-function"></a>カスタム関数を作成する

この演習では、2 個のサイコロを振ることで構成される、一般的なカジノをシミュレートする、カスタム R 関数を作成します。 ゲームのルールにより、勝利または敗北の結果が決定されます。

+ 最初に転がしたとき、7 か 11 になれば、あなたの勝ちです。
+ 2、3、12 が出た場合、あなたの負けです。
+ 4、5、6、8、9、10 が出た場合、その数があなたのポイントになり、もう一度そのポイントを出すか、7 を出すまでサイコロを振り続けます。もう一度そのポイントが出たらあなたの勝ちで、7 が出たらあなたの負けです。

このゲームは R で簡単にシミュレートできます。カスタム関数を作成し、それを何度も実行します。

1.  次の R コードを使用して、カスタム関数を作成します。
  
    ```R
    rollDice <- function()
    {
        result <- NULL
        point <- NULL
        count <- 1
            while (is.null(result))
            {
                roll <- sum(sample(6, 2, replace=TRUE))
  
                if (is.null(point))
                { point <- roll }
                if (count == 1 && (roll == 7 || roll == 11))
                {  result <- "Win" }
                else if (count == 1 && (roll == 2 || roll == 3 || roll == 12))
                { result <- "Loss" }
                else if (count > 1 && roll == 7 )
                { result <- "Loss" }
                else if (count > 1 && point == roll)
                { result <- "Win" }
                else { count <- count + 1 }
            }
            result
    }
    ```
  
2.  関数を実行して、サイコロ ゲームを 1 回シミュレートします。
  
    ```R
    rollDice()
    ```
  
    あなたの勝ちでしたか。それとも負けでしたか。
  
これで、一回動作するスクリプトが完成しました。**rxExec** を使用して関数を複数回実行して、勝利の確率を判断するのに役立つシミュレーションを作成する方法を見てみましょう。

## <a name="pass-rolldice-in-rxexec"></a>rxExec で rollDice () を渡す

リモート SQL Server のコンテキストで任意の関数を実行するには、**rxExec** 関数を呼び出します。

1. シミュレーションを変更するその他のパラメーターと共に、**rxExec** への引数としてカスタム関数を呼び出します。
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    + *timesToRun* 引数を使用すれば、関数を実行する回数を指示できます。  この場合、20 回サイコロを振ります。
  
    + *RNGseed* 引数と *RNGkind* 引数を利用し、乱数の生成を制御できます。 *RNGseed* が **auto**に設定されると、各ワーカーで並行乱数ストリームが初期化されます。
  
2. **rxExec** 関数は実行のたびに 1 つの要素で一覧を作成します。ただし、一覧が完了するまで内容はわかりません。 すべての繰り返しが完了すると、**length** から始まる行は値を返します。
  
    次の手順に進むと、勝敗記録のまとめを取得できます。
  
3. R の **unlist** 関数を使用して、返された一覧をベクトルに変換し、 **table** 関数を使用して結果をまとめます。
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    結果は次のようになります。
  
     *負け  勝ち* *12  8*

## <a name="conclusion"></a>まとめ

この演習は単純ですが、SQL Server で実行されている R スクリプトで任意の R 関数を統合するための重要なメカニズムを示しています。 この手法を可能にする主なポイントをまとめると、次のようになります。

+ SQL Server は、機械学習と R の統合用に構成される必要があります。たとえば、R 機能付きの [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)、または [SQL Server 2016 R Services (データベース内)](../install/sql-r-services-windows-install.md)。

+ 依存関係も含め、関数で使用されているオープンソースまたはサードパーティのライブラリを SQL Server にインストールする必要があります。 詳細については、「[新しい R パッケージのインストール](../package-management/install-additional-r-packages-on-sql-server.md)」に関するページを参照してください。

+ 開発環境から、堅牢な運用環境にスクリプトを移動すると、ファイアウォールとネットワークの制限が生じる可能性があります。 慎重にテストして、スクリプトが期待どおりに実行できることを確認します。

## <a name="next-steps"></a>次のステップ

**rxExec** を使用するより複雑な例については、次の記事を参照してください。[foreach と rxExec による粒度の粗い並列処理](https://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)