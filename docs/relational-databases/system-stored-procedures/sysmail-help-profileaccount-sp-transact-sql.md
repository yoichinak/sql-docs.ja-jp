---
description: sysmail_help_profileaccount_sp (Transact-SQL)
title: sysmail_help_profileaccount_sp (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_profileaccount_sp_TSQL
- sysmail_help_profileaccount_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_profileaccount_sp
ms.assetid: 3ea68271-0a6b-4d77-991c-4757f48f747a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6894b44d7a09fa8f49ffa1d76a8613f930db7d18
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541073"
---
# <a name="sysmail_help_profileaccount_sp-transact-sql"></a>sysmail_help_profileaccount_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  1 つ以上のデータベース メール プロファイルに関連付けられているアカウントを一覧表示します。  
    
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_help_profileaccount_sp  
   {   [ @profile_id = ] profile_id   
      | [ @profile_name = ] 'profile_name' }  
   [ , {   [ @account_id = ] account_id  
         | [ @account_name = ] 'account_name' } ]  
```  
  
## <a name="arguments"></a>引数  
`[ @profile_id = ] profile_id` 一覧表示するプロファイルのプロファイル ID を示します。 *profile_id* は **int**,、既定値は NULL です。 *Profile_id*または*profile_name*のいずれかを指定する必要があります。  
  
`[ @profile_name = ] 'profile_name'` 一覧表示するプロファイルのプロファイル名を指定します。 *profile_name* は **sysname**,、既定値は NULL です。 *Profile_id*または*profile_name*のいずれかを指定する必要があります。  
  
`[ @account_id = ] account_id` 一覧表示するアカウント ID を示します。 *account_id* は **int**,、既定値は NULL です。 *Account_id*と*account_name*が両方とも NULL の場合、はプロファイル内のすべてのアカウントを一覧表示します。  
  
`[ @account_name = ] 'account_name'` 一覧表示するアカウントの名前を指定します。 *account_name* は **sysname**,、既定値は NULL です。 *Account_id*と*account_name*が両方とも NULL の場合、はプロファイル内のすべてのアカウントを一覧表示します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 次の列を含む結果セットが返されます。  
  
| 列名 | データ型 | 説明 |
| ----------- | --------- | ----------- |
|**profile_id**|**int**|プロファイルのプロファイル ID。|  
|**profile_name**|**sysname**|プロファイルの名前。|  
|**account_id**|**int**|アカウントのアカウント ID。|  
|**account_name**|**sysname**|アカウントの名前。|  
|**sequence_number**|**int**|プロファイル内のアカウントのシーケンス番号。|  
  
## <a name="remarks"></a>解説  
 *Profile_id*または*profile_name*が指定されていない場合、このストアドプロシージャは、インスタンス内のすべてのプロファイルに関する情報を返します。  
  
 ストアドプロシージャ **sysmail_help_profileaccount_sp** は **msdb** データベースにあり、 **dbo** スキーマが所有しています。 現在のデータベースが **msdb**でない場合は、3つの部分で構成される名前を使用してプロシージャを実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの実行権限は、既定では **sysadmin** 固定サーバーロールのメンバーに与えています。  
  
## <a name="examples"></a>例  
 **A. 特定のプロファイルのアカウントを名前順に一覧表示する**  
  
 次の例では、プロファイル名を指定して、プロファイルの情報を一覧表示し `AdventureWorks Administrator` ます。  
  
```  
EXECUTE msdb.dbo.sysmail_help_profileaccount_sp  
   @profile_name = 'AdventureWorks Administrator';  
```  
  
 次に結果セットを示します。行の長さは編集されています。  
  
```  
profile_id  profile_name                 account_id  account_name         sequence_number  
----------- ---------------------------- ----------- -------------------- ---------------  
131         AdventureWorks Administrator 197         Admin-MainServer     1  
131         AdventureWorks Administrator 198         Admin-BackupServer   2  
```  
  
 **B. 特定のプロファイルのアカウントをプロファイル ID 順に一覧表示する**  
  
 次の例では、`AdventureWorks Administrator` プロファイルの情報を、プロファイル ID を指定して一覧表示します。  
  
```  
EXECUTE msdb.dbo.sysmail_help_profileaccount_sp  
    @profile_id = 131 ;  
```  
  
 次に結果セットを示します。行の長さは編集されています。  
  
```  
profile_id  profile_name                 account_id  account_name         sequence_number  
----------- ---------------------------- ----------- -------------------- ---------------  
131         AdventureWorks Administrator 197         Admin-MainServer     1  
131         AdventureWorks Administrator 198         Admin-BackupServer   2  
```  
  
 **C. すべてのプロファイルのアカウントを一覧表示する**  
  
 次の例では、インスタンス内のすべてのプロファイルのアカウントを一覧表示します。  
  
```  
EXECUTE msdb.dbo.sysmail_help_profileaccount_sp;  
```  
  
 次に結果セットを示します。行の長さは編集されています。  
  
```  
profile_id  profile_name                 account_id  account_name         sequence_number  
----------- ---------------------------- ----------- -------------------- ---------------  
131         AdventureWorks Administrator 197         Admin-MainServer     1  
131         AdventureWorks Administrator 198         Admin-BackupServer   2  
106         AdventureWorks Operator      210         Operator-MainServer  1  
```  
  
## <a name="see-also"></a>参照  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [データベースメールアカウントを作成する](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [データベースメール構成オブジェクト](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースメール ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
