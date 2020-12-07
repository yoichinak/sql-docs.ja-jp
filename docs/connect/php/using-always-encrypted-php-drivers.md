---
title: SQL Server 用 PHP ドライバーと共に Always Encrypted を使用する
description: SQL Server 用 PHP ドライバーと共に Always Encrypted を使用し、アプリケーションの機密データを保護する方法について説明します。
ms.date: 12/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: v-kaywon
ms.author: v-daenge
author: David-Engel
manager: v-mabarw
ms.openlocfilehash: fc89f54ca7ab27aad141b8f1bd9bc386d613bcd5
ms.sourcegitcommit: 2600a414c321cfd6dc6daf5b9bcbc9a99c049dc4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603405"
---
# <a name="using-always-encrypted-with-the-php-drivers-for-sql-server"></a>SQL Server 用 PHP ドライバーと共に Always Encrypted を使用する
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="applicable-to"></a>次に対して適用可能
 -   Microsoft SQL Server 用 Drivers 5.2 for PHP
 
## <a name="introduction"></a>はじめに

この記事では、[Always Encrypted (データベース エンジン)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) と [SQL Server 用 PHP ドライバー](../../connect/php/Microsoft-php-driver-for-sql-server.md)を使用して PHP アプリケーションを開発する方法について説明します。

Always Encrypted を使用すると、クライアント アプリケーションは SQL Server または Azure SQL データベースにデータまたは暗号化キーを開示することなく、機密データを暗号化することができます。 ODBC Driver for SQL Server など、Always Encrypted が有効なドライバーは、クライアント アプリケーション内の機密データを透過的に暗号化および暗号化解除します。 ドライバーは、どのクエリ パラメーターが機密データベース列 (Always Encrypted を使用して保護される) に対応するかを自動的に決定し、SQL Server または Azure SQL データベースにデータを渡す前にこれらのパラメーターの値を暗号化します。 同様に、ドライバーは、クエリ結果内の暗号化されたデータベース列から取得されたデータを透過的に暗号化解除します。 詳細については、「 [Always Encrypted (データベース エンジン)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)」を参照してください。 SQL Server 用 PHP ドライバーでは、機密データを暗号化するために、ODBC Driver for SQL Server を使用します。

## <a name="prerequisites"></a>前提条件

 -   データベースで Always Encrypted を構成します。 この構成には、Always Encrypted キーのプロビジョニング、および選択したデータベース列の暗号化の設定が含まれます。 Always Encrypted が構成されたデータベースがない場合は、「 [Always Encrypted の作業の開始](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)」の手順に従います。 特に、ご利用のデータベースには、列マスターキー (CMK) 用、列暗号化キー (CEK) 用、およびその CEK を使用して暗号化された 1 つまたは複数の列を含むテーブル用のメタデータ定義を含める必要があります。
 -   開発用コンピューターに ODBC Driver for SQL Server バージョン 17 以降がインストールされていることを確認します。 詳細については、「[SQL Server 用 ODBC Driver](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)」を参照してください。

## <a name="enabling-always-encrypted-in-a-php-application"></a>PHP アプリケーションで Always Encrypted を有効にする

暗号化された列をターゲットとするパラメーターの暗号化と、クエリ結果の暗号化解除を有効にする最も簡単な方法としては、`ColumnEncryption` 接続文字列キーワードの値を `Enabled` に設定します。 SQLSRV および PDO_SQLSRV ドライバーで Always Encrypted を有効化する例を次に示します。

SQLSRV:
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled");
$conn = sqlsrv_connect($server, $connectionInfo);
```

PDO_SQLSRV:
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```

暗号化または暗号化解除を正常に行うには、Always Encrypted を有効にするだけでは不十分です。さらに、次のようになっていることを確認する必要があります。
 -   アプリケーションが、データベース内の Always Encrypted キーに関するメタデータへのアクセスに必要な VIEW ANY COLUMN MASTER KEY DEFINITION および VIEW ANY COLUMN ENCRYPTION KEY DEFINITION データベース権限を持っています。 詳細については、[データベース権限](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)に関するページをご覧ください。
 -   アプリケーションで、クエリ対象の暗号化された列の CEK を保護する CMK にアクセスできる。 この要件は、CMK を格納するキー ストア プロバイダーに応じて異なります。 詳細については、「[列マスター キー ストアを操作する](#working-with-column-master-key-stores)」をご覧ください。

## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>暗号化された列のデータを取得および変更する

接続に対して Always Encrypted を有効にすると、標準の SQLSRV API (「[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)」を参照) または PDO_SQLSRV API (「[PDO_SQLSRV ドライバー API リファレンス](../../connect/php/pdo-sqlsrv-driver-reference.md)」を参照) を使用して、暗号化されたデータベース列内のデータを取得または変更することができます。 ご利用のアプリケーションが必要なデータベース権限を備えていて、列マスター キーにアクセスできると仮定すると、ドライバーによって、暗号化された列をターゲットとするクエリ パラメータが暗号化され、暗号化された列から取得したデータの暗号化が解除されます。これらの動作は列が暗号化されていないかのようにアプリケーションに対して透過的に行われます。

Always Encrypted が有効でない場合、暗号化された列をターゲットとするパラメーターを含むクエリは失敗します。 暗号化された列をターゲットとするパラメーターがクエリにない場合は、暗号化された列からデータを取得できます。 ただし、ドライバーによって暗号化の解除は試みられず、アプリケーションでは暗号化されたバイナリ データを (バイト配列として) 受け取ることになります。

次の表は、Always Encrypted が有効かどうかに応じたクエリの動作をまとめたものです。

|クエリの特性|Always Encrypted が有効になっており、アプリケーションがキーとキー メタデータにアクセスできる|Always Encrypted が有効になっており、アプリケーションがキーまたはキー メタデータにアクセスできない|Always Encrypted が無効になっている|
|---|---|---|---|
|暗号化された列をターゲットとするパラメーター。|パラメーター値は透過的に暗号化されます。|エラー|エラー|
|暗号化された列をターゲットとするパラメーターを含まない、暗号化された列からのデータの取得。|暗号化された列の結果は透過的に暗号化解除されます。 アプリケーションでは、プレーン テキスト列の値を受け取ります。 |エラー|暗号化された列の結果は暗号化解除されません。 アプリケーションは、暗号化された値をバイト配列として受け取ります。|
 
次の例は、暗号化された列のデータを取得および変更する方法を示しています。 この例では、次のスキーマを持つテーブルを想定しています。 SSN 列と BirthDate 列は暗号化されています。
```
CREATE TABLE [dbo].[Patients](
 [PatientId] [int] IDENTITY(1,1),
 [SSN] [char](11) COLLATE Latin1_General_BIN2
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = CEK1) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL,
 [BirthDate] [date]
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = CEK1) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY])
 GO
```

### <a name="data-insertion-example"></a>データ挿入の例

次の例は、SQLSRV および PDO_SQLSRV ドライバーを使用して Patient テーブルに行を挿入する方法を示しています。 以下の点に注意してください。
 -   このサンプル コードの暗号化に固有のものは何もありません。 暗号化された列をターゲットとする SSN および BirthDate パラメーターの値が、ドライバーによって自動的に検出されて、暗号化されます。 このメカニズムにより、アプリケーションに対して暗号化が透過的に実行されます。
 -   暗号化された列を含め、データベース列に挿入された値は、バインドされたパラメーターとして渡されます。 暗号化されていない列に値を送信する場合、パラメーターの使用は省略可能です (ただし、SQL インジェクションを防ぐのに役立つので、強くお勧めします) が、暗号化された列をターゲットとする値に対しては必須です。 SSN 列または BirthDate 列に挿入された値がクエリ ステートメントに埋め込まれたリテラルとして渡された場合、ドライバーではクエリ内のリテラルの暗号化または処理が試行されないため、クエリは失敗します。 その結果、サーバーはこれらの値を、暗号化された列と互換性がないと見なして拒否します。
 -   バインド パラメーターを使用して値を挿入する場合、ターゲット列のデータ型と一致する SQL 型またはターゲット列のデータ型への変換がサポートされている SQL 型が、データベースに渡される必要があります。 この要件は、Always Encrypted では、ほとんどの型変換がサポートされていないためです (詳細については、[「Always Encrypted」(データベース エンジン) ](../../relational-databases/security/encryption/always-encrypted-database-engine.md)を参照してください)。 2 つの PHP ドライバーである SQLSRV と PDO_SQLSRV では、ユーザーが値の SQL 型を決定できるメカニズムが、それぞれに用意されています。 そのため、ユーザーは SQL 型を明示的に指定する必要はありません。
  -   SQLSRV ドライバーの場合、ユーザーには 2 つのオプションが用意されています。
   -   PHP ドライバーを利用して、適切な SQL 型を決めて設定する。 この場合、ユーザーは `sqlsrv_prepare` および `sqlsrv_execute` を使用して、パラメーター化クエリを実行する必要があります。
   -   SQL 型を明示的に設定する。
  -   PDO_SQLSRV ドライバーの場合、ユーザーが明示的にパラメーターの SQL 型を設定するオプションは用意されていません。 PDO_SQLSRV ドライバーでは、パラメーターをバインドするときに、ユーザーによる SQL 型の決定が自動的に行われます。
 -   ドライバーによって SQL 型が決定されるためには、いくつかの制限事項が適用されます。
  -   SQLSRV ドライバー:
   -   暗号化された列の SQL 型がドライバーによって決定されることをユーザーが希望する場合、そのユーザーは `sqlsrv_prepare` および `sqlsrv_execute` を使用する必要があります。
   -   `sqlsrv_query` を選ぶ場合、ユーザーは、すべてのパラメーターの SQL 型を指定する必要があります。 指定された SQL 型には、文字列型の文字列の長さと、10 進数型の小数点以下桁数および有効桁数が含まれる必要があります。
  -   PDO_SQLSRV ドライバー:
   -   ステートメント属性 `PDO::SQLSRV_ATTR_DIRECT_QUERY` は、パラメーター化クエリではサポートされていません。
   -   ステートメント属性 `PDO::ATTR_EMULATE_PREPARES` は、パラメーター化クエリではサポートされていません。
   
SQLSRV ドライバーおよび [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md):
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Abel;
$birthDate = "1996-10-19";
$params = array($ssn, $firstName, $lastName, $birthDate);
// during sqlsrv_prepare, the driver determines the SQL types for each parameter and pass them to SQL server
$stmt = sqlsrv_prepare($conn, $query, $params);
sqlsrv_execute($stmt);
```

SQLSRV ドライバーおよび [sqlsrv_query](../../connect/php/sqlsrv-query.md):
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Abel";
$birthDate = "1996-10-19";
// need to provide the SQL types for ALL parameters  
// note the SQL types (including the string length) have to be the same at the column definition
$params = array(array(&$ssn, null, null, SQLSRV_SQLTYPE_CHAR(11)),
                array(&$firstName, null, null, SQLSRV_SQLTYPE_NVARCHAR(50)),
                array(&$lastName, null, null, SQLSRV_SQLTYPE_NVARCHAR(50)),
                array(&$birthDate, null, null, SQLSRV_SQLTYPE_DATE));
sqlsrv_query($conn, $query, $params);
```

PDO_SQLSRV ドライバーおよび [PDO::prepare](../../connect/php/pdo-prepare.md):
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Able";
$birthDate = "1996-10-19";
// during PDO::prepare, the driver determines the SQL types for each parameter and pass them to SQL server
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $ssn);
$stmt->bindParam(2, $firstName);
$stmt->bindParam(3, $lastName);
$stmt->bindParam(4, $birthDate);
$stmt->execute();
```

### <a name="plaintext-data-retrieval-example"></a>プレーンテキスト データの取得の例

次の例は、SQLSRV および PDO_SQLSRV ドライバーを使用して、暗号化された値に基づいてデータをフィルター処理し、暗号化された列からプレーンテキスト データを取得する方法を示しています。 以下の点に注意してください。
 -   バインド パラメーターを使用して SSN 列に対してフィルター処理するために WHERE 句で使用される値は、サーバーに送信する前にドライバーが透過的に暗号化できるように、パラメーターとして渡す必要があります。
 -   バインドされたパラメーターを使用してクエリを実行した場合、PHP ドライバーでは、SQLSRV ドライバーの使用時にユーザーが明示的に SQL 型を指定していない限り、ユーザーに対して自動的に SQL 型が決定されます。
 -   ドライバーが SSN 列と BirthDate 列から取得されたデータを透過的に暗号化解除するので、プログラムで出力される値はすべてプレーンテキストになります。
 
注: 暗号化が決定論的である場合にのみ、クエリで暗号化された列に対する等価比較を実行できます。 詳細については、「[明確な暗号化またはランダム化された暗号化の選択](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)」を参照してください。

SQLSRV:
```
// since SSN is an encrypted column, need to pass the value in the WHERE clause through bind parameter
$query = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN] = ?";
$ssn = "795-73-9838";
$stmt = sqlsrv_prepare($conn, $query, array(&$ssn));
// during sqlsrv_execute, the driver encrypts the ssn value and passes it to the database
sqlsrv_execute($stmt);
// fetch like usual
$row = sqlsrv_fetch_array($stmt);
```

PDO_SQLSRV:
```
// since SSN is an encrypted column, need to pass the value in the WHERE clause through bind parameter
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN] = ?";
$ssn = "795-73-9838";
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $ssn);
// during PDOStatement::execute, the driver encrypts the ssn value and passes it to the database
$stmt->execute();
// fetch like usual
$row = $stmt->fetch();
```

### <a name="ciphertext-data-retrieval-example"></a>暗号化テキスト データの取得の例

Always Encrypted が有効になっていない場合でも、暗号化された列をターゲットとするパラメーターがクエリになければ、クエリでは、暗号化された列からデータを取得できます。

次の例は、SQLSRV および PDO_SQLSRV ドライバーを使用して、暗号化された列から暗号化されたバイナリ データを取得する方法を示しています。 以下の点に注意してください。
 -   接続文字列で Always Encrypted が有効になっていないので、クエリは、SSN と BirthDate の暗号化された値をバイト配列として返します (プログラムによって値が文字列に変換されます)。
 -   Always Encrypted が無効の状態で、暗号化された列からデータを取得するクエリは、暗号化された列をターゲットとするパラメーターがない場合に限り、パラメーターを含むことができます。 次のクエリは、データベースで暗号化されない LastName によってフィルター処理を行います。 クエリが SSN または BirthDate によってフィルター処理を行った場合、クエリは失敗します。
 
SQLSRV:
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName] = ?";
$lastName = "Abel";
$stmt = sqlsrv_prepare($conn, $query, array(&$lastName));
sqlsrv_execute($stmt);
$row = sqlsrv_fetch_array($stmt);
```

PDO_SQLSRV:
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName] = ?";
$lastName = "Abel";
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $lastName);
$stmt->execute();
$row = $stmt->fetch();
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>暗号化された列をクエリする際の一般的な問題を回避する

ここでは、暗号化された列を PHP アプリケーションからクエリする際のエラーの一般的なカテゴリと、その対処方法に関するいくつかのガイドラインを示します。

#### <a name="unsupported-data-type-conversion-errors"></a>サポートされていないデータ型の変換エラー

Always Encrypted では、暗号化されたデータ型に対するいくつかの変換がサポートされています。 サポートされている型の変換の詳細な一覧については、「[Always Encrypted (データベース エンジン)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)」を参照してください。 データ型の変換エラーを回避するには、次の操作を行います。
 -   `sqlsrv_prepare` および `sqlsrv_execute` を指定して SQLSRV ドライバーを使用した場合、列サイズとパラメーターの 10 進桁数と共に、SQL 型が自動的に決定されます。
 -   PDO_SQLSRV ドライバーを使用してクエリを実行した場合、列サイズおよびパラメーターの 10 進桁数と共に、SQL 型も自動的に決定されます
 -   `sqlsrv_query` を指定して SQLSRV ドライバーを使用し、クエリを実行した場合:
  -   パラメーターの SQL 型については、ターゲットとする列の型とまったく同じであるか、または SQL 型から列の型への変換がサポートされている。
  -   `decimal` と `numeric` の SQL Server データ型の列をターゲットとするパラメーターの有効桁数と小数点以下桁数が、ターゲット列に対して構成する有効桁数と小数点と同じである。
  -   ターゲット列を変更するクエリで、`datetime2`、`datetimeoffset`、または `time` の SQL Server データ型の列をターゲットとするパラメーターの有効桁数が、ターゲット列の有効桁数以下である。
 -   パラメーター化クエリ内で、PDO_SQLSRV ステートメント属性 `PDO::SQLSRV_ATTR_DIRECT_QUERY` または `PDO::ATTR_EMULATE_PREPARES` を使用しないでください
 
#### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>暗号化された値の代わりにプレーンテキストを渡すことによるエラー

暗号化された列をターゲットとする値はいずれも、サーバーに送信する前に暗号化する必要があります。 暗号化された列でプレーンテキスト値の挿入、変更、フィルター処理を行おうとすると、エラーになります。 このようなエラーを防ぐには、次のことを確認してください。
 -   Always Encrypted が有効になっている (接続文字列内で、`ColumnEncryption` キーワードが `Enabled` に設定されている)。
 -   バインド パラメーターを使用して、暗号化された列をターゲットとするデータを送信すること。 次の例は、暗号化された列 (SSN) に対して、リテラル/定数によって不正なフィルター処理を行うクエリを示しています。
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

## <a name="controlling-performance-impact-of-always-encrypted"></a>Always Encrypted のパフォーマンスの影響を制御する

Always Encrypted はクライアント側暗号化テクノロジであるため、ほとんどのパフォーマンス オーバーヘッドは、データベースではなくクライアント側で発生します。 暗号化および暗号化解除の操作のコストとは別に、クライアント側のパフォーマンス オーバーヘッドのその他の原因を次に示します。
 -   クエリ パラメーターのメタデータを取得するためのデータベースへの追加のラウンド トリップ。
 -   列マスター キーにアクセスするための列マスター キー ストアの呼び出し。
 
### <a name="round-trips-to-retrieve-metadata-for-query-parameters"></a>クエリ パラメーターのメタデータを取得するためのラウンド トリップ

既定では、接続に対して Always Encrypted が有効になっている場合、ODBC Driver は、各パラメーター化クエリに対して [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) を呼び出し、クエリ ステートメント (パラメーター値を除く) を SQL Server に渡します。 このストアド プロシージャでは、クエリ ステートメントを分析して、パラメーターを暗号化する必要があるかどうかが判断され、必要がある場合は、ドライバーでパラメーターを暗号化できるようにするため、パラメーターごとに暗号化関連の情報が返されます。

PHP ドライバーを使用すると、Always Encrypted が有効化された接続でパラメーターがバインドされている場合、ユーザーは SQL 型を指定しなくても準備済みのステートメントでパラメーターをバインドできるため、PHP ドライバーでは、そのパラメーターに対する [SQLDescribeParam](../../odbc/reference/syntax/sqldescribeparam-function.md) を呼び出して、SQL 型、列サイズ、および 10 進数を取得します。 その後、メタデータを使用して [SQLBindParameter]( ../../odbc/reference/syntax/sqlbindparameter-function.md) が呼び出されます。 `sys.sp_describe_parameter_encryption` が呼び出されたときに、ODBC ドライバーでは既にクライアント側での情報を格納しているため、これらの追加の `SQLDescribeParam` 呼び出しによって、データベースへのラウンド トリップが余計に必要になることはありません。

前述の動作により、次のような高度な透過性が確保されます: 暗号化された列をターゲットとする値がパラメーターでドライバーに渡される限り、クライアント アプリケーション (およびアプリケーション開発者) は、どのクエリが暗号化された列にアクセスするかを認識する必要がありません。

ODBC Driver for SQL Server とは異なり、ステートメント/クエリ レベルでの Always Encrypted の有効化は、PHP ドライバーではまだサポートされていません。 

### <a name="column-encryption-key-caching"></a>列暗号化キーのキャッシュ

列暗号化キー (CEK) を暗号化解除するための列マスター キー ストアの呼び出し回数を減らすために、ドライバーによってプレーンテキスト CEK がメモリにキャッシュされます。 データベース メタデータから暗号化された CEK (ECEK) を受け取った後、ODBC ドライバーでは、まず、キャッシュ内の暗号化されたキー値に対応するプレーンテキスト CEK の検索が試みられます。 ドライバーでは、キャッシュ内で対応するプレーンテキスト CEK が見つからない場合にのみ、CMK を含むキー ストアが呼び出されます。

注: ODBC Driver for SQL Server では、2 時間のタイムアウト後にキャッシュ内のエントリが削除されます。 この動作は、つまり、ECEK が指定されている場合、ドライバーはアプリケーションの有効期間中または 2 時間間隔のうち、どちらか短い方の期間中に 1 回だけキー ストアと交信するということです。

## <a name="working-with-column-master-key-stores"></a>列マスター キー ストアを操作する

データを暗号化または暗号化解除する場合、ターゲット列に対して構成された CEK がドライバーによって取得される必要があります。 CEK は、データベース メタデータ内に暗号化された形式 (ECEK) で格納されます。 各 CEK には、暗号化する際に使用された対応する CMK があります。 [データベース メタデータ](../../t-sql/statements/create-column-master-key-transact-sql.md)に CMK 自体は格納されません。これにはキー ストアの名前と、キー ストアが CMK を検索するために使用できる情報のみが含まれます。

ECEK のプレーンテキスト値を取得するために、ドライバーでは、まず、CEK とそれに対応する CMK の両方に関するメタデータが取得されます。次に、この情報を使用して CMK を含むキー ストアへのアクセスが行われ、ECEK の暗号化を解除するよう要求が出されます。 ドライバーとキー ストアの通信は、キー ストア プロバイダーを使用して行われます。

Microsoft Driver 5.3.0 for PHP for SQL Server では、Windows 証明書ストア プロバイダーと Azure Key Vault のみがサポートされています。 ODBC ドライバーによってサポートされているその他のキーストア プロバイダー (カスタム キーストア プロバイダー) は、まだサポートされていません。

### <a name="using-the-windows-certificate-store-provider"></a>Windows 証明書ストア プロバイダーの使用

Windows 用の ODBC Driver for SQL Server には、`MSSQL_CERTIFICATE_STORE` と呼ばれる Windows 証明書ストア用の組み込みの列マスター キー ストア プロバイダーが含まれています (このプロバイダーは macOS または Linux では使用できません)。このプロバイダーを使用すると、CMK はクライアント コンピューター上にローカルに格納され、ドライバーでそれを使用するためにアプリケーションで追加の構成を行う必要はありません。 ただし、アプリケーションには、ストア内の証明書とその秘密キーへのアクセス権が必要です。 詳細については、 [列マスター キーの作成と格納 (Always Encrypted)](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md) を参照してください。

### <a name="using-azure-key-vault"></a>Azure Key Vault の使用

Azure Key Vault では、Azure を使用して暗号化キー、パスワード、およびその他のシークレットを格納する方法が提供されており、Always Encrypted 用のキーを格納するために使用できます。 ODBC Driver for SQL Server (バージョン 17 以降) には、Azure Key Vault 向けの組み込みのマスター キー ストア プロバイダーが用意されています。 次の接続オプション `KeyStoreAuthentication`、`KeyStorePrincipalId`、および `KeyStoreSecret` では、Azure Key Vault の構成を処理します。 
 -   `KeyStoreAuthentication` には、使用できる 2 つの文字列値 `KeyVaultPassword` および `KeyVaultClientSecret` のうち 1 つを指定できます。 これらの値では、残り 2 つのキーワードによって使用される認証資格情報の種類が制御されます。
 -   `KeyStorePrincipalId` には、Azure Key Vault へのアクセスをシークするアカウント用の識別子を表す文字列を指定します。 
     -   `KeyStoreAuthentication` が `KeyVaultPassword` に設定された場合、`KeyStorePrincipalId` には Azure ActiveDirectory ユーザーの名前が指定される必要があります。
     -   `KeyStoreAuthentication` が `KeyVaultClientSecret` に設定された場合、`KeyStorePrincipalId` にはアプリケーション クライアント ID が指定される必要があります。
 -   `KeyStoreSecret` には、資格情報のシークレットを表す文字列を指定します。 
     -   `KeyStoreAuthentication` が `KeyVaultPassword` に設定された場合、`KeyStoreSecret` にはユーザーのパスワードが指定される必要があります。 
     -   `KeyStoreAuthentication` が `KeyVaultClientSecret` に設定された場合、`KeyStoreSecret` はアプリケーション クライアント ID に関連付けられているアプリケーション シークレットを指定する必要があります。

3 つのオプションはすべて、Azure Key Vault を使用するための接続文字列の中で指定される必要があります。 さらに、`ColumnEncryption` は `Enabled` に設定される必要があります。 `ColumnEncryption` が `Disabled` に設定されているのに、Azure Key Vault のオプションが指定されている場合、スクリプトはエラーにならずに処理されますが、暗号化は実行されません。

次の例では、Azure Key Vault を使用して SQL Server に接続する方法を示しています。

SQLSRV:

Azure Active Directory アカウントを使用する場合:
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled", "KeyStoreAuthentication"=>"KeyVaultPassword", "KeyStorePrincipalId"=>$AADUsername, "KeyStoreSecret"=>$AADPassword);
$conn = sqlsrv_connect($server, $connectionInfo);
```
Azure アプリケーションのクライアント ID とシークレットを使用する場合:
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled", "KeyStoreAuthentication"=>"KeyVaultClientSecret", "KeyStorePrincipalId"=>$applicationClientID, "KeyStoreSecret"=>$applicationClientSecret);
$conn = sqlsrv_connect($server, $connectionInfo);
```

PDO_SQLSRV:Azure Active Directory アカウントを使用する場合:
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled; KeyStoreAuthentication = KeyVaultPassword; KeyStorePrincipalId = $AADUsername; KeyStoreSecret = $AADPassword;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```
Azure アプリケーションのクライアント ID とシークレットを使用する場合:
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled; KeyStoreAuthentication = KeyVaultClientSecret; KeyStorePrincipalId = $applicationClientID; KeyStoreSecret = $applicationClientSecret;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```

## <a name="limitations-of-the-php-drivers-when-using-always-encrypted"></a>Always Encrypted を使用するときの PHP ドライバーの制限事項

SQLSRV および PDO_SQLSRV:
 -   Linux/macOS では、Windows 証明書ストア プロバイダーはサポートされません
 -   パラメーターの暗号化の強制適用
 -   ステートメント レベルでの Always Encrypted の有効化 
 -   Linux および macOS 上で Always Encrypted 機能と非 UTF8 ロケールを使用する ("en_US.ISO-8859-1" など) 場合、コード ページ 1252 がシステム上にインストールされていない限り、暗号化された char(n) 列への null データまたは空の文字列の挿入は機能しないことがあります
 
SQLSRV のみ:
 -   SQL 型を指定せずに、パラメーターのバインドに `sqlsrv_query` を使用する
 -   SQL ステートメントのバッチ内で、パラメーターのバインドに `sqlsrv_prepare` を使用する  
 
PDO_SQLSRV のみ:
 -   パラメーター化クエリ内で `PDO::SQLSRV_ATTR_DIRECT_QUERY` ステートメント属性が指定される
 -   パラメーター化クエリ内で `PDO::ATTR_EMULATE_PREPARE` ステートメント属性が指定される
 -   SQL ステートメントのバッチ内でパラメーターをバインドする
 
また、PHP ドライバーでは、ODBC Driver for SQL Server およびデータベースによって課される制限事項も引き継ぎます。 [Always Encrypted を使用する場合の ODBC ドライバーの制限事項](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)に関するページと [Always Encrypted 機能の詳細](../../relational-databases/security/encryption/always-encrypted-database-engine.md#feature-details)に関するページを参照してください。  
  
## <a name="see-also"></a>参照  
[プログラミング ガイド](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)  

[PDO_SQLSRV ドライバー API リファレンス](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
