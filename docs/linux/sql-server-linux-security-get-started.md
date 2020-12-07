---
title: Linux での SQL Server のセキュリティの概要
description: さらに調査する部分がわかるように、SQL Server on Linux のセキュリティ機能について説明します。
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ecc72850-8b01-492e-9a27-ec817648f0e0
ms.openlocfilehash: 4a9137ad71947d222d246df046c6ab573fb4500d
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115815"
---
# <a name="walkthrough-for-the-security-features-of-sql-server-on-linux"></a>SQL Server on Linux のセキュリティ機能のチュートリアル

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

SQL Server を初めて使用する Linux ユーザーの場合は、以下のタスクでは一部のセキュリティ タスクの手順がわかります。 これらは Linux 独自または固有のものではありませんが、さらに調べる領域について考えるヒントになります。 各例には、その領域の詳細なドキュメントのリンクが記載されています。

> [!NOTE]
>  次の例では、**AdventureWorks2014** サンプル データベースを使用します。 このサンプル データベースを入手してインストールする手順については、[Windows から Linux への SQL Server データベースの復元](sql-server-linux-migrate-restore-database.md)に関する記事を参照してください。


## <a name="create-a-login-and-a-database-user"></a>ログインとデータベース ユーザーを作成する 

[CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md) ステートメントを使って master データベースにログインを作成することにより、他のユーザーに SQL Server へのアクセスを許可します。 次に例を示します。

```
CREATE LOGIN Larry WITH PASSWORD = '************';  
```

> [!NOTE]
>  前のコマンドのアスタリスクの代わりに、常に強力なパスワードを使用します。

ログインは、SQL Server に接続し、master データベースに (制限付きで) アクセスできます。 ユーザー データベースに接続するには、データベース レベルで対応するデータベース ユーザーと呼ばれる ID がログインに必要です。 ユーザーは各データベースに固有であり、アクセス権を付与するには、データベースごとに個別に作成する必要があります。 次の例では、AdventureWorks2014 データベースに移動し、[CREATE USER](../t-sql/statements/create-user-transact-sql.md) ステートメントを使って、ログイン名 Larry に関連付けられている Larry という名前のユーザーを作成します。 ログインとユーザーは関連して (相互にマップされて) いますが、それらは異なるオブジェクトです。 ログインは、サーバー レベルの原則です。 ユーザーは、データベース レベルのプリンシパルです。

```
USE AdventureWorks2014;
GO
CREATE USER Larry;
GO
```

- SQL Server の管理者アカウントでは、任意のデータベースに接続し、データベースにさらに多くのログインとユーザーを作成できます。  
- データベースを作成したユーザーはデータベース所有者になり、そのデータベースに接続できます。 データベース所有者は、さらにユーザーを作成できます。

その後、他のログインに `ALTER ANY LOGIN` アクセス許可を付与することで、より多くのログインを作成することを承認できます。 データベース内では、他のユーザーに `ALTER ANY USER` アクセス許可を付与することで、より多くのユーザーを作成することを承認できます。 次に例を示します。   

```
GRANT ALTER ANY LOGIN TO Larry;   
GO   
   
USE AdventureWorks2014;   
GO   
GRANT ALTER ANY USER TO Jerry;    
GO   
```

これで、ログイン Larry はさらに多くのログインを作成でき、ユーザー Jerry はより多くのユーザーを作成できるようになります。


## <a name="granting-access-with-least-privileges"></a>最小限の特権でアクセス権を付与する

ユーザー データベースに最初に接続するユーザーは、管理者アカウントとデータベース所有者アカウントになります。 ただし、これらのユーザーは、データベースに対するすべてのアクセス許可を使用できます。 これは、ほとんどのユーザーが持つべきものより多いアクセス許可です。 

作業を始めるだけのときは、組み込みの "*固定データベース ロール*" を使って、いくつかの一般的なアクセス許可のカテゴリを割り当てることができます。 たとえば、`db_datareader` 固定データベース ロールでは、データベース内のすべてのテーブルを読み取ることができますが、変更することはできません。 固定データベース ロールのメンバーシップを許可するには、[ALTER ROLE](../t-sql/statements/alter-role-transact-sql.md) ステートメントを使います。 次の例では、ユーザー `Jerry` を `db_datareader` 固定データベース ロールに追加します。   
   
```   
USE AdventureWorks2014;   
GO   
   
ALTER ROLE db_datareader ADD MEMBER Jerry;   
```   

固定データベース ロールの一覧については、「[データベース レベルのロール](../relational-databases/security/authentication-access/database-level-roles.md)」をご覧ください。

後で、データへのより正確なアクセス (強くお勧めします) を構成する準備ができたら、[CREATE ROLE](../t-sql/statements/create-role-transact-sql.md) ステートメントを使って、独自のユーザー定義のデータベース ロールを作成します。 次に、カスタム ロールに特定の詳細なアクセス許可を割り当てます。

たとえば、次のステートメントでは、`Sales` という名前のデータベース ロールが作成され、`Sales` グループに対して `Orders` テーブルの行を表示、更新、削除する権限が与えられてから、ユーザー `Jerry` が `Sales` ロールに追加されます。   
   
```   
CREATE ROLE Sales;   
GRANT SELECT ON Object::Sales TO Orders;   
GRANT UPDATE ON Object::Sales TO Orders;   
GRANT DELETE ON Object::Sales TO Orders;   
ALTER ROLE Sales ADD MEMBER Jerry;   
```

権限システムの詳細については、「[データベース エンジンの権限の概要](../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)」を参照してください。


## <a name="configure-row-level-security"></a>行レベルのセキュリティを構成する  

[行レベルのセキュリティ](../relational-databases/security/row-level-security.md)を使用すると、クエリを実行するユーザーに基づいて、データベース内の行へのアクセスを制限することができます。 この機能は、お客様が自分のデータにのみアクセスできるようにする場合や、ユーザーが自分の部署に関連するデータにのみアクセスできるようにする場合などに役立ちます。   

次の手順では、`Sales.SalesOrderHeader` テーブルに対して異なる行レベルのアクセス権を持つ 2 人のユーザーを設定する方法について説明します。 

行レベルのセキュリティをテストするには、次の 2 つのユーザー アカウントを作成します。    
   
```   
USE AdventureWorks2014;   
GO   
   
CREATE USER Manager WITHOUT LOGIN;     
   
CREATE USER SalesPerson280 WITHOUT LOGIN;    
```

両方のユーザーに、`Sales.SalesOrderHeader` テーブルに対する読み取りアクセス権を付与します。    
   
```   
GRANT SELECT ON Sales.SalesOrderHeader TO Manager;      
GRANT SELECT ON Sales.SalesOrderHeader TO SalesPerson280;
```
   
新しいスキーマと、インライン テーブル値関数を作成します。 `SalesPersonID` 列内の行が `SalesPerson` ログインの ID と一致する場合、またはクエリを実行しているユーザーがマネージャー ユーザーである場合、関数は 1 を返します。   
   
```     
CREATE SCHEMA Security;   
GO   
   
CREATE FUNCTION Security.fn_securitypredicate(@SalesPersonID AS int)     
    RETURNS TABLE   
WITH SCHEMABINDING   
AS     
   RETURN SELECT 1 AS fn_securitypredicate_result    
WHERE ('SalesPerson' + CAST(@SalesPersonId as VARCHAR(16)) = USER_NAME())     
    OR (USER_NAME() = 'Manager');    
```

テーブルで、フィルター述語およびブロック述語としてこの関数を追加するセキュリティ ポリシーを作成します。  

```
CREATE SECURITY POLICY SalesFilter   
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader,   
ADD BLOCK PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader   
WITH (STATE = ON);   
```

次を実行し、`SalesOrderHeader` テーブルに各ユーザーとしてクエリを実行します。 `SalesPerson280` によって、それぞれの売上から 95 行だけが表示され、テーブル内のすべての行が `Manager` に表示されることを確認します。  

```    
EXECUTE AS USER = 'SalesPerson280';   
SELECT * FROM Sales.SalesOrderHeader;    
REVERT; 
 
EXECUTE AS USER = 'Manager';   
SELECT * FROM Sales.SalesOrderHeader;   
REVERT;   
```
 
セキュリティ ポリシーを変更してポリシーを無効にします。  これで、両方のユーザーがすべての行にアクセスできるようになりました。 

```
ALTER SECURITY POLICY SalesFilter   
WITH (STATE = OFF);    
``` 


## <a name="enable-dynamic-data-masking"></a>動的データ マスクを有効にする

[動的データ マスク](../relational-databases/security/dynamic-data-masking.md)を使用すると、特定の列を完全にまたは部分的にマスキングすることによって、アプリケーションのユーザーに機密データの公開を制限することができます。 

`Person.EmailAddress` テーブルの `EmailAddress` 列にマスキング関数を追加するには、`ALTER TABLE` ステートメントを使用します。 
 
```
USE AdventureWorks2014;
GO
ALTER TABLE Person.EmailAddress    
ALTER COLUMN EmailAddress    
ADD MASKED WITH (FUNCTION = 'email()');
``` 
 
テーブルに対する `SELECT` のアクセス許可を持つ新しいユーザー `TestUser` を作成し、次に `TestUser` としてクエリを実行して、マスクされたデータを表示します。   

```  
CREATE USER TestUser WITHOUT LOGIN;   
GRANT SELECT ON Person.EmailAddress TO TestUser;    
 
EXECUTE AS USER = 'TestUser';   
SELECT EmailAddressID, EmailAddress FROM Person.EmailAddress;       
REVERT;    
```
 
マスキング関数によって、最初のレコードの電子メール アドレスが次のように変更されていることを確認します。
  
|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |ken0@adventure-works.com |    
 
変更前: 

|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |kXXX@XXXX.com |   


## <a name="enable-transparent-data-encryption"></a>Transparent Data Encryption の有効化

データベースに対する脅威の 1 つに、誰かがデータベース ファイルをハード ドライブから盗み出すリスクがあります。 これは、侵入者がシステムへの昇格されたアクセス権を取得すること、問題のある従業員のアクション、ファイルを含むコンピューター (ラップトップなど) の盗難などによって発生する可能性があります。

Transparent Data Encryption (TDE) は、ハード ドライブに格納されているデータ ファイルを暗号化します。 データベース エンジンがデータを操作できるように、SQL Server データベース エンジンのマスター データベースには暗号化キーがあります。 キーへのアクセス権なしには、データベース ファイルを読み取ることができません。 上級管理者は、キーの管理、バックアップ、再作成を行うことができます。そのため、データベースを移動することはできますが、選ばれたメンバーのみが行えます。 TDE を構成すると、`tempdb` データベースも自動的に暗号化されます。 

データベース エンジンはデータを読み取ることができるため、Transparent Data Encryption では、メモリを直接読み取ることができるコンピューターの管理者による不正なアクセスや、管理者アカウントを使用した SQL Server へのアクセスを防ぐことはできません。

### <a name="configure-tde"></a>TDE の構成

- マスター キーを作成します。
- マスター キーで保護された証明書を作成または取得します。
- データベース暗号化キーを作成し、証明書で保護します。
- 暗号化を使用するようにデータベースを設定します。

TDE を構成するには、マスター データベースに対する `CONTROL` 権限と、ユーザー データベースに対する `CONTROL` 権限が必要です。 通常、管理者が TDE を構成します。 

次の例では、 `AdventureWorks2014` という名前のサーバーにインストールされた証明書を使用して、 `MyServerCert`データベースを暗号化および暗号化解除しています。


```
USE master;  
GO  

CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**********';  
GO  

CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My Database Encryption Key Certificate';  
GO  

USE AdventureWorks2014;  
GO
  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_256  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO
  
ALTER DATABASE AdventureWorks2014  
SET ENCRYPTION ON;   
```

TDE を削除するには、`ALTER DATABASE AdventureWorks2014 SET ENCRYPTION OFF;` を実行します。   

暗号化および暗号化解除の操作は、SQL Server によってバックグラウンド スレッドでスケジュールされます。 これらの操作の状態は、この後の一覧に示すカタログ ビューおよび動的管理ビューを使用して確認できます。   

> [!WARNING]
>  TDE が有効になっているデータベースのバックアップ ファイルも、データベース暗号化キーを使用して暗号化されます。 このため、このバックアップを復元するときには、データベース暗号化キーを保護している証明書が必要です。 つまり、データの損失を防ぐには、データベースをバックアップするだけでなく、サーバー証明書のバックアップも確実に保守する必要があります。 証明書が使用できなくなると、データの損失が発生します。 詳細については、「 [SQL Server Certificates and Asymmetric Keys](../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)」をご覧ください。  

TDE の詳細については、「[Transparent Data Encryption (TDE)](../relational-databases/security/encryption/transparent-data-encryption.md)」を参照してください。   


## <a name="configure-backup-encryption"></a>バックアップの暗号化の構成
SQL Server には、バックアップの作成中にデータを暗号化する機能があります。 バックアップの作成時に暗号化アルゴリズムと暗号化機能 (証明書または非対称キー) を指定することにより、暗号化されたバックアップ ファイルを作成することができます。    
  
> [!WARNING]
> 証明書または非対称キーをバックアップすることが非常に重要であり、これらを使用して暗号化したバックアップ ファイルとは別の場所に保存することをお勧めします。 証明書または非対称キーがないと、バックアップ ファイルが使用不可能になり、バックアップを復元することができません。 
 
 
次の例では、証明書を作成し、証明書によって保護されているバックアップを作成します。

```
USE master;  
GO  
CREATE CERTIFICATE BackupEncryptCert   
   WITH SUBJECT = 'Database backups';  
GO 
BACKUP DATABASE [AdventureWorks2014]  
TO DISK = N'/var/opt/mssql/backups/AdventureWorks2014.bak'  
WITH  
  COMPRESSION,  
  ENCRYPTION   
   (  
   ALGORITHM = AES_256,  
   SERVER CERTIFICATE = BackupEncryptCert  
   ),  
  STATS = 10  
GO  
```

詳細については、「 [バックアップの暗号化](../relational-databases/backup-restore/backup-encryption.md)」をご覧ください。


## <a name="next-steps"></a>次のステップ

SQL Server のセキュリティ機能の詳細については、「[SQL Server データベース エンジンと Azure SQL Database のセキュリティ センター](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)」を参照してください。