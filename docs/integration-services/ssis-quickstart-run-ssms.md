---
description: SQL Server Management Studio (SSMS) を使用して SSIS パッケージを実行する
title: SSMS を使用して SSIS パッケージを実行する | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: beb9a1e1dcb25f42e2d9a49c1e0e5c1a77a3f0ea
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "92193062"
---
# <a name="run-an-ssis-package-with-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS) を使用して SSIS パッケージを実行する

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


このクイックスタートでは、SQL Server Management Studio (SSMS) を使用して SSIS カタログ データベースに接続してから、SSMS のオブジェクト エクスプローラーから SSIS カタログに格納されている SSIS パッケージを実行する方法を示します。

SQL Server Management Studio は、SQL Server から SQL Database まで、SQL インフラストラクチャを管理するための統合環境です。 SSMS については、「[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)」をご覧ください。

## <a name="prerequisites"></a>前提条件

開始する前に、最新バージョンの SQL Server Management Studio (SSMS) があることを確認します。 SSMS をダウンロードするには、「[SQL Server Management Studio (SSMS) のダウンロード](../ssms/download-sql-server-management-studio-ssms.md)」を参照してください。

Azure SQL Database サーバーは、ポート 1433 でリッスンします。 企業のファイアウォール内から Azure SQL Database サーバーに接続しようとする場合、正常に接続するには、このポートを企業のファイアウォールで開ける必要があります。

## <a name="supported-platforms"></a>サポートされているプラットフォーム

このクイックスタートの情報を使用して、次のプラットフォームで SSIS パッケージを実行することができます。

-   SQL Server on Windows。

-   Azure SQL Database。 Azure でパッケージをデプロイし、実行する方法については、「[SQL Server Integration Services ワークロードをクラウドにリフト アンド シフトする](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)」を参照してください。

Linux で SSIS パッケージを実行する場合は、このクイックスタートの情報を使用することはできません。 Linux でパッケージを実行する方法については、[SSIS を使用し、Linux でデータの抽出、変換、読み込みを行う](../linux/sql-server-linux-migrate-ssis.md)方法に関するページを参照してください。

## <a name="for-azure-sql-database-get-the-connection-info"></a>Azure SQL Database の場合の接続情報の取得

Azure SQL Database でパッケージを実行するには、SSIS カタログ データベース (SSISDB) に接続するために必要な接続情報を取得します。 次の手順では、完全修飾サーバー名とログイン情報が必要です。

1. [Azure Portal](https://portal.azure.com/) にログインします。
2. 左側のメニューから **[SQL Databases]** を選択し、**[SQL データベース]** ページで SSISDB データベースを選びます。 
3. データベースの **[概要]** ページで、完全修飾サーバー名を確認します。 **[クリックしてコピー]** オプションを表示するには、サーバー名にマウス ポインターを移動します。 
4. Azure SQL Database サーバーのログイン情報を忘れた場合は、[SQL Database サーバー] ページに移動し、サーバーの管理者名を表示します。 必要に応じて、パスワードをリセットできます。

## <a name="connect-to-the-ssisdb-database"></a>SSISDB データベースに接続する

SQL Server Management Studio を使って、SSIS カタログへの接続を確立します。 

1. SQL Server Management Studio を開きます。

2. **[サーバーへの接続]** ダイアログ ボックスで、次の情報を入力します。

   | 設定       | 推奨値 | 詳細情報 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **サーバーの種類** | データベース エンジン | この値は必須です。 |
   | **サーバー名** | 完全修飾サーバー名 | Azure SQL Database サーバーに接続する場合、名前は次の形式になります。`<server_name>.database.windows.net` |
   | **認証** | SQL Server 認証 | SQL Server 認証を使用すると、SQL Server または Azure SQL Database に接続できます。 Azure SQL Database サーバーに接続する場合、Windows 認証を使用できません。 |
   | **Login** | サーバー管理者アカウント | このアカウントは、サーバーの作成時に指定したアカウントです。 |
   | **パスワード** | サーバー管理者アカウントのパスワード | このパスワードは、サーバーの作成時に指定したパスワードです。 |

3. **[Connect]** をクリックします。 SSMS で [オブジェクト エクスプローラー] ウィンドウが開きます。 

4. オブジェクト エクスプローラーで、 **[Integration Services カタログ]** 、 **[SSISDB]** の順に展開し、SSIS カタログ データベース内のオブジェクトを表示します。

## <a name="run-a-package"></a>パッケージの実行

1. オブジェクト エクスプローラーで、実行するパッケージを選択します。

2. 右クリックして、**[実行]** を選択します。 **[パッケージの実行]** ダイアログ ボックスが開きます。

3.  **[パッケージの実行]** ダイアログ ボックスの **[パラメーター]** タブ、 **[接続マネージャー]** タブ、 [詳細設定] タブの設定を使用して、パッケージの実行を構成します。

4.  [OK] をクリックしてパッケージを実行します。

## <a name="next-steps"></a>次のステップ
- パッケージを実行する他の方法を検討します。
    - [Transact-SQL (SSMS) を使用して SSIS パッケージを実行する](./ssis-quickstart-run-tsql-ssms.md)
    - [Transact-SQL (VS Code) を使用して SSIS パッケージを実行する](ssis-quickstart-run-tsql-vscode.md)
    - [コマンド プロンプトから SSIS パッケージを実行する](./ssis-quickstart-run-cmdline.md)
    - [PowerShell を使用して SSIS パッケージを実行する](ssis-quickstart-run-powershell.md)
    - [C# を使用して SSIS パッケージを実行する](./ssis-quickstart-run-dotnet.md)