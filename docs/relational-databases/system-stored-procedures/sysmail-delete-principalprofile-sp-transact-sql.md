---
description: sysmail_delete_principalprofile_sp (Transact-SQL)
title: sysmail_delete_principalprofile_sp (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_principalprofile_sp_TSQL
- sysmail_delete_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_principalprofile_sp
ms.assetid: 8fc14700-e17a-4073-9a96-7fc23e775c69
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e5cfe34ff4bebc2e21517e6515b5ea2ebee3a37f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538492"
---
# <a name="sysmail_delete_principalprofile_sp-transact-sql"></a>sysmail_delete_principalprofile_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベースのユーザーやロールから、パブリックまたはプライベートなデータベース メール プロファイルを使用する権限を削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_delete_principalprofile_sp  { [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
```  
  
## <a name="arguments"></a>引数  
`[ @principal_id = ] principal_id` 関連付けを削除する **msdb** データベースのデータベースユーザーまたはロールの ID を示します。 *principal_id* は **int**,、既定値は NULL です。 パブリックプロファイルをプライベートプロファイルにするには、プリンシパル ID **0** またはプリンシパル名 **' public '** を指定します。 *Principal_id*または*principal_name*のいずれかを指定する必要があります。  
  
`[ @principal_name = ] 'principal_name'` 関連付けを削除する **msdb** データベースのデータベースユーザーまたはロールの名前を指定します。 *principal_name* は **sysname**,、既定値は NULL です。 パブリックプロファイルをプライベートプロファイルにするには、プリンシパル ID **0** またはプリンシパル名 **' public '** を指定します。 *Principal_id*または*principal_name*のいずれかを指定する必要があります。  
  
`[ @profile_id = ] profile_id` 関連付けを削除するプロファイルの ID を示します。 *profile_id* は **int**,、既定値は NULL です。 *Profile_id*または*profile_name*のいずれかを指定する必要があります。  
  
`[ @profile_name = ] 'profile_name'` 関連付けを削除するプロファイルの名前を指定します。 *profile_name* は **sysname**,、既定値は NULL です。 *Profile_id*または*profile_name*のいずれかを指定する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 パブリックプロファイルをプライベートプロファイルにするには、プリンシパル名に **' public '** を指定するか、プリンシパル id に **0** を指定します。  
  
 ユーザーの既定のプライベート プロファイルや、既定のパブリック プロファイルを削除する場合は慎重に行ってください。 既定のプロファイルが使用できない場合、 **sp_send_dbmail** にはプロファイルの名前を引数として指定する必要があります。 したがって、既定のプロファイルを削除すると、 **sp_send_dbmail** の呼び出しが失敗する可能性があります。 詳細については、「 [sp_send_dbmail &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)」を参照してください。  
  
 ストアドプロシージャ **sysmail_delete_principalprofile_sp** は **msdb** データベースにあり、 **dbo** スキーマが所有しています。 現在のデータベースが **msdb**でない場合は、3つの部分で構成される名前を使用してプロシージャを実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの実行権限は、既定では **sysadmin** 固定サーバーロールのメンバーに与えています。  
  
## <a name="examples"></a>例  
 次の例では、 **msdb**データベースの Profile **AdventureWorks Administrator**と login **applicationuser**の関連付けを削除しています。  
  
```  
EXECUTE msdb.dbo.sysmail_delete_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
## <a name="see-also"></a>参照  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [データベースメール構成オブジェクト](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースメール ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
