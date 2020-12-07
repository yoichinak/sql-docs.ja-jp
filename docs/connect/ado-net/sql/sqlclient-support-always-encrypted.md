---
title: SqlClient で Always Encrypted を使用する
description: データの安全性を維持するために、Microsoft.Data.SqlClient と Always Encrypted を使用してアプリケーションを開発する方法について説明します。
ms.date: 11/16/2020
ms.assetid: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: cheenamalhotra
ms.author: v-chmalh
ms.reviewer: v-kaywon
ms.openlocfilehash: bb971ed9fdc24491babf1ce9fe777210778037de
ms.sourcegitcommit: 4c3949f620d09529658a2172d00bfe37aeb1a387
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2020
ms.locfileid: "96123906"
---
# <a name="using-always-encrypted-with-the-microsoft-net-data-provider-for-sql-server"></a>Always Encrypted と Microsoft .NET Data Provider for SQL Server を使用する

[!INCLUDE[appliesto-netfx-netcore-xxxx-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

この記事では、[Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) または [セキュリティで保護されたエンクレーブが設定された Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-enclaves.md) と [**Microsoft .NET Data Provider for SQL Server**](../microsoft-ado-net-sql-server.md) を使用して、.NET アプリケーションを開発する方法について説明します。

Always Encrypted を使用すると、クライアント アプリケーションは SQL Server または Azure SQL データベースにデータまたは暗号化キーを開示することなく、機密データを暗号化することができます。 **Microsoft .NET Data Provider for SQL Server** など、Always Encrypted が有効になっているドライバーは、クライアント アプリケーション内の機密データを透過的に暗号化および暗号化解除することで、これを実現します。 ドライバーは、どのクエリ パラメーターが機密データベース列 (Always Encrypted を使用して保護される) に対応するかを自動的に決定し、SQL Server または Azure SQL データベースにデータを渡す前にこれらのパラメーターの値を暗号化します。 同様に、ドライバーは、クエリ結果内の暗号化されたデータベース列から取得されたデータを透過的に暗号化解除します。 詳しくは、「[Always Encrypted を使用したアプリケーションの開発](../../../relational-databases/security/encryption/always-encrypted-client-development.md)」および「[セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用してアプリケーションを開発する](../../../relational-databases/security/encryption/always-encrypted-enclaves-client-development.md)」をご覧ください。

## <a name="prerequisites"></a>前提条件

- データベースで Always Encrypted を構成します。 この処理には、Always Encrypted キーのプロビジョニング、および選択したデータベース列の暗号化の設定が含まれます。 Always Encrypted が構成されたデータベースがまだない場合は、「[Always Encrypted の作業の開始](../../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)」の手順に従います。
- 必要な .NET プラットフォームが開発用マシンにインストールされていることを確認します。 [Microsoft.Data.SqlClient](../microsoft-ado-net-sql-server.md) では、.NET Framework と .NET Core の両方で Always Encrypted 機能がサポートされています。 開発環境内で .NET プラットフォームのターゲット バージョンとして、[.NET Framework 4.6](/dotnet/framework/) 以降または [.NET Core 2.1](/dotnet/core/) 以降が構成されていることを確認します。 Microsoft.Data.SqlClient バージョン 2.1.0 以降では、Always Encrypted の機能は [.NET Standard 2.0](/dotnet/standard/net-standard) でもサポートされています。 セキュリティで保護されたエンクレーブを使用する Always Encrypted を使用するには、[.NET Standard 2.1](/dotnet/standard/net-standard) が必要です。 Visual Studio を使用している場合は、「[フレームワーク対象設定機能の概要](/visualstudio/ide/visual-studio-multi-targeting-overview)」を参照してください。

次の表は、**Microsoft.Data.SqlClient** で Always Encrypted を使用するために必要な .NET プラットフォームをまとめたものです。

| Always Encrypted のサポート | セキュリティで保護されたエンクレーブを使用する Always Encrypted のサポート  | [対象とする Framework] | Microsoft.Data.SqlClient のバージョン | オペレーティング システム |
|:--|:--|:--|:--:|:--:|
| はい | はい | .NET Framework 4.6+ | 1.1.0 以降 | Windows |
| はい | はい | .NET Core 2.1 以降 | 2.1.0 以降<sup>1</sup> | Windows、Linux、macOS |
| はい | いいえ | .NET Standard 2.0 | 2.1.0 以降 | Windows、Linux、macOS |
| はい | はい | .NET Standard 2.1 以降 | 2.1.0 以降 | Windows、Linux、macOS |

> [!NOTE]
> <sup>1</sup> バージョン 2.1.0 より前の Microsoft.Data.SqlClient では、Always Encrypted は Windows でのみサポートされています。 

## <a name="enabling-always-encrypted-for-application-queries"></a>アプリケーション クエリで Always Encrypted を有効にする

パラメーターを暗号化し、暗号化された列を対象にクエリ結果の暗号化を解除できるようにする最も簡単な方法は、`Column Encryption Setting` 接続文字列キーワードの値を **enabled** に設定することです。

Always Encrypted を有効にする接続文字列を使用する例を次に示します。

```cs
string connectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true; Column Encryption Setting=enabled";
SqlConnection connection = new SqlConnection(connectionString);
```

SqlConnectionStringBuilder.ColumnEncryptionSetting プロパティを使用した同等のコード スニペットの例を次に示します。

```cs
SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
builder.DataSource = "server63";
builder.InitialCatalog = "Clinic";
builder.IntegratedSecurity = true;
builder.ColumnEncryptionSetting = SqlConnectionColumnEncryptionSetting.Enabled;
SqlConnection connection = new SqlConnection(builder.ConnectionString);
connection.Open();
```

Always Encrypted は、個々のクエリに対しても有効にすることができます。 以下の「**Always Encrypted のパフォーマンスの影響を制御する**」セクションを参照してください。
暗号化または暗号化解除を正常に行うには、Always Encrypted を有効にするだけでは不十分です。 次のことを確認する必要もあります。

- アプリケーションが、データベース内の Always Encrypted キーに関するメタデータへのアクセスに必要な *VIEW ANY COLUMN MASTER KEY DEFINITION* および *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* データベース権限を持っている。 詳細については、[Always Encrypted (データベース エンジン) に関するページの「データベース権限」セクション](../../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)を参照してください。
- アプリケーションが、列暗号化キーを保護する列マスター キーにアクセスでき、クエリされたデータベース列を暗号化する。

## <a name="enabling-always-encrypted-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted を有効にする

Microsoft.Data.SqlClient バージョン 1.1.0 以降のドライバーでは、[セキュリティで保護されたエンクレーブが設定された Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-enclaves.md) がサポートされています。

[!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] 以降に接続するときにエンクレーブを使用できるようにするには、エンクレーブの計算とエンクレーブの構成証明を有効にするように、アプリケーションを構成する必要があります。

エンクレーブの計算とエンクレーブの構成証明におけるクライアント ドライバーの役割に関する一般的な情報については、「[セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用してアプリケーションを開発する](../../../relational-databases/security/encryption/always-encrypted-enclaves-client-development.md)」をご覧ください。

アプリケーションを構成するには:

1. [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] インスタンスがエンクレーブの種類を使用して構成されていることを確認します (「[Always Encrypted サーバー構成オプションのエンクレーブの種類を構成する](../../../database-engine/configure-windows/configure-column-encryption-enclave-type.md)」を参照してください)。 [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] では、構成証明に対して VBS エンクレーブの種類と[ホスト ガーディアン サービス](/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-setting-up-the-host-guardian-service-hgs)がサポートされています。
2. 構成証明エンドポイントへの接続文字列で `Enclave Attestation URL` キーワードを設定することにより、アプリケーションからデータベースへの接続に対してエンクレーブの計算を有効にします。 キーワードの値は、お使いの環境で構成されている HGS サーバーの構成証明エンドポイントに設定する必要があります。
3. 接続文字列で `Attestation Protocol` キーワードを設定して、使用する構成証明プロトコルを指定します。 このキーワードの値は、"HGS" に設定する必要があります。

詳しいチュートリアルについては、「[チュートリアル: セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して .NET アプリケーションを開発する](tutorial-always-encrypted-enclaves-develop-net-apps.md)」を参照してください。


## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>暗号化された列のデータを取得および変更する

アプリケーション クエリに対して Always Encrypted を有効にすると、標準の SqlClient API シリーズ (「[ADO.NET でのデータの取得および変更](/dotnet/framework/data/adonet/retrieving-and-modifying-data)」を参照) または [**Microsoft .NET Data Provider for SQL Server**](index.md) API シリーズ ([Microsoft.Data.SqlClient 名前空間](/dotnet/api/microsoft.data.sqlclient)で定義) を使用して、暗号化されたデータベース列のデータを取得または変更することができます。 アプリケーションに必要なデータベース アクセス許可があり、列マスター キーにアクセスできるなら、**Microsoft .NET Data Provider for SQL Server** によって、暗号化された列をターゲットとするすべてのクエリ パラメーターが暗号化され、暗号化された列から取得されたデータが解読されて、データベース スキーマで列に対して設定された SQL Server データ型に対応する .NET 型のプレーンテキスト値が返されます。
Always Encrypted が有効でない場合、暗号化された列をターゲットとするパラメーターを含むクエリは失敗します。 暗号化された列をターゲットとするパラメーターがクエリにない場合、クエリでは、暗号化された列からデータを取得できます。 ただし、**Microsoft .NET Data Provider for SQL Server** では、暗号化された列から取得された値の暗号化解除は試みられず、アプリケーションは、暗号化されたバイナリ データを (バイト配列として) 受け取ります。

次の表は、Always Encrypted が有効かどうかに応じたクエリの動作をまとめたものです。

|クエリの特性 | Always Encrypted が有効になっており、アプリケーションがキーやキー メタデータにアクセスできる|Always Encrypted が有効になっており、アプリケーションがキーやキー メタデータにアクセスできない | Always Encrypted が無効になっている|
|:---|:---|:---|:---|
| 暗号化された列をターゲットとするパラメーターを含むクエリ。 | パラメーター値は透過的に暗号化されます。 | エラー | エラー |
| 暗号化された列をターゲットとするパラメーターを含まず、暗号化された列からデータを取得するクエリ。 | 暗号化された列の結果は透過的に暗号化解除されます。 アプリケーションは、暗号化された列に対して構成された SQL Server 型に対応する、.NET データ型のプレーンテキスト値を受け取ります。 | エラー | 暗号化された列の結果は暗号化解除されません。 アプリケーションは、暗号化された値をバイト配列 (byte[]) として受け取ります。 |

次の例は、暗号化された列のデータを取得および変更する方法を示しています。 この例では、下のスキーマを含むターゲット テーブルを想定しています。 `SSN` および `BirthDate` 列は暗号化されています。

```sql
CREATE TABLE [dbo].[Patients]([PatientId] [int] IDENTITY(1,1),
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

### <a name="inserting-data-example"></a>データの挿入の例

この例では、Patients テーブルに列を挿入します。 次のことを考慮してください。

- このサンプル コードの暗号化に固有のものは何もありません。 **Microsoft .NET Data Provider for SQL Server** は、暗号化された列をターゲットとする `paramSSN` および `paramBirthdate` パラメーターを自動的に検出し、暗号化します。 これにより、アプリケーションに対して暗号化が透過的に実行されます。
- 暗号化された列を含め、データベース列に挿入された値は、 [SqlParameter](/dotnet/api/microsoft.data.sqlclient.sqlparameter) オブジェクトとして渡されます。 **SqlParameter** の使用は、暗号化されていない列に値を送信する場合は省略可能ですが (ただし、SQL インジェクションを防ぐのに役立つので、強くお勧めします)、暗号化された列をターゲットとする値に対しては必須です。 `SSN` または `BirthDate` 列に挿入された値が、クエリ ステートメントに埋め込まれたリテラルとして渡された場合、クエリは失敗します。これは、**Microsoft .NET Data Provider for SQL Server** で、暗号化されたターゲットの列の値を決定できず、値を解読できないためです。 その結果、サーバーはこれらの値を、暗号化された列と互換性がないと見なして拒否します。
- `SSN` 列をターゲットとするパラメーターのデータ型は、ANSI (非 Unicode) 文字列に設定され、char または varchar の SQL Server データ型にマップされます。 パラメーターの型が Unicode 文字列 (String) に設定された場合、これらは nchar/nvarchar にマップされ、クエリは失敗します。これは、暗号化された nchar/nvarchar 値から暗号化された char/varchar 値への変換が、Always Encrypted でサポートされていないためです。 データ型のマッピングについては、「 [SQL Server データ型のマッピング](/dotnet/framework/data/adonet/sql-server-data-type-mappings) 」を参照してください。
- `BirthDate` 列に挿入されるパラメーターのデータ型は、[SqlParameter.DbType プロパティ](/dotnet/api/microsoft.data.sqlclient.sqlparameter.dbtype)の使用時に適用される、.NET 型から SQL Server データ型への暗黙的なマッピングに依存するのではなく、[SqlParameter.SqlDbType プロパティ](/dotnet/api/microsoft.data.sqlclient.sqlparameter.sqldbtype)を使用してターゲットの SQL Server データ型に明示的に設定されます。 既定では、[DateTime 構造体](/dotnet/api/system.datetime)は SQL Server datetime データ型にマップされます。 `BirthDate` 列のデータ型は date であり、暗号化された datetime 値から暗号化された date 値の変換は Always Encrypted でサポートされていないので、既定のマッピングを使用するとエラーになります。

```cs
string connectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true; Column Encryption Setting=enabled";

using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
using (SqlCommand cmd = connection.CreateCommand())
{
    connection.Open();
    cmd.CommandText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

    SqlParameter paramSSN = cmd.CreateParameter();
    paramSSN.ParameterName = @"@SSN";
    paramSSN.DbType = DbType.AnsiStringFixedLength;
    paramSSN.Direction = ParameterDirection.Input;
    paramSSN.Value = "795-73-9838";
    paramSSN.Size = 11;
    cmd.Parameters.Add(paramSSN);

    SqlParameter paramFirstName = cmd.CreateParameter();
    paramFirstName.ParameterName = @"@FirstName";
    paramFirstName.DbType = DbType.String;
    paramFirstName.Direction = ParameterDirection.Input;
    paramFirstName.Value = "Catherine";
    paramFirstName.Size = 50;
    cmd.Parameters.Add(paramFirstName);

    SqlParameter paramLastName = cmd.CreateParameter();
    paramLastName.ParameterName = @"@LastName";
    paramLastName.DbType = DbType.String;
    paramLastName.Direction = ParameterDirection.Input;
    paramLastName.Value = "Abel";
    paramLastName.Size = 50;
    cmd.Parameters.Add(paramLastName);

    SqlParameter paramBirthdate = cmd.CreateParameter();
    paramBirthdate.ParameterName = @"@BirthDate";
    paramBirthdate.SqlDbType = SqlDbType.Date;
    paramBirthdate.Direction = ParameterDirection.Input;
    paramBirthdate.Value = new DateTime(1996, 09, 10);
    cmd.Parameters.Add(paramBirthdate);

    cmd.ExecuteNonQuery();
}
```

### <a name="retrieving-plaintext-data-example"></a>プレーンテキスト データの取得の例

次の例は、暗号化された値に基づいてデータをフィルター処理し、暗号化された列からプレーンテキスト データを取得する方法を示しています。 次のことを考慮してください。

```cs
string connectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true; Column Encryption Setting=enabled";
using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
using (SqlCommand cmd = connection.CreateCommand())
{
    connection.Open();
    cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN=@SSN";

    SqlParameter paramSSN = cmd.CreateParameter();
    paramSSN.ParameterName = @"@SSN";
    paramSSN.DbType = DbType.AnsiStringFixedLength;
    paramSSN.Direction = ParameterDirection.Input;
    paramSSN.Value = "795-73-9838";
    paramSSN.Size = 11;
    cmd.Parameters.Add(paramSSN);
    using (SqlDataReader reader = cmd.ExecuteReader())
    {
        if (reader.HasRows)
        {
            while (reader.Read())
            {
                Console.WriteLine(@"{0}, {1}, {2}, {3}", reader[0], reader[1], reader[2], ((DateTime)reader[3]).ToShortDateString());
            }
        }
    }
}
```

> [!NOTE]
> - `SSN` 列でのフィルター処理のために WHERE 句で使用される値は、**Microsoft .NET Data Provider for SQL Server** によってデータベースに送信される前に透過的に暗号化できるよう、SqlParameter を使用して渡す必要があります。
>
> - `SSN` と `BirthDate` 列から取得されたデータは **Microsoft .NET Data Provider for SQL Server** によって透過的に解読されるので、プログラムで出力される値はすべてプレーンテキストになります。
>
> - 決定論的暗号化を使用して列が暗号化される場合、クエリは列に対して等価比較を実行できます。 詳しくは、「[明確な暗号化またはランダム化された暗号化の選択](../../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)」をご覧ください。

### <a name="retrieving-encrypted-data-example"></a>暗号化されたデータの取得の例

Always Encrypted が有効になっていない場合でも、暗号化された列をターゲットとするパラメーターがクエリになければ、クエリでは、暗号化された列からデータを取得できます。

次の例は、暗号化された列から暗号化されたバイナリ データを取得する方法を示しています。 

```cs
string connectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true";

using (SqlConnection connection = new SqlConnection(connectionString))
using (SqlCommand cmd = connection.CreateCommand())
{
    connection.Open();
    cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName]=@LastName";

    SqlParameter paramLastName = cmd.CreateParameter();
    paramLastName.ParameterName = @"@LastName";
    paramLastName.DbType = DbType.String;
    paramLastName.Direction = ParameterDirection.Input;
    paramLastName.Value = "Abel";
    paramLastName.Size = 50;
    cmd.Parameters.Add(paramLastName);
    using (SqlDataReader reader = cmd.ExecuteReader())
    {
        if (reader.HasRows)
        {
            while (reader.Read())
            {
                Console.WriteLine(@"{0}, {1}, {2}, {3}", BitConverter.ToString((byte[])reader[0]), reader[1], reader[2], BitConverter.ToString((byte[])reader[3]));
            }
        }
    }
}
```

> [!NOTE]
> - 接続文字列で Always Encrypted が有効になっていないので、クエリからは、`SSN` と `BirthDate` の暗号化された値がバイト配列として返されます (プログラムによって値が文字列に変換されます)。
>
> - Always Encrypted が無効の状態で、暗号化された列からデータを取得するクエリは、暗号化された列をターゲットとするパラメーターがない場合に限り、パラメーターを含むことができます。 上記のクエリでは、データベースで暗号化されていない LastName によるフィルター処理が行われます。 クエリで `SSN` または `BirthDate` によるフィルター処理が行われた場合、クエリは失敗します。

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>暗号化された列をクエリする際の一般的な問題を回避する

ここでは、暗号化された列を .NET アプリケーションからクエリする際のエラーの一般的なカテゴリと、その対処方法に関するいくつかのガイドラインを示します。

### <a name="unsupported-data-type-conversion-errors"></a>サポートされていないデータ型の変換エラー

Always Encrypted では、暗号化されたデータ型に対するいくつかの変換がサポートされています。 サポートされている型の変換の詳細な一覧については、「[Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)」をご覧ください。 データ型の変換エラーを回避するには、次の操作を行います。

- パラメーターの SQL Server データ型が、ターゲット列の型とまったく同じになるか、またはパラメーターの SQL Server データ型から列のターゲット型への変換がサポートされるように、暗号化された列をターゲットとするようにパラメーターの型を設定する。 SqlParameter.SqlDbType プロパティを使用して、.NET データ型から特定の SQL Server データ型への望ましいマッピングを強制できます。
- 10 進数と数値の SQL Server データ型の列をターゲットとするパラメーターの有効桁数と小数点以下桁数が、ターゲット列に対して構成された有効桁数と小数点以下桁数と同じであることを確認する。  
- ターゲット列の値を変更するクエリで、datetime2、datetimeoffset、または time の SQL Server データ型の列をターゲットとするパラメーターの有効桁数が、ターゲット列の有効桁数以下であることを確認する。  

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>暗号化された値の代わりにプレーンテキストを渡すことによるエラー

暗号化された列をターゲットとするすべての値は、アプリケーションの内部で暗号化される必要があります。 暗号化された列でプレーンテキスト値を挿入/変更したり、この値によってフィルター処理を行おうとすると、次のようなエラーになります。

```log
Microsoft.Data.SqlClient.SqlException (0x80131904): Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', column_encryption_key_database_name = 'Clinic') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

このようなエラーを防ぐには、次のことを確認してください。

- Always Encrypted が、暗号化された列をターゲットとするアプリケーション クエリに対して有効になっている (接続文字列で、または特定のクエリの [SqlCommand](/dotnet/api/microsoft.data.sqlclient.sqlcommand) オブジェクトで)。
- SqlParameter を使用して、暗号化された列をターゲットとするデータを送信すること。 次の例は、SqlParameter オブジェクト内のリテラルを渡す代わりに、暗号化された列 (SSN) でリテラルまたは定数によって不適切なフィルター処理を行うクエリを示しています。

```cs
using (SqlCommand cmd = connection.CreateCommand())
{
    cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN = '795-73-9838'";
    cmd.ExecuteNonQuery();
}
```

## <a name="working-with-column-master-key-stores"></a>列マスター キー ストアを操作する

パラメーター値を暗号化したり、クエリ結果内のデータを暗号化解除したりするには、**Microsoft .NET Data Provider for SQL Server** では、ターゲット列に対して構成された列暗号化キーを取得する必要があります。 列暗号化キーは、データベースのメタデータに暗号化された形式で格納されています。 各列暗号化キーには、列暗号化キーの暗号化に使用された対応する列マスター キーが含まれます。 データベースのメタデータには、列マスター キーは格納されず、特定の列マスター キーとキー ストア内のキーの場所を含むキー ストアに関する情報のみが含まれます。

列暗号化キーのプレーンテキスト値を取得するため、**Microsoft .NET Data Provider for SQL Server** により、最初に、列暗号化キーとそれに対応する列マスター キーの両方に関するメタデータが取得されます。 その後、メタデータ内の情報を使用して、列マスター キーが格納されているキー ストアへのアクセスが行われて、暗号化された列暗号化キーが解読されます。 **Microsoft .NET Data Provider for SQL Server** は、[SqlColumnEncryptionKeyStoreProvider クラス](/dotnet/api/microsoft.data.sqlclient.sqlcolumnencryptionkeystoreprovider)から派生したクラスのインスタンスである列マスター キー ストア プロバイダーを使用して、キー ストアと通信します。

列暗号化キーを取得するプロセスは次のとおりです。

1. クエリで Always Encrypted が有効になっている場合、**Microsoft .NET Data Provider for SQL Server** は透過的に **sys.sp_describe_parameter_encryption** を呼び出し、暗号化された列をターゲットとするパラメーターの暗号化メタデータを取得します (クエリにパラメーターがある場合)。 クエリ結果に含まれる暗号化されたデータの場合、SQL Server は自動的に暗号化メタデータをアタッチします。 列マスター キーに関する情報には、以下のものが含まれます。
    - 列マスター キーを含むキー ストアをカプセル化する、キー ストア プロバイダーの名前。
    - キー ストア内の列マスター キーの場所を指定するキー パス。

    列暗号化キーに関する情報には、以下のものが含まれます。

    - 列暗号化キーの暗号化された値。
    - 列暗号化キーの暗号化に使用されたアルゴリズムの名前。
2. **Microsoft .NET Data Provider for SQL Server** により、列マスター キー ストア プロバイダーの名前を使用して、内部データ構造でプロバイダー オブジェクト (SqlColumnEncryptionKeyStoreProvider クラスから派生したクラスのインスタンス) が検索されます。
3. 列暗号化キーを暗号化解除するために、**Microsoft .NET Data Provider for SQL Server** は `SqlColumnEncryptionKeyStoreProvider.DecryptColumnEncryptionKey()` メソッドを呼び出します。その場合、暗号化された列暗号化キーの生成に使用される、列マスター キー パス、列暗号化キーの暗号化された値、および暗号化アルゴリズムの名前を渡します。

### <a name="using-built-in-column-master-key-store-providers"></a>組み込み列マスター キー ストア プロバイダーを使用する

**Microsoft .NET Data Provider for SQL Server** には、次の組み込み列マスター キー ストア プロバイダーが付属しており、これらは特定のプロバイダー名 (プロバイダーの検索に使用) で事前に登録されています。 これらの組み込みキー ストア プロバイダーは、Windows でのみサポートされています。

| クラス | 説明 | プロバイダー (検索) 名 | プラットフォーム |
|:---|:---|:---|:---|
|[SqlColumnEncryptionCertificateStoreProvider クラス](/dotnet/api/microsoft.data.sqlclient.sqlcolumnencryptioncertificatestoreprovider) | Windows 証明書ストアのプロバイダー。 | MSSQL_CERTIFICATE_STORE | Windows |
|[SqlColumnEncryptionCngProvider クラス](/dotnet/api/microsoft.data.sqlclient.sqlcolumnencryptioncngprovider) | [Microsoft Cryptography API:Next Generation (CNG) API](/windows/win32/seccng/cng-portal) をサポートするキー ストアのプロバイダー。 通常、このタイプのストアは、デジタル キーを保護および管理し、暗号化処理を提供する物理デバイスである、ハードウェア セキュリティ モジュールです。 | MSSQL_CNG_STORE | Windows |
| [SqlColumnEncryptionCspProvider クラス](/dotnet/api/microsoft.data.sqlclient.sqlcolumnencryptioncspprovider) | [Microsoft Cryptography API (CAPI)](/windows/win32/seccrypto/cryptographic-service-providers)をサポートするキー ストアのプロバイダー。 通常、このタイプのストアは、デジタル キーを保護および管理し、暗号化処理を提供する物理デバイスである、ハードウェア セキュリティ モジュールです。 | MSSQL_CSP_PROVIDER | Windows |

これらのプロバイダーを使用するために、アプリケーション コードを変更する必要はありませんが、次のことに注意してください。

- ユーザー (またはデータベース管理者) は、列マスター キーのメタデータで構成されているプロバイダー名が正しいこと、および列マスター キー パスが、特定のプロバイダーに対して有効なキー パス形式に準拠していることを確認する必要があります。 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) ステートメントを発行した際に有効なプロバイダー名とキー パスを自動的に生成する、SQL Server Management Studio などのツールを使用してキーを構成することをお勧めします。 詳細については、「 [SQL Server Management Studio を使用した Always Encrypted の構成](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md) 」および「 [PowerShell を使用した Always Encrypted の構成](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)」を参照してください。
- アプリケーションがキー ストア内のキーにアクセスできることを確認します。 これには、キーストアに応じてキーまたはキー ストアへのアクセスをアプリケーションに許可したり、その他のキー ストア固有の構成手順を実行するプロセスが含まれる場合があります。 たとえば、CNG または CAPI (ハードウェア セキュリティ モジュールなど) を実装するキー ストアにアクセスするには、ストアに対して CNG または CAPI を実装するライブラリがアプリケーション コンピューターにインストールされていることを確認する必要があります。 詳しくは、「[Always Encrypted の列マスター キーを作成して保存する](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)」をご覧ください。

### <a name="using-the-azure-key-vault-provider"></a>Azure Key Vault プロバイダーを使用する

Azure Key Vault は、特にアプリケーションが Azure でホストされている場合、Always Encrypted の列マスター キーの格納と管理に便利なオプションです。 **Microsoft .NET Data Provider for SQL Server** には、Azure Key Vault 用の組み込み列マスター キー ストア プロバイダーは含まれませんが、アプリケーションと容易に統合できる NuGet パッケージ ([Microsoft.Data.SqLClient.AlwaysEncrypted.AzureKeyVaultProvider](https://www.nuget.org/packages/Microsoft.Data.SqlClient.AlwaysEncrypted.AzureKeyVaultProvider)) としてこれを利用できます。 詳細については、「 [Always Encrypted - Protect sensitive data in SQL Database with data encryption and store your encryption keys in the Azure Key Vault (Always Encrypted - データ暗号化によって SQL データベースの機密データを保護し、Azure Key Vault に暗号化キーを格納する)](/azure/azure-sql/database/always-encrypted-azure-key-vault-configure)」を参照してください。

| クラス | 説明 | プロバイダー (検索) 名 | プラットフォーム |
|:---|:---|:---|:---|
|[SqlColumnEncryptionAzureKeyVaultProvider クラス](/dotnet/api/microsoft.data.sqlclient.alwaysencrypted.azurekeyvaultprovider.sqlcolumnencryptionazurekeyvaultprovider) | Azure Key Vault 用のプロバイダー。 | AZURE_KEY_VAULT | Windows、Linux、macOS |

Azure Key Vault で暗号化と暗号化解除を実行する例については、[Azure Key Vault と Always Encrypted の連携](azure-key-vault-example.md)に関するページおよび [Azure Key Vault と、セキュリティで保護されたエンクレーブが設定された Always Encrypted の連携](azure-key-vault-enclave-example.md)に関するページを参照してください。

### <a name="implementing-a-custom-column-master-key-store-provider"></a>カスタム列マスター キー ストア プロバイダーを実装する

既存のプロバイダーでサポートされていないキー ストアに列マスター キーを格納する場合は、[SqlColumnEncryptionKeyStoreProvider クラス](/dotnet/api/microsoft.data.sqlclient.sqlcolumnencryptionkeystoreprovider)を拡張し、[SqlConnection.RegisterColumnEncryptionKeyStoreProviders](/dotnet/api/microsoft.data.sqlclient.sqlconnection.registercolumnencryptionkeystoreproviders) メソッドを使用してプロバイダーを登録することにより、カスタム プロバイダーを実装できます。

```cs
public class MyCustomKeyStoreProvider : SqlColumnEncryptionKeyStoreProvider
{
    public const string ProviderName = "MY_CUSTOM_STORE";

    public override byte[] EncryptColumnEncryptionKey(string masterKeyPath, string encryptionAlgorithm, byte[] columnEncryptionKey)
    {
        // Logic for encrypting a column encrypted key.
    }
    public override byte[] DecryptColumnEncryptionKey(string masterKeyPath, string encryptionAlgorithm, byte[] EncryptedColumnEncryptionKey)
    {
        // Logic for decrypting a column encrypted key.
    }
}  
class Program
{
    static void Main(string[] args)
    {
        Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
            new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();
        providers.Add(MyCustomKeyStoreProvider.ProviderName, new MyCustomKeyStoreProvider());
        SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
        // ...
    }
}
```

### <a name="using-column-master-key-store-providers-for-programmatic-key-provisioning"></a>プログラムによるキーのプロビジョニングに列マスター キー ストア プロバイダーを使用する

**Microsoft .NET Data Provider for SQL Server** は、暗号化された列にアクセスする際に、列暗号化キーを暗号化解除するための適切な列マスター キー ストア プロバイダーを透過的に検索して呼び出します。 一般的に、通常のアプリケーション コードは列マスター キー ストア プロバイダーを直接呼び出しません。 ただし、プロバイダーを明示的にインスタンス化して呼び出し、プログラムを使用して Always Encrypted キーをプロビジョニングおよび管理することができます。これにより、(たとえば、一部の列マスター キーの回転として) 暗号化された列暗号化キーを生成したり、列暗号化キーを暗号化解除することができます。 詳しくは、「[Always Encrypted のキー管理の概要](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)」をご覧ください。
カスタム キー ストア プロバイダーを使用する場合に限り、独自のキー管理ツールの実装が必要になることがあります。 組み込みのプロバイダーが存在するキー ストア、または Azure Key Vault に格納されたキーを使用する場合は、SQL Server Management Studio や PowerShell などの既存のツールを使用してキーを管理およびプロビジョニングすることができます。
次の例は、列暗号化キーを生成し、[SqlColumnEncryptionCertificateStoreProvider クラス](/dotnet/api/microsoft.data.sqlclient.sqlcolumnencryptioncertificatestoreprovider)を使用して証明書でキーを暗号化する方法を示しています。

```cs
using System.Security.Cryptography;
static void Main(string[] args)
{
    byte[] EncryptedColumnEncryptionKey = GetEncryptedColumnEncryptonKey();
    Console.WriteLine("0x" + BitConverter.ToString(EncryptedColumnEncryptionKey).Replace("-", ""));
    Console.ReadKey();
}

static byte[]  GetEncryptedColumnEncryptonKey()
{
    int cekLength = 32;
    String certificateStoreLocation = "CurrentUser";
    String certificateThumbprint = "698C7F8E21B2158E9AED4978ADB147CF66574180";
    // Generate the plaintext column encryption key.
    byte[] columnEncryptionKey = new byte[cekLength];
    RNGCryptoServiceProvider rngCsp = new RNGCryptoServiceProvider();
    rngCsp.GetBytes(columnEncryptionKey);

    // Encrypt the column encryption key with a certificate.
    string keyPath = String.Format(@"{0}/My/{1}", certificateStoreLocation, certificateThumbprint);
    SqlColumnEncryptionCertificateStoreProvider provider = new SqlColumnEncryptionCertificateStoreProvider();
    return provider.EncryptColumnEncryptionKey(keyPath, @"RSA_OAEP", columnEncryptionKey);
}
```

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>Always Encrypted のパフォーマンスの影響を制御する

Always Encrypted はクライアント側暗号化テクノロジであるため、ほとんどのパフォーマンス オーバーヘッドは、データベースではなくクライアント側で発生します。 暗号化および暗号化解除の操作のコストとは別に、クライアント側のパフォーマンス オーバーヘッドのその他の原因を次に示します。

- クエリ パラメーターのメタデータを取得するためのデータベースへの追加のラウンド トリップ。
- 列マスター キーにアクセスするための列マスター キー ストアの呼び出し。

このセクションでは、**Microsoft .NET Data Provider for SQL Server** における組み込みのパフォーマンス最適化、および上記の 2 つの要因によるパフォーマンスへの影響を制御する方法について説明します。

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>クエリ パラメーターのメタデータを取得するためのラウンド トリップを制御する

既定では、接続に対して Always Encrypted が有効になっている場合、**Microsoft .NET Data Provider for SQL Server** は、パラメーター化クエリごとに [sys.sp_describe_parameter_encryption](../../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) を呼び出し、クエリ ステートメント (パラメーター値を除く) を SQL Server に渡します。 **sys.sp_describe_parameter_encryption** はクエリ ステートメントを分析して、パラメーターを暗号化する必要があるかどうかを判断し、その必要がある場合は、これらのパラメーターごとに暗号化関連の情報を返します。この情報により、**Microsoft .NET Data Provider for SQL Server** はパラメーター値を暗号化できます。 上記の動作により、クライアント アプリケーションに対する高度な透明性が確保されます。 暗号化された列をターゲットとする値が SqlParameter オブジェクトで **Microsoft .NET Data Provider for SQL Server** に渡される限り、アプリケーション (およびアプリケーション開発者) は、暗号化された列にどのクエリがアクセスするかを認識する必要はありません。

### <a name="query-metadata-caching"></a>クエリ メタデータ キャッシュ

**Microsoft .NET Data Provider for SQL Server** はクエリ ステートメントごとに **sys.sp_describe_parameter_encryption** の結果をキャッシュします。 したがって、同じクエリ ステートメントが複数回実行される場合、ドライバーは **sys.sp_describe_parameter_encryption** を 1 回だけ呼び出します。 クエリ ステートメントの暗号化メタデータ キャッシュにより、データベースからメタデータをフェッチする場合のパフォーマンス コストが大幅に削減されます。 キャッシュは既定で有効になっています。 [SqlConnection.ColumnEncryptionQueryMetadataCacheEnabled プロパティ](/dotnet/api/microsoft.data.sqlclient.sqlconnection.columnencryptionquerymetadatacacheenabled)を false に設定して、パラメーター メタデータ キャッシュを無効にできますが、以下に示すようなまれなケースを除き、無効にすることはお勧めできません。

データベースに `s1` と `s2` という 2 つの異なるスキーマがあるとします。 各スキーマには、`t` という同じ名前のテーブルが含まれています。 `s1.t` と `s2.t` の各テーブルの定義は同じですが、暗号化関連のプロパティは異なります。`c` という名前の列は、`s1.t` では暗号化されませんが、`s2.t` では暗号化されます。 データベースには `u1` と `u2` という 2 人のユーザーがいます。 `u1` ユーザーの既定のスキーマは `s1` です。 `u2` の既定のスキーマは `s2` です。 .NET アプリケーションによってデータベースへの 2 つの接続が開かれ、一方の接続では `u1` ユーザーが借用され、もう一方の接続では `u2` ユーザーが借用されます。 アプリケーションにより、ユーザー `u1` の接続経由で `c` 列をターゲットとするパラメーターを含むクエリが送信されます (クエリではスキーマが指定されないため、既定のユーザー スキーマが想定されます)。 次に、アプリケーションで、`u2` ユーザーの接続経由で同じクエリが送信されます。 クエリ メタデータ キャッシュが有効になっている場合は、最初のクエリの後で、`c` 列 (クエリ パラメーターのターゲット) が暗号化されていないことを示すメタデータがキャッシュに格納されます。 2 番目のクエリのクエリ ステートメントが同じであるため、キャッシュに格納されている情報が使用されます。 その結果、ドライバーにより、パラメーターが暗号化されずにクエリが送信されて (ターゲット列 `s2.t.c` は暗号化対象であるため、この動作は正しくありません)、サーバーにパラメーターのプレーン テキスト値がリークします。 サーバーはその非互換性を検出し、ドライバーに強制的にキャッシュを更新させるため、アプリケーションはパラメーター値が正しく暗号化されたクエリを透過的に再送します。 このような場合は、キャッシュを無効にして、サーバーへの機微な値のリークを防ぐ必要があります。

### <a name="setting-always-encrypted-at-the-query-level"></a>クエリ レベルで Always Encrypted を設定する

パラメーター化クエリに対して暗号化メタデータを取得することによるパフォーマンスへの影響を制御するには、Always Encrypted を接続に対して設定する代わりに、個々のクエリに対して有効にします。 これにより、暗号化された列をターゲットとするパラメーターを含むことがわかっているクエリに対してのみ、 **sys.sp_describe_parameter_encryption** が呼び出されるように設定できます。 ただし、これにより、暗号化の透明度が損なわれることに注意してください。データベースの列の暗号化プロパティを変更する場合は、スキーマの変更に合わせてアプリケーション コードの変更が必要になる可能性があります。

> [!NOTE]
> Always Encrypted をクエリ レベルで設定すると、パラメーター暗号化メタデータ キャッシュのパフォーマンス上の利点が制限されます。

個々のクエリの Always Encrypｔed 動作を制御するには、 [SqlCommand](/dotnet/api/microsoft.data.sqlclient.sqlcommand) および [SqlCommandColumnEncryptionSetting](/dotnet/api/microsoft.data.sqlclient.sqlcommandcolumnencryptionsetting)のこのコンストラクターを使用する必要があります。 有用なガイドラインを次に示します。

- クライアントがデータベース接続を介して送信するほとんどのクエリが、暗号化された列をアクセスする場合:
  - **Column Encryption Setting** 接続文字列キーワードを **[有効]** に設定します。
  - 暗号化された列にアクセスしない個々のクエリに対して、 **SqlCommandColumnEncryptionSetting.Disabled** を設定します。 これにより、**sys.sp_describe_parameter_encryption** の呼び出しと、結果セット内の値を暗号化解除しようとする試みの両方が無効になります。
  - 暗号化を必要とするパラメーターは含まれなくても、暗号化された列からデータを取得する個々のクエリには、**SqlCommandColumnEncryptionSetting.ResultSetOnly** を設定します。 これにより、**sys.sp_describe_parameter_encryption** の呼び出しと、パラメーターの暗号化が無効になります。 クエリは、暗号化列の結果を暗号化解除できます。
- クライアントがデータベース接続を介して送信するほとんどのクエリが、暗号化された列をアクセスしない場合:
  - **Column Encryption Setting** 接続文字列キーワードを **[無効]** に設定します。
  - 暗号化を必要とするパラメーターを含む個々のクエリに対して、 **SqlCommandColumnEncryptionSetting.Enabled** を設定します。 これにより、**sys.sp_describe_parameter_encryption** の呼び出しと、暗号化された列から取得されたクエリ結果の暗号化解除の両方が有効になります。
  - 暗号化を必要とするパラメーターは含まれなくても、暗号化された列からデータを取得するクエリには、**SqlCommandColumnEncryptionSetting.ResultSetOnly** を設定します。 これにより、**sys.sp_describe_parameter_encryption** の呼び出しと、パラメーターの暗号化が無効になります。 クエリは、暗号化列の結果を暗号化解除できます。

次の例では、データベース接続に対して Always Encrypted が無効になっています。 アプリケーションが実行するクエリに、暗号化されていない LastName 列をターゲットとするパラメーターが含まれています。 このクエリを使用すると、どちらも暗号化されている `SSN` および `BirthDate` 列からデータが取得されます。 このような場合、暗号化メタデータを取得するために **sys.sp_describe_parameter_encryption** を呼び出す必要はありません。 ただし、アプリケーションが 2 つの暗号化された列からプレーンテキスト値を受け取ることができるよう、クエリ結果の暗号化解除を有効にする必要があります。 それを確実に行うために、**SqlCommandColumnEncryptionSetting.ResultSetOnly** 設定が使用されます。

```cs
string connectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true";
using (SqlConnection connection = new SqlConnection(connectionString))
using (SqlCommand cmd = new SqlCommand(@"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName]=@LastName",
connection, null, SqlCommandColumnEncryptionSetting.ResultSetOnly))
{
    connection.Open();
    SqlParameter paramLastName = cmd.CreateParameter();
    paramLastName.ParameterName = @"@LastName";
    paramLastName.DbType = DbType.String;
    paramLastName.Direction = ParameterDirection.Input;
    paramLastName.Value = "Abel";
    paramLastName.Size = 50;
    cmd.Parameters.Add(paramLastName);
    using (SqlDataReader reader = cmd.ExecuteReader())
    {
        if (reader.HasRows)
        {
            while (reader.Read())
            {
                Console.WriteLine(@"{0}, {1}, {2}, {3}", reader[0], reader[1], reader[2], ((DateTime)reader[3]).ToShortDateString());
            }
        }
    }
}
```

### <a name="column-encryption-key-caching"></a>列暗号化キーのキャッシュ

列暗号化キーを暗号化解除するための列マスター キー ストアの呼び出し回数を減らすために、**Microsoft .NET Data Provider for SQL Server** は、プレーンテキストの列暗号化キーをメモリにキャッシュします。 暗号化された列暗号化キー値をデータベース メタデータから受け取った後、ドライバーは、暗号化されたキー値に対応するプレーンテキストの列暗号化キーをまず見つけようとします。 ドライバーは、暗号化された列暗号化キー値がキャッシュ内に見つからない場合にのみ、列マスター キーを含むキー ストアを呼び出します。

セキュリティ上の理由から構成可能な有効期間後にキャッシュ エントリが削除されます。 既定の有効期間の値は 2 時間です。 アプリケーションで列暗号化キーをプレーンテキストでキャッシュできる期間について、より厳密なセキュリティ要件がある場合は、[SqlConnection.ColumnEncryptionKeyCacheTtl プロパティ](/dotnet/api/microsoft.data.sqlclient.sqlconnection.columnencryptionkeycachettl)を使用して期間を変更できます。 

## <a name="enabling-additional-protection-for-a-compromised-sql-server"></a>侵害された SQL Server の追加保護を有効にする

既定では、**Microsoft .NET Data Provider for SQL Server** は、データベース システム (SQL Server または Azure SQL データベース) を使用して、データベースの暗号化対象の列と暗号化の方法に関するメタデータを提供します。 暗号化メタデータを使用することで、**Microsoft .NET Data Provider for SQL Server** は、アプリケーションからの入力なしに、クエリ パラメーターを暗号化し、クエリ結果を復号化できます。これにより、アプリケーションで必要な変更の数が大幅に削減されます。 ただし、SQL Server プロセスが侵害され、SQL Server が **Microsoft .NET Data Provider for SQL Server** に送信したメタデータを攻撃者が改ざんした場合、その攻撃者は機密情報を盗むことができる可能性があります。 このセクションでは、透明度は損なわれますが、この種の攻撃に対する追加の保護レベルを提供するのに役立つ API について説明します。

### <a name="forcing-parameter-encryption"></a>パラメーターの暗号化の強制適用

**Microsoft .NET Data Provider for SQL Server** は、SQL Server にパラメーター化クエリを送信する前に、[sys.sp_describe_parameter_encryption](../../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) を呼び出して、SQL Server に対して、クエリ ステートメントを分析し、クエリ内のどのパラメーターを暗号化する必要があるかという情報を提供するよう要求します。 実際にはデータベースの列が暗号化されていても、侵害された SQL Server インスタンスは、パラメーターが暗号化された列をターゲットにしていないことを示すメタデータを送信して、**Microsoft .NET Data Provider for SQL Server** を誤解させる可能性があります。 その結果、**Microsoft .NET Data Provider for SQL Server** は、パラメーターの値を暗号化せずに、侵害された SQL Server インスタンスにプレーンテキストとして値を送信するようになります。

このような攻撃を防ぐために、アプリケーションはパラメーターの [SqlParameter.ForceColumnEncryption プロパティ](/dotnet/api/microsoft.data.sqlclient.sqlparameter.forcecolumnencryption) を true に設定することができます。 これにより、**Microsoft .NET Data Provider for SQL Server** は、サーバーから受信したメタデータに、パラメーターを暗号化する必要がないことが示されている場合に、例外をスローするようになります。

**SqlParameter.ForceColumnEncryption プロパティ** の使用はセキュリティの向上に役立ちますが、クライアント アプリケーションに対する暗号化の透明度が損なわれます。 データベース スキーマを更新して暗号化された列のセットを変更する場合は、アプリケーションの変更も必要になることがあります。

以下のコード サンプルに、**SqlParameter.ForceColumnEncryption プロパティ** を使用して、社会保障番号がプレーンテキストでデータベースに送信されないようにする方法を示します。

```cs
using (SqlCommand cmd = _sqlconn.CreateCommand())
{
    // Use parameterized queries to access Always Encrypted data.

    cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN] = @SSN;";

    SqlParameter paramSSN = cmd.CreateParameter();
    paramSSN.ParameterName = @"@SSN";
    paramSSN.DbType = DbType.AnsiStringFixedLength;
    paramSSN.Direction = ParameterDirection.Input;
    paramSSN.Value = ssn;
    paramSSN.Size = 11;
    paramSSN.ForceColumnEncryption = true;
    cmd.Parameters.Add(paramSSN);

    using (SqlDataReader reader = cmd.ExecuteReader())
    {
        // Do something.
    }
}
```

### <a name="configuring-trusted-column-master-key-paths"></a>信頼された列マスター キー パスの構成

暗号化された列をターゲットとするクエリ パラメーターと暗号化列から取得された結果について SQL Server が返す暗号化メタデータには、キー ストアとキー ストア内のキーの場所を識別する列マスター キーのキー パスが含まれています。 SQL Server インスタンスは、侵害された場合、攻撃者が制御する場所に **Microsoft .NET Data Provider for SQL Server** を誘導するキー パスを送信する可能性があります。 これにより、アプリケーションの認証を必要とするキー ストアの場合、キー ストアの資格情報が漏えいする可能性があります。

このような攻撃を防ぐために、アプリケーションは、[SqlConnection.ColumnEncryptionTrustedMasterKeyPaths プロパティ](/dotnet/api/microsoft.data.sqlclient.sqlconnection.columnencryptiontrustedmasterkeypaths)を使用して、特定のサーバーに対して信頼されたキー パスの一覧を指定することができます。 **Microsoft .NET Data Provider for SQL Server** は、信頼されたキー パスの一覧にないキー パスを受信した場合、例外をスローします。

信頼されたキー パスを設定するとアプリケーションのセキュリティが向上しますが、列マスター キーのローテーション (列マスター キー パスの変更) を行うたびに、アプリケーションのコードや構成を変更する必要があります。

次の例では、信頼された列マスター キー パスを構成する方法を示します。

```cs
// Configure trusted key paths to protect against fake key paths sent by a compromised SQL Server instance
// First, create a list of trusted key paths for your server
List<string> trustedKeyPathList = new List<string>();
trustedKeyPathList.Add("CurrentUser/my/425CFBB9DDDD081BB0061534CE6AB06CB5283F5Ea");

// Register the trusted key path list for your server
SqlConnection.ColumnEncryptionTrustedMasterKeyPaths.Add(serverName, trustedKeyPathList);

```

## <a name="copying-encrypted-data-using-sqlbulkcopy"></a>SqlBulkCopy を使用して、暗号化されたデータをコピーする

SqlBulkCopy を使用して、データの暗号化解除を行うことなく、既に暗号化されて 1 つのテーブルに格納されているデータを別のテーブルにコピーできます。 その手順を次に示します。

- ターゲット テーブルの暗号化構成が、ソース テーブルの構成と同じであることを確認します。 具体的には、両方のテーブルで同じ列が暗号化されており、同じ暗号化タイプおよび同じ暗号化キーを使用してこれらの列が暗号化されている必要があります。 いずれかのターゲット列が、対応するソース列と異なる方法で暗号化されている場合、コピー操作の後でターゲット テーブル内のデータを暗号化解除することはできません。 データは破損します。
- Always Encrypted を有効にせずに、ソース テーブルとターゲット テーブルへの両方のデータベース接続を構成します。
- `AllowEncryptedValueModifications` オプションを設定します ([SqlBulkCopyOptions](/dotnet/api/microsoft.data.sqlclient.sqlbulkcopyoptions) に関するページを参照してください)。

> [!NOTE]
> データベースが破損する可能性があるので、`AllowEncryptedValueModifications` を指定する際には注意が必要です。**Microsoft .NET Data Provider for SQL Server** は、データが実際に暗号化されているかどうか、またはターゲット列と同じ暗号化の種類、アルゴリズム、およびキーを使用して正しく暗号化されているかどうかをチェックしないためです。

次の例は、テーブル間でデータをコピーする方法を示しています。 `SSN` と `BirthDate` 列は暗号化されていると仮定します。

```cs
static public void CopyTablesUsingBulk(string sourceTable, string targetTable)
{
    string sourceConnectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true";
    string targetConnectionString = "Data Source=server64; Initial Catalog=Clinic; Integrated Security=true";
    using (SqlConnection connSource = new SqlConnection(sourceConnectionString))
    {
        connSource.Open();
        using (SqlCommand cmd = new SqlCommand(string.Format("SELECT [PatientID], [SSN], [FirstName], [LastName], [BirthDate] FROM {0}", sourceTable), connSource))
        {
            using (SqlDataReader reader = cmd.ExecuteReader())
            using (SqlBulkCopy copy = new SqlBulkCopy(targetConnectionString, SqlBulkCopyOptions.KeepIdentity | SqlBulkCopyOptions.AllowEncryptedValueModifications))
            {
                copy.EnableStreaming = true;
                copy.DestinationTableName = targetTable;
                copy.WriteToServer(reader);
            }
        }
    }
}
```

## <a name="always-encrypted-api-reference"></a>Always Encrypted API リファレンス

**名前空間:** [Microsoft.Data.SqlClient](/dotnet/api/microsoft.data.sqlclient)

**アセンブリ:** Microsoft.Data.SqlClient.dll

|名前|説明|
|:---|:---|
|[SqlColumnEncryptionCertificateStoreProvider クラス](/dotnet/api/microsoft.data.sqlclient.sqlcolumnencryptioncertificatestoreprovider)|Windows 証明書ストアのキー ストア プロバイダー。|
|[SqlColumnEncryptionCngProvider クラス](/dotnet/api/microsoft.data.sqlclient.sqlcolumnencryptioncngprovider)|Microsoft Cryptography API: Next Generation (CNG) のキー ストア プロバイダー。|
|[SqlColumnEncryptionCspProvider クラス](/dotnet/api/microsoft.data.sqlclient.sqlcolumnencryptioncspprovider)|Microsoft CAPI ベースの暗号化サービス プロバイダー (CSP) のキー ストア プロバイダー。|
|[SqlColumnEncryptionKeyStoreProvider クラス](/dotnet/api/microsoft.data.sqlclient.sqlcolumnencryptionkeystoreprovider)|キー ストア プロバイダーの基本クラス。|
|[SqlCommandColumnEncryptionSetting 列挙体](/dotnet/api/microsoft.data.sqlclient.sqlcommandcolumnencryptionsetting)|個々のクエリの Always Encrypted の動作を制御するための設定。|
|[SqlConnectionAttestationProtocol 列挙型](/dotnet/api/microsoft.data.sqlclient.sqlconnectionattestationprotocol)|セキュリティで保護されたエンクレーブをが設定された Always Encrypted を使用するときに、構成証明プロトコルの値を指定します|
|[SqlConnectionColumnEncryptionSetting 列挙体](/dotnet/api/microsoft.data.sqlclient.sqlconnectioncolumnencryptionsetting)|データベース接続の暗号化と暗号化解除を有効にするための設定。|
|[SqlConnectionStringBuilder.ColumnEncryptionSetting プロパティ](/dotnet/api/microsoft.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting)|接続文字列で、Always Encrypted を取得して設定します。|
|[SqlConnection.ColumnEncryptionQueryMetadataCacheEnabled プロパティ](/dotnet/api/microsoft.data.sqlclient.sqlconnection.columnencryptionquerymetadatacacheenabled)|暗号化クエリ メタデータ キャッシュの有効化と無効化を行います。|
|[SqlConnection.ColumnEncryptionKeyCacheTtl プロパティ](/dotnet/api/microsoft.data.sqlclient.sqlconnection.columnencryptionkeycachettl)|列暗号化キー キャッシュ内のエントリの有効期間の取得と設定を行います。|
|[SqlConnection.ColumnEncryptionTrustedMasterKeyPaths プロパティ](/dotnet/api/microsoft.data.sqlclient.sqlconnection.columnencryptiontrustedmasterkeypaths)|データベース サーバーの信頼されたキー パスの一覧を設定できます。 アプリケーションのクエリを処理中に、一覧に存在しないキー パスをドライバーが受け取ると、クエリは失敗します。 このプロパティは、セキュリティが侵害され、偽のキー パスを提供し、キー ストアの資格情報漏洩につながるおそれがある SQL Server を含めたセキュリティ攻撃に対して、セキュリティ保護をさらに強化します。|
|[SqlConnection.RegisterColumnEncryptionKeyStoreProviders メソッド](/dotnet/api/microsoft.data.sqlclient.sqlconnection.registercolumnencryptionkeystoreproviders)|カスタム キー ストア プロバイダーを登録できます。 これは、キー ストア プロバイダー名をキー ストア プロバイダー実装にマップするディクショナリです。|
|[SqlCommand コンストラクター (String、SqlConnection、SqlTransaction、SqlCommandColumnEncryptionSetting)](/dotnet/api/microsoft.data.sqlclient.sqlcommand.-ctor?view=sqlclient-dotnet-core-1.0&preserve-view=true#Microsoft_Data_SqlClient_SqlCommand__ctor_System_String_Microsoft_Data_SqlClient_SqlConnection_Microsoft_Data_SqlClient_SqlTransaction_Microsoft_Data_SqlClient_SqlCommandColumnEncryptionSetting_)|個々のクエリの Always Encrypted の動作を制御できます。|
|[SqlParameter.ForceColumnEncryption プロパティ](/dotnet/api/microsoft.data.sqlclient.sqlparameter.forcecolumnencryption)|パラメーターの暗号化を強制的に適用します。 パラメーターの暗号化が不要であることが SQL Server からドライバーに通知された場合、このパラメーターを使用するクエリは失敗します。 攻撃を受けた SQL Server がクライアントに不正な暗号化メタデータを提供すると、データ漏えいが引き起こされる可能性がありますが、このプロパティは、そのようなセキュリティ攻撃に対する保護を強化します。|
|[接続文字列](/dotnet/api/microsoft.data.sqlclient.sqlconnection.connectionstring)のキーワード: `Column Encryption Setting=enabled`|接続に対して Always Encrypted 機能を有効または無効にします。|

## <a name="see-also"></a>関連項目

- [常に暗号化](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-enclaves.md)
- [SQL Database のチュートリアル:Always Encrypted で機密データを保護する](/azure/azure-sql/database/always-encrypted-certificate-store-configure)
- [チュートリアル:セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する .NET アプリケーションの開発](tutorial-always-encrypted-enclaves-develop-net-apps.md)」をご覧ください。
- [例:Azure Key Vault と Always Encrypted の連携](azure-key-vault-example.md)
- [例:Azure Key Vault と、セキュリティで保護されたエンクレーブが設定された Always Encrypted の連携](azure-key-vault-enclave-example.md)。
