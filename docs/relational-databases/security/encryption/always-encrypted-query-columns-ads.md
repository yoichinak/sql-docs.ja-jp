---
description: Azure Data Studio で Always Encrypted を使用した列のクエリを実行する
title: Azure Data Studio で Always Encrypted を使用した列のクエリを実行する | Microsoft Docs
ms.custom: ''
ms.date: 5/19/2020
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 82315c744073fa5f497f0aaf78eb6dedc04126a9
ms.sourcegitcommit: 22e97435c8b692f7612c4a6d3fe9e9baeaecbb94
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/27/2020
ms.locfileid: "92679040"
---
# <a name="query-columns-using-always-encrypted-with-azure-data-studio"></a>Azure Data Studio で Always Encrypted を使用した列のクエリを実行する
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

この記事では、[Azure Data Studio](../../../azure-data-studio/what-is.md) を使用して [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) によって暗号化された列にクエリを実行する方法について説明します。 Azure Data Studio では、以下を実行できます。
- 暗号化された列に格納された暗号化テキスト値を取得する。 
- 暗号化された列に格納されたプレーンテキスト値を取得する。  
- 暗号化された列をターゲットとするプレーンテキスト値を送信する (たとえば、`INSERT` または `UPDATE` ステートメントや、`WHERE` ステートメントの `SELECT` 句のルックアップ パラメーターとして)。 

## <a name="retrieving-ciphertext-values-stored-in-encrypted-columns"></a>暗号化された列に格納された暗号化テキスト値の取得    
このセクションでは、暗号化された列に格納されているデータを暗号化テキストとして取得する方法について説明します。

### <a name="steps"></a>手順
1. 暗号化テキスト値を取得する `SELECT` クエリの実行元のクエリ ウィンドウのデータベース接続に対して Always Encrypted を無効にしていることを確認します。 以下の「[データベース接続での Always Encrypted の有効化と無効化](#enabling-and-disabling-always-encrypted-for-a-database-connection)」を参照してください。     
1. `SELECT` クエリを実行します。 暗号化された列から取得されたデータは、バイナリ (暗号化された) 値として返されます。   

### <a name="example"></a>例
`SSN` が `Patients` テーブルの暗号化された列であると仮定して、以下に示されているクエリでバイナリ暗号化テキスト値を取得します (Always Encrypted がデータベース接続で無効になっている場合)。   

![SELECT * FROM [dbo].[Patients] クエリと、バイナリ暗号化テキスト値として表示されたクエリの結果のスクリーンショット。](../../../relational-databases/security/encryption/media/always-encrypted-ads-query-ciphertext.png)
 
## <a name="retrieving-plaintext-values-stored-in-encrypted-columns"></a>暗号化された列に格納されたプレーンテキスト値の取得    
このセクションでは、暗号化された列に格納されているデータを暗号化テキストとして取得する方法について説明します。

### <a name="prerequisites"></a>前提条件
- Azure Data Studio バージョン 17.1 以降。
- 列マスター キーと、クエリの実行対象の列を保護するキーに関するメタデータにアクセスできる必要があります。 詳しくは、以下の「[暗号化された列にクエリを実行するためのアクセス許可](#permissions-for-querying-encrypted-columns)」を参照してください。
- 列マスター キーは、Windows 証明書ストアまたは Azure Key Vault に格納する必要があります。 Azure Data Studio はその他のキー ストアをサポートしていません。

### <a name="steps"></a>手順
1.  データを取得および暗号化解除する `SELECT` クエリの実行元のクエリ ウィンドウのデータベース接続に対して Always Encrypted を有効にします。 これにより、[Microsoft .NET Data Provider for SQL Server](../../../connect/ado-net/sql/sqlclient-support-always-encrypted.md) (Azure Data Studio で使用) は、クエリの結果セット内の暗号化された列の暗号化を解除するよう指示されます。 以下の「[データベース接続での Always Encrypted の有効化と無効化](#enabling-and-disabling-always-encrypted-for-a-database-connection)」を参照してください。
1.  `SELECT` クエリを実行します。 暗号化された列から取得されたデータは、元のデータ型のプレーンテキスト値として返されます。
 
### <a name="example"></a>例
SSN が `Patients` テーブルで暗号化された列であると仮定して、以下に示されているクエリでプレーンテキスト値を返します (Always Encrypted がデータベース接続で有効になっている場合、および `SSN` 列に構成された列マスター キーにアクセスできる場合)。   

![SELECT * FROM [dbo].[Patients] クエリと、プレーン テキスト値として表示されたクエリの結果のスクリーンショット。](../../../relational-databases/security/encryption/media/always-encrypted-ads-query-plaintext.png)
 
## <a name="sending-plaintext-values-targeting-encrypted-columns"></a>暗号化された列をターゲットとするプレーンテキスト値の送信       
このセクションでは、暗号化された列をターゲットとする値を送信するクエリを実行する方法について説明します。 たとえば、暗号化された列に格納されている値の挿入、更新、またはフィルター処理を行うクエリについて説明します。

### <a name="prerequisites"></a>前提条件
- Azure Data Studio バージョン 18.1 以降。
- 列マスター キーと、クエリの実行対象の列を保護するキーに関するメタデータにアクセスできる必要があります。 詳しくは、以下の「[暗号化された列にクエリを実行するためのアクセス許可](#permissions-for-querying-encrypted-columns)」を参照してください。
- 列マスター キーは、Windows 証明書ストアまたは Azure Key Vault に格納する必要があります。 Azure Data Studio はその他のキー ストアをサポートしていません。

### <a name="steps"></a>手順
1. データを取得および暗号化解除する `SELECT` クエリの実行元のクエリ ウィンドウのデータベース接続に対して Always Encrypted を有効にします。 これにより、[Microsoft .NET Data Provider for SQL Server](../../../connect/ado-net/sql/sqlclient-support-always-encrypted.md) (Azure Data Studio によって使用されます) は、暗号化された列をターゲットとするクエリ パラメーターを暗号化し、暗号化された列から取得した結果を復号化するように指示されます。 以下の「[データベース接続での Always Encrypted の有効化と無効化](#enabling-and-disabling-always-encrypted-for-a-database-connection)」を参照してください。 
1. クエリ ウィンドウの Always Encrypted のパラメーター化を有効にします。 詳細については、以下の「 [Always Encrypted のパラメーター化](#parameterization-for-always-encrypted) 」を参照してください。
1. Transact-SQL 変数を宣言し、データベースに送信 (挿入、更新またはフィルタリング) する値で初期化します。 
1. データベースに Transact-SQL 変数の値を送信するクエリを実行します。 Azure Data Studio は変数をクエリ パラメーターに変換し、その値を暗号化してからデータベースに送信します。   

### <a name="example"></a>例
`SSN` が `Patients` テーブルの暗号化された `char(11)` 列であるとすると、次のスクリプトによって、SSN 列に `'795-73-9838'` が含まれる行が検索されます。 データベース接続に対して Always Encrypted が有効になっており、クエリ ウィンドウで Always Encrypted のパラメーター化が有効になっていて、かつ `SSN` 列に対して構成されている列マスター キーにアクセスできる場合は、結果が返されます。   

![DECLARE @SSN char(11) = '795-73-9838' SELECT * FROM [dbo].[Patients] WHERE [SSN] = @SSN クエリとクエリ結果のスクリーンショット。](../../../relational-databases/security/encryption/media/always-encrypted-ads-query-parameters.png)

## <a name="permissions-for-querying-encrypted-columns"></a>暗号化された列にクエリを実行するためのアクセス許可

暗号化された列に対してクエリ (暗号化テキストでデータを取得するクエリを含む) を実行するには、データベースの **VIEW ANY COLUMN MASTER KEY DEFINITION** 権限と **VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** 権限が必要です。

これらの権限に加え、クエリ結果を暗号化解除する場合や、(Transact-SQL 変数をパラメーター化することで生成される) クエリ パラメーターを暗号化する場合には、ターゲット列を保護する列マスター キーにアクセスする必要もあります。

- **証明書ストア - ローカル コンピューター:** 列マスター キーとして使用される証明書への **読み取り** アクセス権を持っているか、コンピューターの管理者である必要があります。   
- **Azure Key Vault:** 列マスター キーが格納されているキー コンテナーに対する **get** 、 **unwrapKey** 、および **verify** の権限が必要です。

詳細については、 [列マスター キーの作成と格納 (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md) を参照してください。

## <a name="enabling-and-disabling-always-encrypted-for-a-database-connection"></a>データベース接続での Always Encrypted の有効化と無効化   
Azure Data Studio でデータベースに接続する場合は、データベース接続について Always Encrypted を有効または無効にすることができます。 既定では、Always Encrypted は無効になっています。 

データベース接続で Always Encrypted を有効にすると、以下の操作を透過的に試行するように、Azure Data Studio で使用される [Microsoft .NET Data Provider for SQL Server](../../../connect/ado-net/sql/sqlclient-support-always-encrypted.md) に指示されます。   
-   暗号化された列から取得され、クエリ結果に返される値の暗号化を解除する。   
-   暗号化されたデータベース列をターゲットとするパラメーター化された Transact-SQL 変数の値を暗号化する。   

接続に対して Always Encrypted を有効にしなかった場合、Microsoft .NET Data Provider for SQL Server は、クエリ パラメーターの暗号化や結果の暗号化解除を試行しません。

データベースに接続するときに、Always Encrypted を有効または無効にすることができます。 データベースへの接続方法に関する一般的な情報については、以下を参照してください。
- [クイック スタート: Azure Data Studio を使用して SQL Server への接続とクエリを実行する](../../../azure-data-studio/quickstart-sql-server.md)
- [クイック スタート: Azure Data Studio を使用した Azure SQL データベースに対する接続およびクエリ](../../../azure-data-studio/quickstart-sql-database.md)

Always Encrypted を有効 (無効) にするには、次のようにします。
1. **[接続]** ダイアログで、 **[詳細...]** をクリックします。
2. 接続に対して Always Encrypted を有効にするには、 **[Always Encrypted]** フィールドを **[有効]** に設定します。 Always Encrypted を無効にするには、 **[Always Encrypted]** の値を空白のままにするか、 **[無効]** に設定します。
3. [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] を使用して SQL Server インスタンスがセキュア エンクレーブで構成されている場合は、エンクレーブ プロトコルおよびエンクレーブ構成証明の URL を指定できます。 SQL Server インスタンスでセキュア エンクレーブを使用しない場合は、 **[Attestation Protocol]** (構成証明プロトコル) および **[エンクレーブ構成証明 URL]** フィールドを空白のままにしてください。 詳細については、「[セキュア エンクレーブを使用する Always Encrypted](always-encrypted-enclaves.md)」を参照してください。
4. **[OK]** をクリックして **[詳細プロパティ]** を閉じます。

![接続に対して Always Encrypted を有効にする手順を示す短い動画。](../../../relational-databases/security/encryption/media/always-encrypted-ads-connect.gif)

> [!TIP]
> 既存のクエリ ウィンドウで Always Encrypted を有効または無効に切り替えるには、 **[切断]** をクリックしてから **[接続]** をクリックし、上記の手順を完了して、 **[Always Encrypted]** フィールドの目的の値を使用してデータベースに再接続します。 

> [!NOTE] 
> 現在、クエリ ウィンドウの **[接続の変更]** ボタンでは、Always Encrypted の有効と無効の切り替えをサポートしていません。

## <a name="parameterization-for-always-encrypted"></a>Always Encrypted のパラメーター化

Always Encrypted のパラメーター化は、Transact-SQL 変数をクエリ パラメーター ([SqlParameter クラス](/dotnet/api/microsoft.data.sqlclient.sqlparameter)のインスタンス) に自動的に変換する Azure Data Studio 18.1 以降の機能です。 これにより、基になる [Microsoft .NET Data Provider for SQL Server](../../../connect/ado-net/sql/sqlclient-support-always-encrypted.md) は暗号化された列をターゲットとするデータを検出し、データベースに送信する前にそのデータを暗号化できます。
  
パラメーター化しないと、Microsoft .NET Data Provider for SQL Server は、クエリ ウィンドウで作成される各ステートメントを非パラメーター化クエリとして渡します。 クエリに、暗号化された列をターゲットとする Transact-SQL 変数またはリテラルが含まれている場合、.NET Framework Data Provider for SQL Server では、データベースにクエリを送信する前に、データを検出して暗号化することはできません。 その結果、(プレーンテキストのリテラル Transact-SQL 変数と暗号化された列の間で) 型が一致しないため、クエリは失敗します。 たとえば、 `SSN` 列が暗号化されていると仮定して、パラメーター化せずに以下のクエリを正常に実行することはできません。   

```sql
DECLARE @SSN CHAR(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN
```

### <a name="enabling-and-disabling-parameterization-for-always-encrypted"></a>Always Encrypted のパラメーター化の有効化/無効化

既定では、Always Encrypted のパラメーター化は無効になっています。

Always Encrypted のパラメーター化の有効/無効を切り替えるには、以下の手順を実行します。

1. **[ファイル]**  >  **[基本設定]**  >  **[設定]** (Mac の場合 **[コード]**  >  **[基本設定]**  >  **[設定]** ) を選択します。
2. **[データ]**  >  **[Microsoft SQL Server]** に移動します。
3. **[Always Encrypted のパラメーター化を有効にする]** を選択または選択解除します。
4. **[設定]** ウィンドウを閉じます。

![Always Encrypted のパラメーター化の有効または無効を切り替える手順を示す短い動画。](../../../relational-databases/security/encryption/media/always-encrypted-ads-parameterization.gif)

> [!NOTE]
> Always Encrypted のパラメーター化は、Always Encrypted が有効にされたデータベース接続を使用するクエリでのみ機能します (「[データベース接続での Always Encrypted の有効化と無効化](#enabling-and-disabling-always-encrypted-for-a-database-connection)」を参照してください)。 クエリ ウィンドウで Always Encrypted が有効な状態ではないデータベース接続を使用すると、Transact-SQL 変数がパラメーター化されません。

### <a name="how-parameterization-for-always-encrypted-works"></a>Always Encrypted のパラメーター化のしくみ

クエリ ウィンドウで Always Encrypted のパラメーター化と Always Encrypted の両方が有効になっている場合、Azure Data Studio は、次の前提条件を満たす Transact-SQL 変数のパラメーター化を試みます。

- 同じステートメントで宣言され、初期化 (インライン初期化) されている。 別個の `SET` ステートメントを使用して宣言された変数はパラメーター化されません。
- 単一のリテラルを使用して初期化されている。 演算子または関数を含む式を使用して初期化された変数はパラメーター化されません。

Azure Data Studio がパラメーター化する変数の例を以下に示します。

```sql
DECLARE @SSN char(11) = '795-73-9838';
   
DECLARE @BirthDate date = '19990104';
DECLARE @Salary money = $30000;
```

Azure Data Studio がパラメーター化を試みない変数の例を以下に示します。

```sql
DECLARE @Name nvarchar(50); --Initialization separate from declaration
SET @Name = 'Abel';

DECLARE @StartDate date = GETDATE(); -- a function used instead of a literal

DECLARE @NewSalary money = @Salary * 1.1; -- an expression used instead of a literal
```
 
試行されたパラメーター化が正常に行われるようにするには   
- パラメーター化する変数の初期化で使用されるリテラルの型は、変数宣言の型と一致する必要があります。   
- 変数の宣言された型が date 型または time 型である場合、以下の ISO 8601 に準拠した形式のいずれかを使用する文字列で変数を初期化する必要があります。   

パラメーター化エラーの原因となる Transact-SQL 変数宣言の例を以下に示します。

```sql
DECLARE @BirthDate date = '01/04/1999' -- unsupported date format   
   
DECLARE @Number int = 1.1 -- the type of the literal does not match the type of the variable   
```

Azure Data Studio では Intellisense を使用して、正常にパラメーター化できた変数と失敗したパラメーター化の試行 (およびその理由) を通知します。   

クエリ ウィンドウでは、正常にパラメーター化できた変数の宣言に、情報メッセージの下線が付けられます。 情報メッセージの下線が付いた宣言ステートメントにカーソルを置くと、パラメーター化プロセスの結果を含むメッセージが表示されます。これには、結果の [SqlParameter クラス](/dotnet/api/microsoft.data.sqlclient.sqlparameter) オブジェクトの主要なプロパティの値が含まれます (変数が [SqlDbType](/dotnet/api/microsoft.data.sqlclient.sqlparameter.dbtype)、[Size](/dotnet/api/microsoft.data.sqlclient.sqlparameter.size)、[Precision](/dotnet/api/microsoft.data.sqlclient.sqlparameter.precision)、[Scale](/dotnet/api/microsoft.data.sqlclient.sqlparameter.scale)、[SqlValue](/dotnet/api/microsoft.data.sqlclient.sqlparameter.sqlvalue) にマップされます)。 また、 **[問題]** ビューには、正常にパラメーター化されたすべての変数の完全な一覧も表示されます。 **[問題]** ビューを開くには、 **[ビュー]**  >  **[問題]** を選択します。    



Azure Data Studio が変数のパラメーター化を試みたときに、パラメーター化が失敗した場合には、変数の宣言にエラーの下線が付けられます。 エラーの下線が付けられた宣言ステートメントにカーソルを置くと、エラーに関する結果が表示されます。 また、 **[問題]** ビューで、すべての変数のパラメーター化エラーの完全な一覧を表示することもできます。

 
> [!NOTE]
> Always Encrypted でサポートされる型変換のサブセットは限られているため、多くの場合、Transact-SQL 変数のデータ型が、ターゲットとなるターゲット データベース列の型と同じである必要があります。 たとえば、`SSN` テーブル内の `Patients` 列の型が `char(11)` であると仮定して、`nchar(11)` である `@SSN` 変数の型が列の型と一致しないため、以下のクエリは失敗します。   

```sql
DECLARE @SSN nchar(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN;
```

```output
Msg 402, Level 16, State 2, Line 5   
The data types char(11) encrypted with (encryption_type = 'DETERMINISTIC', 
encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
column_encryption_key_database_name = 'Clinic') collation_name = 'Latin1_General_BIN2' 
and nchar(11) encrypted with (encryption_type = 'DETERMINISTIC', 
encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
column_encryption_key_database_name = 'Clinic') are incompatible in the equal to operator.
```

> [!NOTE]
> パラメーター化しないと、型変換を含め、クエリ全体が SQL Server/Azure SQL Database 内で処理されます。 パラメーター化を有効にすると、Azure Data Studio 内の Microsoft .NET Data Provider for SQL Server によって、一部の型変換が実行されます。 Microsoft .NET 型システムと SQL Server 型システムには違いがある (float など、いくつかの型の精度が異なる) ため、パラメーター化を有効にして実行されたクエリでは、パラメーター化を有効にせずに実行されたクエリとは異なる結果が生成される場合があります。 

## <a name="next-steps"></a>次の手順
- [Always Encrypted を使用したアプリケーションの開発](always-encrypted-client-development.md)


## <a name="see-also"></a>参照
- [常に暗号化](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)