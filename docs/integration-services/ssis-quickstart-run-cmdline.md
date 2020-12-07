---
description: DTExec.exe を使用してコマンド プロンプトから SSIS パッケージを実行する
title: コマンド プロンプトから SSIS パッケージを実行する | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e9efc610f33e2f58a8c1ae66b43480fb1d1da164
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195826"
---
# <a name="run-an-ssis-package-from-the-command-prompt-with-dtexecexe"></a>DTExec.exe を使用してコマンド プロンプトから SSIS パッケージを実行する

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


このクイックスタートでは、コマンド プロンプトから適切なパラメーターを使用して `DTExec.exe` を実行し、SSIS パッケージを実行する方法を説明します。

> [!NOTE]
> この記事で説明する方法は、Azure SQL Database サーバーに展開されているパッケージではテストされていません。

`DTExec.exe` の詳細については、「[dtexec ユーティリティ](./packages/dtexec-utility.md)」を参照してください。

## <a name="supported-platforms"></a>サポートされているプラットフォーム

このクイックスタートの情報を使用して、次のプラットフォームで SSIS パッケージを実行することができます。

-   SQL Server on Windows。

この記事で説明する方法は、Azure SQL Database サーバーに展開されているパッケージではテストされていません。 Azure でパッケージをデプロイし、実行する方法については、「[SQL Server Integration Services ワークロードをクラウドにリフト アンド シフトする](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)」を参照してください。

Linux で SSIS パッケージを実行する場合は、このクイックスタートの情報を使用することはできません。 Linux でパッケージを実行する方法については、[SSIS を使用し、Linux でデータの抽出、変換、読み込みを行う](../linux/sql-server-linux-migrate-ssis.md)方法に関するページを参照してください。

## <a name="run-a-package-with-dtexec"></a>Dtexec でのパッケージの実行

`DTExec.exe` を含むフォルダーが `path` 環境変数にない場合、そのディレクトリに変更するために `cd` コマンドを使用する必要がある場合があります。 SQL Server 2017 の場合、このフォルダーは通常 `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn` です。

次の例で使用されているパラメーター値で、プログラムは (SSIS カタログ データベース (SSISDB) をホストするサーバーである) SSIS サーバーの指定したフォルダー パスでパッケージを実行します。 `/Server` パラメーターによって、サーバー名が提供されます。 プログラムは、Windows 統合認証を使用して、現在のユーザーとして接続します。 SQL 認証を使用するには、適切な値を使用して、`/User` と `Password` を指定します。

1. コマンド プロンプト ウィンドウを開きます。

2. `DTExec.exe` を実行し、次の例のとおり、最低限 `ISServer` パラメーターと `Server` パラメーターの値は渡します。

    ```cmd
    dtexec /ISServer "\SSISDB\Project1Folder\Integration Services Project1\Package.dtsx" /Server "localhost"
    ```

## <a name="next-steps"></a>次のステップ
- パッケージを実行する他の方法を検討します。
    - [SSMS を使用して SSIS パッケージを実行する](./ssis-quickstart-run-ssms.md)
    - [Transact-SQL (SSMS) を使用して SSIS パッケージを実行する](./ssis-quickstart-run-tsql-ssms.md)
    - [Transact-SQL (VS Code) を使用して SSIS パッケージを実行する](ssis-quickstart-run-tsql-vscode.md)
    - [PowerShell を使用して SSIS パッケージを実行する](ssis-quickstart-run-powershell.md)
    - [C# を使用して SSIS パッケージを実行する](./ssis-quickstart-run-dotnet.md)