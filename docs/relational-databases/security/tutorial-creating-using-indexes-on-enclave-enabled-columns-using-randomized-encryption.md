---
title: ランダム化された暗号化を使用してエンクレーブ対応の列でインデックスを作成する (チュートリアル)
description: このチュートリアルでは、SQL Server および Azure SQL Database 用のセキュリティで保護されたエンクレーブが設定された Always Encrypted でサポートされているランダム化された暗号化を使用して、エンクレーブ対応の列にインデックスを作成して使用する方法を説明します。
ms.custom: seo-lt-2019
ms.date: 01/15/2021
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: 5e08a42f9112379951c9fcff27693ab3700b69fd
ms.sourcegitcommit: 8ca4b1398e090337ded64840bcb8d6c92d65c29e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2021
ms.locfileid: "98534821"
---
# <a name="tutorial-create-and-use-indexes-on-enclave-enabled-columns-using-randomized-encryption"></a>チュートリアル:ランダム化された暗号化を使用してエンクレーブ対応の列でインデックスを作成して使用する

[!INCLUDE [sqlserver2019-windows-only-asdb](../../includes/applies-to-version/sqlserver2019-windows-only-asdb.md)]

このチュートリアルでは、[セキュリティで保護されたエンクレーブが設定された Always Encrypted](encryption/always-encrypted-enclaves.md) でサポートされているランダム化された暗号化を使用して、エンクレーブ対応の列にインデックスを作成して使用する方法を説明します。 次のことを示します。

> [!div class="checklist"]
> - 列を保護しているキー (列マスター キーと列暗号化キー) にアクセスできるときに、インデックスを作成する方法。
> - 列を保護しているキーにアクセスできないときに、インデックスを作成する方法。

## <a name="prerequisites"></a>前提条件

このチュートリアルの次の手順に従う前に、以下のチュートリアルのいずれかを完了していることを確認してください。

- [チュートリアル: SQL Server でのセキュリティで保護されたエンクレーブを使用する Always Encrypted の概要](tutorial-getting-started-with-always-encrypted-enclaves.md)
- [チュートリアル: Azure SQL Database でのセキュリティで保護されたエンクレーブを使用する Always Encrypted の概要](/azure/azure-sql/database/always-encrypted-enclaves-getting-started)

## <a name="step-1-enable-accelerated-database-recovery-adr-in-your-database"></a>手順 1:データベースで高速データベース復旧 (ADR) を有効にする

> [!NOTE]
> この手順は [!INCLUDE [ssnoversion-md](../../includes/ssnoversion-md.md)] にのみ適用されます。 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] を使用している場合は、この手順をスキップしてください。 ADR は [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] で自動的に有効になり、無効化はサポートされていません。

ランダム化された暗号化を使用してエンクレーブ対応の列で最初のインデックスを作成する前に、データベースで ADR を有効にすることを強くお勧めします。 「[セキュリティで保護されたエンクレーブが設定された Always Encrypted](./encryption/always-encrypted-enclaves.md)」の「[データベース復旧](./encryption/always-encrypted-enclaves.md#database-recovery)」セクションを参照してください。



1. 前のチュートリアルで使ったすべての SSMS インスタンスを閉じます。 これにより、開いたデータベース接続が閉じられます。ADR を有効にするにはこうする必要があります。
1. SSMS の新しいインスタンスを開き、データベース接続の Always Encrypted を有効に **しないで**、sysadmin として [!INCLUDE [ssnoversion-md](../../includes/ssnoversion-md.md)] インスタンスに接続します。
    1. SSMS を起動します。
    1. **[サーバーへの接続]** ダイアログで、サーバーの名前を指定し、認証方法を選択して、資格情報を指定します。
    1. **[オプション >>]** をクリックして、 **[Always Encrypted]** タブを選択します。
    1. **[Always Encrypted を有効にする (列の暗号化)]** チェック ボックスがオンになって **いない** ことを確認します。
    1. **[接続]** を選択します。
1. 新しいクエリ ウィンドウを開き、下のステートメントを実行して ADR を有効にします。

   ```sql
   ALTER DATABASE ContosoHR SET ACCELERATED_DATABASE_RECOVERY = ON;
   ```

## <a name="step-2-create-and-test-an-index-without-role-separation"></a>手順 2:ロールを分離せずにインデックスを作成してテストする

この手順では、暗号化された列でインデックスを作成してテストします。 データベースを管理する DBA と、データを保護しているキーにアクセスできるデータ所有者の両方のロールを担う、1 人のユーザーとして作業します。

1. 新しい SSMS インスタンスを開き、データベース接続に対して Always Encrypted を有効に **して**、[!INCLUDE [ssnoversion-md](../../includes/ssnoversion-md.md)] インスタンスに接続します。
   1. SSMS の新しいインスタンスを開始します。
   1. **[サーバーへの接続]** ダイアログで、サーバーの名前を指定し、認証方法を選択して、資格情報を指定します。
   1. **[オプション >>]** をクリックして、 **[Always Encrypted]** タブを選択します。
   1. **[Always Encrypted を有効にする (列の暗号化)]** チェック ボックスをオンにして、エンクレーブ構成証明 URL (たとえば、`http://hgs.bastion.local/Attestation` や `https://MyAttestationProvider.us.attest.azure.net/attest/SgxEnclave`) を指定します。
   1. **[接続]** を選択します。
   1. Always Encrypted クエリのパラメーター化を有効にすることの確認を求められたら、**[有効]** をクリックします。
1. Always Encrypted のパラメーター化を有効にすることを求められなかった場合は、有効になっていることを確認します。
   1. SSMS のメイン メニューから **[ツール]** を選択します。
   2. **[オプション...]** を選択します。
   3. **[クエリ実行]**  >  **[SQL Server]**  >  **[詳細]** の順に移動します。
   4. **[Always Encrypted のパラメーター化を有効にする]** がオンであることを確認します。
   5. **[OK]** を選択します。
1. クエリ ウィンドウを開き、下のステートメントを実行して、**Employees** テーブルの **LastName** 列を暗号化します。 後の手順では、その列にインデックスを作成して使用します。

   ```sql  
   ALTER TABLE [HR].[Employees]
   ALTER COLUMN [LastName] [nvarchar](50) COLLATE Latin1_General_BIN2 
   ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL;
   GO   
   ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
   GO
   ```

1. **LastName** 列にインデックスを作成します。 Always Encrypted を有効にしてデータベースに接続しているため、SSMS 内のクライアント ドライバーによって、**CEK1** (**LastName** 列を保護している列暗号化キー) がエンクレーブに透過的に提供されます。インデックスを作成するにはこれが必要です。

   ```sql
   CREATE INDEX IX_LastName ON [HR].[Employees] ([LastName])
   INCLUDE ([EmployeeID], [FirstName], [SSN], [Salary]);
   GO
   ```

1. **LastName** 列に対して高度なクエリを実行し、クエリの実行時に SQL Server によってインデックスが使われることを確認します。
   1. 同じクエリ ウィンドウまたは新しいクエリ ウィンドウで、ツール バーの **[ライブ クエリ統計を含む]** ボタンがオンになっていることを確認します。
   1. 下のクエリを実行します。

       ```sql
       DECLARE @LastNamePrefix NVARCHAR(50) = 'Aber%';
       SELECT * FROM [HR].[Employees] WHERE [LastName] LIKE @LastNamePrefix;
       GO
      ```

   1. **[ライブ クエリ統計]** タブ (クエリ ウィンドウの下部) で、クエリによりインデックスが使われていることを確認します。

## <a name="step-3-create-an-index-with-role-separation"></a>手順 3: ロールを分離してインデックスを作成する

この手順では、2 人の異なるユーザーとして、暗号化された列にインデックスを作成します。 1 人のユーザーは、インデックスを作成する必要がありますが、キーにアクセスできない DBA です。 もう 1 人のユーザーは、キーにアクセスできるデータ所有者です。

1. Always Encrypted が有効になって **いない** SSMS インスタンスを使い、下のステートメントを実行して **LastName** 列のインデックスを削除します。

   ```sql
   DROP INDEX IX_LastName ON [HR].[Employees]; 
   GO
   ```

1. データ所有者 (または、キーにアクセスできるアプリケーション) として、エンクレーブ内のキャッシュに **CEK1** を設定します。

   > [!NOTE]
   > 「**手順 2: ロールを分離せずにインデックスを作成してテストする**」の後で SQL Server インスタンスを再起動していない場合、**CEK1** はキャッシュに既に存在しているので、この手順は冗長です。 キーがエンクレーブにまだ存在しない場合に、データ所有者がエンクレーブにキーを提供できる方法を示すため、キーを追加しました。

   1. Always Encrypted が有効になって **いる** SSMS インスタンスにおいて、次のステートメントをクエリ ウィンドウで実行します。 そのステートメントでは、エンクレーブ対応の列のすべての暗号化キーがエンクレーブに送信されます。 詳しくは、「[sp_enclave_send_keys](../system-stored-procedures/sp-enclave-send-keys-sql.md)」をご覧ください。

        ```sql
        EXEC sp_enclave_send_keys;
        GO
        ```

   1. 上のストアド プロシージャを実行する代わりに、エンクレーブを使う DML クエリを **LastName** 列に対して実行してもかまいません。 これにより、エンクレーブに **CEK1** だけが設定されます。

        ```sql
        DECLARE @LastNamePrefix NVARCHAR(50) = 'Aber%';
        SELECT * FROM [HR].[Employees] WHERE [LastName] LIKE @LastNamePrefix;
        GO
        ```

1. DBA として、インデックスを作成します。
    1. Always Encrypted が有効になって **いない** SSMS インスタンスにおいて、次のステートメントをクエリ ウィンドウで実行します。

        ```sql
        CREATE INDEX IX_LastName ON [HR].[Employees] ([LastName])
        INCLUDE ([EmployeeID], [FirstName], [SSN], [Salary]);
        GO
        ```

1. データ所有者として、**LastName** 列に対して高度なクエリを実行し、クエリの実行時に SQL Server によってインデックスが使われることを確認します。
   1. Always Encrypted が有効になって **いる** SSMS インスタンスで、既存のクエリ ウィンドウを選択するか、または新しいクエリ ウィンドウを開き、ツール バーの **[ライブ クエリ統計を含む]** ボタンがオンになっていることを確認します。
   1. 下のクエリを実行します。 

        ```sql
        DECLARE @LastNamePrefix NVARCHAR(50) = 'Aber%';
        SELECT * FROM [HR].[Employees] WHERE [LastName] LIKE @LastNamePrefix;
        GO
        ```

   1. **[ライブ クエリ統計]** (クエリ ウィンドウの下部) で、クエリによりインデックスが使われていることを確認します。

## <a name="next-steps"></a>次のステップ
- [チュートリアル:セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する .NET アプリケーションの開発](../../connect/ado-net/sql/tutorial-always-encrypted-enclaves-develop-net-apps.md)」をご覧ください。
- [チュートリアル:セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する .NET Framework アプリケーションの開発](tutorial-always-encrypted-enclaves-develop-net-framework-apps.md)

## <a name="see-also"></a>関連項目
- [セキュリティで保護されたエンクレーブ列が設定された Always Encrypted でのインデックスの作成と使用](encryption/always-encrypted-enclaves-create-use-indexes.md)
