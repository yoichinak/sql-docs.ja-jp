---
title: 接続文字列の構文
description: Microsoft SqlClient Data Provider for SQL Server の接続文字列の構文について説明します。 各プロバイダーの構文は、対応する ConnectionString プロパティのトピックで説明されています。
ms.date: 11/13/2020
ms.assetid: 0977aeee-04d1-4cce-bbed-750c77fce06e
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 40fc82cdc264951d1e776875a48b5a516b4b26a8
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126522"
---
# <a name="connection-string-syntax"></a>接続文字列の構文

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

<xref:Microsoft.Data.SqlClient> には、<xref:System.Data.Common.DbConnection> から継承される `Connection` オブジェクトと、プロバイダー固有の <xref:System.Data.Common.DbConnection.ConnectionString%2A> プロパティがあります。 SqlClient プロバイダーの特定の接続文字列の構文については、その `ConnectionString` プロパティに記載されています。 接続文字列の構文の詳細については、「<xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>」を参照してください。

## <a name="connection-string-builders"></a>接続文字列ビルダー

 Microsoft SqlClient Data Provider for SQL Server では、次の接続文字列ビルダーが導入されました。

- <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder>

接続文字列ビルダーを使用すると、構文的に正しい接続文字列を実行時に構築できるため、コード内で接続文字列値を手動で連結する必要はありません。 詳細については、「[接続文字列ビルダー](connection-string-builders.md)」をご覧ください。

## <a name="windows-authentication"></a>Windows 認証

データ ソースでサポートされている場合は、Windows 認証 ("*統合セキュリティ*" とも呼ばれます) を使用して接続することをお勧めします。 次の表は、Microsoft SqlClient Data Provider for SQL Server で使用される Windows 認証構文を示しています。

|プロバイダー|構文|  
|--------------|------------|  
|`SqlClient`|`Integrated Security=true;`<br /><br /> `-- or --`<br /><br /> `Integrated Security=SSPI;`|  

## <a name="sqlclient-connection-strings"></a>SqlClient 接続文字列

<xref:Microsoft.Data.SqlClient.SqlConnection> 接続文字列の構文については、<xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=nameWithType> プロパティで説明されています。 <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A> プロパティを使用すると、SQL Server データベースの接続文字列を取得または設定することができます。 接続文字列のキーワードは、<xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> のプロパティにもマップされます。

> [!IMPORTANT]
> `Persist Security Info` キーワードの既定の設定は `false` です。 このキーワードを `true` または `yes` に設定すると、ユーザー ID やパスワードなどのセキュリティ関連情報を、接続を開いた後にその接続から取得できます。 機密を要する接続文字列情報が、信頼できないソースによってアクセスされることのないよう、`Persist Security Info` は必ず `false` にしてください。

### <a name="windows-authentication-with-sqlclient"></a>SqlClient での Windows 認証

次の構文のフォームはそれぞれ、Windows 認証を使用してローカル サーバー上の **AdventureWorks** データベースに接続します。

```csharp  
"Persist Security Info=False;Integrated Security=true;  
    Initial Catalog=AdventureWorks;Server=MSSQL1"  
"Persist Security Info=False;Integrated Security=SSPI;  
    database=AdventureWorks;server=(local)"  
"Persist Security Info=False;Trusted_Connection=True;  
    database=AdventureWorks;server=(local)"  
```  

### <a name="sql-server-authentication-with-sqlclient"></a>SqlClient での SQL Server 認証

SQL Server への接続には Windows 認証の使用をお勧めします。 ただし、どうしても SQL Server 認証を使用する必要がある場合は、次の構文に従ってユーザー名とパスワードを指定してください。 この例では、アスタリスクを使用して有効なユーザー名とパスワードを表しています。

```csharp  
"Persist Security Info=False;User ID=*****;Password=*****;Initial Catalog=AdventureWorks;Server=MySqlServer"  
```  

Azure SQL Database または Azure SQL Data Warehouse に接続し、`user@servername` の形式でログインを指定する場合は、ログインの `servername` の値が `Server=` に指定されている値と一致することを確認します。

> [!NOTE]
> Windows 認証は SQL Server ログインよりも優先されます。 Integrated Security を true に指定し、ユーザー名とパスワードも指定した場合、ユーザー名とパスワードは無視され、Windows 認証が使用されます。

### <a name="connect-to-a-named-instance-of-sql-server"></a>SQL Server の名前付きインスタンスに接続する

SQL Server の名前付きインスタンスに接続するには、*server name\instance name* 構文を使用します。

```csharp  
"Data Source=MySqlServer\MSSQL1;"  
```  

接続文字列の作成時に、<xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.DataSource%2A> の `SqlConnectionStringBuilder` プロパティをインスタンス名に設定することもできます。 <xref:Microsoft.Data.SqlClient.SqlConnection.DataSource%2A> オブジェクトの <xref:Microsoft.Data.SqlClient.SqlConnection> プロパティは読み取り専用です。

### <a name="type-system-version-changes"></a>Type System Version の変更

<xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=nameWithType> の `Type System Version` キーワードは、クライアント側での SQL Server 型の表現を指定します。 <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=nameWithType> キーワードの詳細については、`Type System Version` のトピックを参照してください。

## <a name="connecting-and-attaching-to-sql-server-express-user-instances"></a>SQL Server Express ユーザー インスタンスへの接続とアタッチ

ユーザー インスタンスは、SQL Server Express の機能の 1 つです。 最小限の特権しか持たないローカル Windows アカウントで実行しているユーザーが、SQL Server データベースにアタッチできます。この場合、管理特権は不要です。 ユーザー インスタンスは、サービスとしてではなく、ユーザーの Windows 資格情報で実行されます。

ユーザー インスタンスの使用について詳しくは、「[SQL Server Express ユーザー インスタンス](./sql/sql-server-express-user-instances.md)」をご覧ください。

## <a name="using-trustservercertificate"></a>TrustServerCertificate の使用

`TrustServerCertificate` キーワードは、有効な証明書を使用して SQL Server インスタンスに接続する場合にのみ使用できます。 `TrustServerCertificate` が `true` に設定されている場合は、トランスポート層で TLS/SSL を使用してチャネルを暗号化し、証明書チェーンで信頼性を検証する処理をバイパスします。

```csharp  
"TrustServerCertificate=true;"
```  

> [!NOTE]
> `TrustServerCertificate` を `true` に設定して暗号化を有効にした場合、接続文字列で `Encrypt` を `false` に設定したとしても、サーバーで指定された暗号化レベルが使用されます。 それ以外の場合、接続は失敗します。

### <a name="enabling-encryption"></a>暗号化の有効化

サーバー証明書がプロビジョニングされていない場合、暗号化を有効にするには、SQL Server 構成マネージャーで **[プロトコルの暗号化を設定する]** オプションと **[サーバー証明書を信頼する]** オプションを設定する必要があります。 このように、検証可能なサーバー証明書がプロビジョニングされていない場合、暗号化には検証を伴わない自己署名入りのサーバー証明書が使用されます。

SQL Server で構成されたセキュリティのレベルを、アプリケーションの設定によって緩和することはできません。ただし、必要に応じて厳密にすることはできます。 アプリケーションから暗号化を要求するには、`TrustServerCertificate` キーワードおよび `Encrypt` キーワードを `true` に設定します。こうすることで、サーバー証明書がプロビジョニングされておらず、なおかつ、クライアントで **[プロトコルの暗号化を設定する]** が構成されていない場合でも常に暗号化が行われます。 ただし、クライアントの構成で `TrustServerCertificate` を有効にしなかった場合は、プロビジョニングされたサーバー証明書が必要です。

次の表ですべてのケースを説明します。

|[プロトコルの暗号化を設定する] クライアント設定|[サーバー証明書を信頼する] クライアント設定|Encrypt/Use Encryption for Data 接続文字列/属性|Trust Server Certificate 接続文字列/属性|結果|  
|----------------------------------------------|---------------------------------------------|-------------------------------------------------------------------|-----------------------------------------------------------|------------|  
|いいえ|N/A|無効 (既定値)|無視|暗号化は行われません。|  
|いいえ|該当なし|はい|無効 (既定値)|暗号化は、検証可能なサーバー証明書が提供されている場合にのみ行われます。それ以外の場合は、接続試行が失敗します。|  
|いいえ|該当なし|はい|はい|暗号化は常に行われますが、自己署名入りのサーバー証明書を使用することがあります。|  
|はい|いいえ|無視|無視|暗号化は、検証可能なサーバー証明書が提供されている場合にのみ行われます。それ以外の場合は、接続試行が失敗します。|  
|はい|はい|無効 (既定値)|無視|暗号化は常に行われますが、自己署名入りのサーバー証明書を使用することがあります。|  
|はい|はい|はい|無効 (既定値)|暗号化は、検証可能なサーバー証明書が提供されている場合にのみ行われます。それ以外の場合は、接続試行が失敗します。|  
|はい|はい|はい|はい|暗号化は常に行われますが、自己署名入りのサーバー証明書を使用することがあります。|  

詳細については、「[検証を伴わない暗号化の使用](/sql/relational-databases/native-client/features/using-encryption-without-validation)」を参照してください。

## <a name="see-also"></a>関連項目

- [接続文字列](connection-strings.md)
- [データ ソースへの接続](connecting-to-data-source.md)
