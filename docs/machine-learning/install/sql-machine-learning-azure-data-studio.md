---
title: Azure Data Studio のノートブック (Python、R)
description: SQL Server Machine Learning Services を使用して Azure Data Studio のノートブックで Python スクリプトと R スクリプトを実行する方法について説明します。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 03/09/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b8f787cdef6baeeaa57e79c9c5c167e12395508b
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956986"
---
# <a name="run-python-and-r-scripts-in-azure-data-studio-notebooks-with-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services を使用して Azure Data Studio のノートブックで Python スクリプトと R スクリプトを実行する
[!INCLUDE [SQL Server 2017 and later](../../includes/applies-to-version/sqlserver2017.md)]

[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) を使用して [Azure Data Studio](../../azure-data-studio/what-is.md) ノートブックで Python スクリプトと R スクリプトを実行する方法について説明します。 Azure Data Studio は、クロスプラットフォームのデータベース ツールです。

## <a name="prerequisites"></a>前提条件

- お使いのワークステーション コンピューターに [Azure Data Studio をダウンロードしてインストール](../../azure-data-studio/download-azure-data-studio.md)します。 Azure Data Studio はクロスプラットフォームであり、Windows、macOS、Linux で実行されます。

- SQL Server Machine Learning Services がインストールされ、有効になっているサーバー。 Machine Learning Services は、Windows、Linux、またはビッグ データ クラスターで使用できます。

  - [Windows に SQL Server Machine Learning Services をインストールする](sql-machine-learning-services-windows-install.md)。
  - [Linux に SQL Server Machine Learning Services をインストールする](../../linux/sql-server-linux-setup-machine-learning.md)。
  - [SQL Server ビッグ データ クラスターで Machine Learning Services を使用して Python スクリプトと R スクリプトを実行する](../../big-data-cluster/machine-learning-services.md)。

## <a name="create-a-sql-notebook"></a>SQL ノートブックを作成する

> [!IMPORTANT]
> Machine Learning Services は SQL Server の一部として実行されます。 そのため、Python カーネルではなく、SQL カーネルを使用する必要があります。

SQL ノートブックを使って、Azure Data Studio で Machine Learning Services を使用できます。 新しいノートブックを作成するには、次の手順に従います。

1. **[ファイル]** と **[新しいノートブック]** をクリックして、新しいノートブックを作成します。 ノートブックでは、既定で **SQL カーネル**が使用されます。

1. **[アタッチ先]** と **[接続の変更]** をクリックしします。 

    > [!div class="mx-imgBorder"]
    > ![Azure Data Studio の SQL ノートブックの接続の変更](media/ads-attach-to-connection.png)
    
1. 既存または新規の SQL Server に接続します。 次のいずれかを実行できます。

    1. **[最近の接続]** または **[保存された接続]** で、既存の接続を選択します。

    1. **[接続の詳細]** で新しい接続を作成します。 接続の詳細をお使いの SQL Server とデータベースに入力します。

    > [!div class="mx-imgBorder"]
    > ![Azure Data Studio の SQL ノートブックの接続の詳細](media/ads-connection-details.png)  

## <a name="run-python-or-r-scripts"></a>Python スクリプトまたは R スクリプトを実行する

SQL ノートブックは、コード セルとテキスト セルで構成されます。 コード セルは、ストアド プロシージャ [sp_execute_external_scripts](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) を介して Python または R スクリプトを実行するために使用します。 テキスト セルを使用して、ノートブック内のコードをドキュメント化できます。

### <a name="run-a-python-script"></a>Python スクリプトを実行する

Python スクリプトを実行するには、次の手順に従います。

1. **[+ コード]** をクリックして、コード セルを追加します。

    > [!div class="mx-imgBorder"]
    > ![Azure Data Studio の SQL ノートブックでコード ブロックを追加する](media/ads-add-code.png)  

1. コード セルに、次のスクリプトを入力します。

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

1. **[セルの実行]** (黒い丸の矢印) をクリックするか、**F5** 押してこの単一セルを実行します。

    > [!div class="mx-imgBorder"]
    > ![Azure Data Studio の SQL ノートブックで Python コードを実行する](media/ads-run-python.png)  

1. 結果がコード セルの下に表示されます。

    > [!div class="mx-imgBorder"]
    > ![Azure Data Studio の SQL ノートブックの Python コードの出力](media/ads-run-python-output.png)  

### <a name="run-an-r-script"></a>R スクリプトを実行する

R スクリプトを実行するには、次の手順に従います。

1. **[+ コード]** をクリックして、コード セルを追加します。

    > [!div class="mx-imgBorder"]
    > ![Azure Data Studio の SQL ノートブックでコード ブロックを追加する](media/ads-add-code.png)  

1. コード セルに、次のスクリプトを入力します。

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
    a <- 1
    b <- 2
    c <- a/b
    d <- a*b
    print(c(c, d))
    '
    ```

1. **[セルの実行]** (黒い丸の矢印) をクリックするか、**F5** 押してこの単一セルを実行します。

    > [!div class="mx-imgBorder"]
    > ![Azure Data Studio の SQL ノートブックで R コードを実行する](media/ads-run-r.png)  

1. 結果がコード セルの下に表示されます。

    > [!div class="mx-imgBorder"]
    > ![Azure Data Studio の SQL ノートブックの R コードの出力](media/ads-run-r-output.png)  

## <a name="next-steps"></a>次のステップ

- [Azure Data Studio でノートブックを使用する方法](../../azure-data-studio/notebooks/notebooks-guidance.md)
- [SQL Server ノートブックを作成して実行する](../../azure-data-studio/notebooks/notebooks-sql-kernel.md)
- [クイック スタート: SQL Server Machine Learning Services を使用してシンプルな Python スクリプトを実行する](../tutorials/quickstart-python-create-script.md)
- [クイック スタート: SQL Server Machine Learning Services を使用してシンプルな R スクリプトを実行する](../tutorials/quickstart-r-create-script.md)