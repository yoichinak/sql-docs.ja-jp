---
description: sp_control_dbmasterkey_password (Transact-SQL)
title: sp_control_dbmasterkey_password (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 04/09/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_control_dbmasterkey_password
- sp_control_dbmasterkey_password_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_control_dbmasterkey_password
ms.assetid: 63979a87-42a2-446e-8e43-30481faaf3ca
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 08b749ad756a47ed991acd1ad0ea1d533bbb770c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481451"
---
# <a name="sp_control_dbmasterkey_password-transact-sql"></a>sp_control_dbmasterkey_password (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  データベースマスターキーを開くために必要なパスワードを含む資格情報を追加または削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_control_dbmasterkey_password @db_name = 'database_name,  
     @password = 'master_key_password' , @action = { 'add' | 'drop' }  
```  
  
## <a name="arguments"></a>引数  
 @db_name= N '*database_name*'  
 この資格情報に関連付けられているデータベースの名前を指定します。 システムデータベースを指定することはできません。 *database_name* は **nvarchar**です。  
  
 @password= N '*パスワード*'  
 マスター キーのパスワードを指定します。 *パスワード* は **nvarchar**です。  
  
 @action= N'add '  
 指定したデータベースの資格情報を、資格情報ストアに追加します。 資格情報には、データベースマスターキーのパスワードが含まれます。 に渡される値 @action は **nvarchar**です。  
  
 @action= N'drop '  
 指定されたデータベースの資格情報が資格情報ストアから削除されることを指定します。 に渡される値 @action は **nvarchar**です。  
  
## <a name="remarks"></a>解説  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、キーの暗号化解除や暗号化にデータベースのマスター キーが必要となる場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではインスタンスのサービス マスター キーを使用して、データベースのマスター キーの暗号化解除が試行されます。 暗号化解除が失敗した場合、は、マスターキーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必要なデータベースと同じファミリ GUID を持つマスターキー資格情報を資格情報ストアで検索します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、次に、一致した資格情報を順に使用してデータベースのマスター キーの暗号化解除が試行されます。これは暗号化解除が成功するか、資格情報がなくなった時点で終了します。  
  
> [!CAUTION]  
>  sa やその他の高位の権限を持つサーバー プリンシパルに対してデータベースへのアクセスを禁止する場合は、データベースのマスター キー資格情報を作成しないでください。 データベースのキー階層をサービス マスター キーで暗号化解除できないようにデータベースを構成できます。 この機能は、sa または高位の権限を持つサーバー プリンシパルに対して、データベースに含まれる暗号化情報へのアクセスを禁止するための、多重の防御としてサポートされているものです。 このようなデータベースに対してマスター キー資格情報を作成すると、この多重の防御が無効になり、sa およびその他の高位の権限を持つサーバー プリンシパルがデータベースの暗号化を解除できるようになります。  
  
 Sp_control_dbmasterkey_password を使用して作成された資格情報は、 [master_key_passwords](../../relational-databases/system-catalog-views/sys-master-key-passwords-transact-sql.md) カタログビューに表示されます。 データベースのマスターキーに対して作成される資格情報の名前は、の形式に `##DBMKEY_<database_family_guid>_<random_password_guid>##` なります。 パスワードは、資格情報のシークレットとして保存されます。 sys.credentials には、資格情報ストアに追加されたパスワードごとに 1 行のデータが格納されます。  
  
 sp_control_dbmasterkey_password を使用して、システム データベース master、model、msdb、または tempdb の資格情報を作成することはできません。  
  
 sp_control_dbmasterkey_password では、指定したデータベースのマスター キーをパスワードで開くことができるかどうかは検証されません。  
  
 指定したデータベースの資格情報に既に格納されているパスワードを指定した場合、sp_control_dbmasterkey_password は失敗します。  
  
> [!NOTE]  
>  異なるサーバー インスタンスの 2 つのデータベースで、同じファミリ GUID を共有することができます。 この場合、両方のデータベースの資格情報ストア内で同じマスター キー レコードが共有されます。  
  
 sp_control_dbmasterkey_password に渡されるパラメーターは、トレースには表示されません。  
  
> [!NOTE]  
>  sp_control_dbmasterkey_password を使用して追加された資格情報を使ってデータベース マスター キーを開く場合、そのデータベース マスター キーはサービス マスター キーによって再暗号化されます。 データベースが読み取り専用モードの場合、再暗号化操作は失敗し、データベースマスターキーは暗号化されずに残ります。 その後、データベースマスターキーにアクセスするには、OPEN MASTER KEY ステートメントとパスワードを使用する必要があります。 パスワードの使用を避けるには、データベースを読み取り専用モードに移行する前に、資格情報を作成するようにしてください。  
  
 **潜在的な旧バージョンとの互換性の問題:** 現在、ストアドプロシージャでは、マスターキーが存在するかどうかは確認されません。 これは下位互換性を確保するために許容されていますが、警告が表示されます。 ただし、この動作は非推奨とされます。 今後のリリースでは、マスターキーが存在する必要があります。また、ストアドプロシージャ **sp_control_dbmasterkey_password** で使用されるパスワードは、データベースマスターキーの暗号化に使用されるパスワードと同じパスワードにする必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-creating-a-credential-for-the-adventureworks2012-master-key"></a>A. AdventureWorks2012 マスターキーの資格情報を作成しています  
 次の例では、`AdventureWorks2012` データベースのマスター キーの資格情報を作成し、マスター キーのパスワードをシークレットとして資格情報に保存します。 に渡されるすべて `sp_control_dbmasterkey_password` のパラメーターのデータ型は **nvarchar**である必要があるため、テキスト文字列はキャスト演算子で変換され `N` ます。  
  
```  
EXEC sp_control_dbmasterkey_password @db_name = N'AdventureWorks2012',   
    @password = N'sdfjlkj#mM00sdfdsf98093258jJlfdk4', @action = N'add';  
GO  
```  
  
### <a name="b-dropping-a-credential-for-a-database-master-key"></a>B. データベースのマスター キーの資格情報を削除する  
 次の例では、例 A で作成した資格情報を削除します。パスワードを含め、すべてのパラメーターが必要であることに注意してください。  
  
```  
EXEC sp_control_dbmasterkey_password @db_name = N'AdventureWorks2012',   
    @password = N'sdfjlkj#mM00sdfdsf98093258jJlfdk4', @action = N'drop';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [暗号化されたミラーデータベースを設定する](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)   
 [セキュリティストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [システムストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [資格情報 &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)  
  
  
