---
title: セキュリティで保護されたエンクレーブを使用して Transact-SQL ステートメントを実行する
description: データ定義言語 (DDL) のステートメントを実行して、列の暗号化を構成したり、暗号化された列のインデックスを管理したり、暗号化された列のクエリを実行したりします
ms.custom: ''
ms.date: 01/15/2021
ms.reviewer: vanto
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 130d2a9f2d92a77ab2d2e033f8e5f4fb9f88ef9f
ms.sourcegitcommit: 9413ddd8071da8861715c721b923e52669a921d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "101837668"
---
# <a name="run-transact-sql-statements-using-secure-enclaves"></a>セキュリティで保護されたエンクレーブを使用して Transact-SQL ステートメントを実行する

[!INCLUDE [sqlserver2019-windows-only-asdb](../../../includes/applies-to-version/sqlserver2019-windows-only-asdb.md)]

[セキュリティで保護されたエンクレーブが設定された Always Encrypted](always-encrypted-enclaves.md) を使用すると、一部の Transact-SQL (T-SQL) ステートメントで、サーバー側のセキュリティで保護されたエンクレーブ内にある暗号化されたデータベース列に対して機密計算を実行できます。

## <a name="statements-using-secure-enclaves"></a>セキュリティで保護されたエンクレーブを使用するステートメント

次の種類の T-SQL ステートメントで、セキュリティで保護されたエンクレーブが利用されます。

### <a name="ddl-statements-using-secure-enclaves"></a>セキュリティで保護されたエンクレーブを使用する DDL ステートメント

次の種類の[データ定義言語 (DDL)](../../../t-sql/statements/statements.md#data-definition-language) ステートメントを使用するときは、セキュリティで保護されたエンクレーブが必要です。

- エンクレーブ対応キーを使用するインプレース暗号化操作をトリガーする [ALTER TABLE column_definition (Transact-SQL)](../../../t-sql/statements/alter-table-column-definition-transact-sql.md) ステートメント。 詳細については、「[セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して列の暗号化をインプレースで構成する](always-encrypted-enclaves-configure-encryption.md)」を参照してください。
- ランダム化された暗号化を使用してエンクレーブ対応列のインデックスを作成または変更する [CREATE INDEX (Transact-SQL)](../../../t-sql/statements/create-index-transact-sql.md) および [ALTER INDEX (Transact-SQL)](../../../t-sql/statements/alter-index-transact-sql.md) ステートメント。 詳細については、「[セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する列でインデックスを作成して使用する](always-encrypted-enclaves-create-use-indexes.md)」を参照してください。
  
### <a name="dml-statements-using-secure-enclaves"></a>セキュリティで保護されたエンクレーブを使用する DML ステートメント

ランダム化された暗号化を使用するエンクレーブ対応列に対して次の[データ操作言語 (DML)](../../../t-sql/statements/statements.md#data-manipulation-language) ステートメントまたはクエリを使用するには、セキュリティで保護されたエンクレーブが必要です。

- セキュリティで保護されたエンクレーブ内でサポートされている次の Transact-SQL 演算子の 1 つ以上を使用するクエリ:
  - [比較演算子](../../../mdx/comparison-operators.md)
  - [BETWEEN (Transact-SQL)](../../../t-sql/language-elements/between-transact-sql.md)
  - [IN (Transact-SQL)](../../../t-sql/language-elements/in-transact-sql.md)
  - [LIKE (Transact-SQL)](../../../t-sql/language-elements/like-transact-sql.md)
  - [DISTINCT](../../../t-sql/queries/select-transact-sql.md#c-using-distinct-with-select)
  - [結合](../../performance/joins.md) - [!INCLUDE[sql-server-2019](../../../includes/sssql19-md.md)]入れ子になったループ結合のみがサポートされます。 [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] では、入れ子になったループ、ハッシュ、マージ結合がサポートされます
  - [SELECT - ORDER BY 句 (Transact-SQL)](../../../t-sql/queries/select-order-by-clause-transact-sql.md) [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] でサポートされます。 [!INCLUDE[sql-server-2019](../../../includes/sssql19-md.md)]
  - [SELECT - GROUP BY 句 (Transact-SQL)](../../../t-sql/queries/select-group-by-transact-sql.md). [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] でサポートされます。 [!INCLUDE[sql-server-2019](../../../includes/sssql19-md.md)]
- 行を挿入、更新、または削除するクエリ。これにより、エンクレーブ対応列のインデックスのインデックス キーの挿入または削除がトリガーされます。 詳細については、「[セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する列でインデックスを作成して使用する](always-encrypted-enclaves-create-use-indexes.md)」を参照してください。

> [!NOTE]
> エンクレーブを使用するインデックスおよび機密 DML クエリに対する操作は、ランダム化された暗号化を使用するエンクレーブ対応列でのみサポートされます。 決定論的な暗号化はサポートされていません。
>
> [!INCLUDE[sql-server-2019](../../../includes/sssql19-md.md)] では、文字列型の列 (`char`、`nchar`) に対してエンクレーブを使用する機密クエリを実行するには、列にバイナリ 2 並べ替え順序 (BIN2) の照合順序が構成されている必要があります。 [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] では、BIN2 または UTF-8 の照合順序を使用する必要があります。

### <a name="dbcc-commands-using-secure-enclaves"></a>セキュリティで保護されたエンクレーブを使用する DBCC コマンド

ランダム化された暗号化を使用するエンクレーブ対応列のインデックスがデータベースに含まれている場合は、インデックスの整合性のチェックを伴う [DBCC (Transact-SQL)](../../../t-sql/database-console-commands/dbcc-transact-sql.md) の管理コマンドでも、セキュリティで保護されたエンクレーブが必要になることがあります。 たとえば、[DBCC CHECKDB (Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) や [DBCC CHECKTABLE (Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md) などです。

## <a name="prerequisites-for-running-statements-using-secure-enclaves"></a>セキュリティで保護されたエンクレーブを使用してステートメントを実行するための前提条件

セキュリティで保護されたエンクレーブを使用するステートメントの実行をサポートするには、環境で次の要件が満たされている必要があります。

- [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] インスタンス、または [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] 内のデータベースとサーバーが、エンクレーブと構成証明をサポートするように正しく構成されている必要があります。 詳細については、「[セキュリティで保護されたエンクレーブと構成証明を設定する](configure-always-encrypted-enclaves.md#set-up-the-secure-enclave-and-attestation)」を参照してください。
- 構成証明サービスの管理者から、環境用の構成証明 URL を入手する必要があります。

  - [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] とホスト ガーディアン サービス (HGS) を使用している場合は、「[HGS 構成証明 URL を確認して共有する](always-encrypted-enclaves-host-guardian-service-deploy.md#step-6-determine-and-share-the-hgs-attestation-url)」を参照してください。
  - [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] と Microsoft Azure Attestation を使用している場合は、「[構成証明ポリシーの構成証明 URL を確認する](./always-encrypted-enclaves.md?view=sql-server-ver15#secure-enclave-attestation)」を参照してください。

- アプリケーションを使用してデータベースに接続している場合は、セキュリティで保護されたエンクレーブが設定された Always Encrypted がサポートされているクライアント ドライバーを使用する必要があります。 アプリケーションは、データベース接続で Always Encrypted が有効になっており、構成証明プロトコルと構成証明 URL が適切に構成されているデータベースに接続する必要があります。 詳細については、「[セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するアプリケーションを開発する](always-encrypted-enclaves-client-development.md)」を参照してください。
- SQL Server Management Studio (SSMS) または Azure SQL Data Studio を使用している場合は、データベースに接続するときに、Always Encrypted を有効にし、構成証明プロトコルと構成証明 URL を構成する必要があります。 詳細については、以下のセクションを参照してください。

> [!NOTE]
> キャッシュされた列暗号化キーを使用している場合、次の操作には、Always Encrypted と構成証明を構成してデータベースに接続する必要はありません。インデックスを作成または変更する DDL クエリ、インデックスを更新する DML クエリ、インデックスの整合性をチェックする DBCC コマンド。 詳細については、「[キャッシュされた列暗号化キーを使用してインデックス付け操作を呼び出す](always-encrypted-enclaves-create-use-indexes.md#invoke-indexing-operations-using-cached-column-encryption-keys)」を参照してください。

### <a name="prerequisites-for-running-t-sql-statements-using-enclaves-in-ssms"></a>SSMS でエンクレーブを使用して T-SQL ステートメントを実行するための前提条件

SQL Server Management Studio での最小バージョン要件:

- SSMS 18.3 ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を使用する場合)。
- SSMS 18.8 ([!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] を使用する場合)。

Always Encrypted と正しい構成証明 URL が構成されている接続を使用するクエリ ウィンドウから、ステートメントを実行してください。

1. **[サーバーへの接続]** ダイアログで、サーバーの名前を指定し、認証方法を選択して、資格情報を指定します。
2. **[オプション >>]** をクリックして、 **[Always Encrypted]** タブを選択します。
3. **[Always Encrypted を有効にする (列の暗号化)]** チェック ボックスをオンにして、エンクレーブ構成証明 URL を指定します。 たとえば、`https://hgs.bastion.local/Attestation` または `https://contososqlattestation.uks.attest.azure.net/attest/SgxEnclave` です。

    ![SSMS を使用して、構成証明を指定してサーバーに接続する](./media/always-encrypted-enclaves/column-encryption-setting.png)

4. **[接続]** を選択します。
5. Always Encrypted クエリのパラメーター化を有効にするように求められたら、パラメーター化された DML クエリを実行する場合は、 **[有効]** を選択します。 詳細については、「[Always Encrypted のパラメーター化](always-encrypted-query-columns-ssms.md#param)」を参照してください。

詳細については、「[データベース接続での Always Encrypted の有効化と無効化](always-encrypted-query-columns-ssms.md#en-dis)」を参照してください。

### <a name="prerequisites-for-running-t-sql-statements-using-enclaves-in-azure-data-studio"></a>Azure Data Studio でエンクレーブを使用して T-SQL ステートメントを実行するための前提条件

推奨される最小バージョンは **1.23** 以降です。

Always Encrypted が有効になっていて、正しい構成証明プロトコルと構成証明 URL の両方が構成されている接続を使用するクエリ ウィンドウから、ステートメントを実行してください。

1. **[接続]** ダイアログで、 **[詳細...]** をクリックします。
2. 接続に対して Always Encrypted を有効にするには、 **[Always Encrypted]** フィールドを **[有効]** に設定します。
3. 構成証明プロトコルと構成証明 URL を指定します。
    - [!INCLUDE [sssql19-md](../../../includes/sssql19-md.md)] を使用している場合は、**構成証明プロトコル** を **ホスト ガーディアン サービス** に設定し、ホスト ガーディアン サービスの構成証明 URL を **[エンクレーブ構成証明 URL]** フィールドに入力します。
    - [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] を使用している場合は、**構成証明プロトコル** を **Azure Attestation** に設定し、Microsoft Azure Attestation でポリシーを参照する構成証明 URL を **[エンクレーブ構成証明 URL]** フィールドに入力します。

    ![Azure Data Studio を使用し、構成証明を指定してサーバーに接続する](./media/always-encrypted-enclaves/azure-data-studio-connect-with-enclaves.png)

4. **[OK]** をクリックして **[詳細プロパティ]** を閉じます。

詳細については、「[データベース接続での Always Encrypted の有効化と無効化](always-encrypted-query-columns-ads.md#enabling-and-disabling-always-encrypted-for-a-database-connection)」を参照してください。

パラメーター化された DML クエリを実行する場合は、[Always Encrypted に対してパラメーター化](always-encrypted-query-columns-ads.md#parameterization-for-always-encrypted)を有効にする必要もあります。

## <a name="examples"></a>例

このセクションには、エンクレーブを使用する DML クエリの例が含まれます。 

例では次のスキーマを使用します。

```sql
CREATE SCHEMA [HR];
GO

CREATE TABLE [HR].[Jobs](
 [JobID] [int] IDENTITY(1,1) PRIMARY KEY,
 [JobTitle] [nvarchar](50) NOT NULL,
 [MinSalary] [money] ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
 [MaxSalary] [money] ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
);
GO

CREATE TABLE [HR].[Employees](
 [EmployeeID] [int] IDENTITY(1,1) PRIMARY KEY,
 [SSN] [char](11) ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
 [FirstName] [nvarchar](50) NOT NULL,
 [LastName] [nvarchar](50) NOT NULL,
 [Salary] [money] ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
 [JobID] [int] NULL,
 FOREIGN KEY (JobID) REFERENCES [HR].[Jobs] (JobID)
);
GO
```

### <a name="exact-match-search"></a>完全一致検索

次のクエリでは、暗号化された `SSN` 文字列型の列に対して完全一致検索を実行します。

```sql
DECLARE @SSN char(11) = '795-73-9838';
SELECT * FROM [HR].[Employees] WHERE [SSN] = @SSN;
GO
```

### <a name="pattern-matching-search"></a>パターン マッチング検索

次のクエリでは、暗号化された `SSN` 文字列型の列に対してパターン マッチング検索を実行し、社会保障番号の数字の末尾が指定したものである従業員を検索します。

```sql
DECLARE @SSN char(11) = '795-73-9838';
SELECT * FROM [HR].[Employees] WHERE [SSN] = @SSN;
GO
```

### <a name="range-comparison"></a>範囲比較

次のクエリでは、暗号化された `Salary` 列に対して範囲比較を実行し、給与が指定した範囲内である従業員を検索します。

```sql
DECLARE @MinSalary money = 40000;
DECLARE @MaxSalary money = 45000;
SELECT * FROM [HR].[Employees] WHERE [Salary] > @MinSalary AND [Salary] < @MaxSalary;
GO
```

### <a name="joins"></a>結合

次のクエリでは、暗号化された `Salary` 列を使用して、`Employees` テーブルと `Jobs` テーブルの間の結合を実行します。 このクエリにより、従業員の職務の給与範囲外の給与を受け取っている従業員が取得されます。

```sql
SELECT * FROM [HR].[Employees] e
JOIN [HR].[Jobs] j
ON e.[JobID] = j.[JobID] AND e.[Salary] > j.[MaxSalary] OR e.[Salary] < j.[MinSalary];
GO
```

### <a name="sorting"></a>並べ替え

次のクエリでは、暗号化された `Salary` 列に基づいて従業員レコードが並べ替えられて、給与が最高の 10 人の従業員が取得されます。
> [!NOTE]
> 暗号化された列の並べ替えは、[!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] ではサポートされていますが、[!INCLUDE[sql-server-2019](../../../includes/sssql19-md.md)] ではサポートされていません。

```sql
SELECT TOP(10) * FROM [HR].[Employees]
ORDER BY [Salary] DESC;
GO
```

## <a name="next-steps"></a>次の手順

- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するアプリケーションを開発する](always-encrypted-enclaves-client-development.md)

## <a name="see-also"></a>関連項目

- [セキュリティで保護されたエンクレーブが設定された Always Encrypted の一般的な問題をトラブルシューティングする](always-encrypted-enclaves-troubleshooting.md)
- [チュートリアル: SQL Server でのセキュリティで保護されたエンクレーブを使用する Always Encrypted の概要](../tutorial-getting-started-with-always-encrypted-enclaves.md)
- [チュートリアル: Azure SQL Database でのセキュリティで保護されたエンクレーブを使用する Always Encrypted の概要](/azure/azure-sql/database/always-encrypted-enclaves-getting-started)
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して列の暗号化をインプレースで構成する](always-encrypted-enclaves-configure-encryption.md)
- [セキュリティで保護されたエンクレーブ列が設定された Always Encrypted でのインデックスの作成と使用](always-encrypted-enclaves-create-use-indexes.md)