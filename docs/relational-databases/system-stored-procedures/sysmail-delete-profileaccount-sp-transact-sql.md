---
description: sysmail_delete_profileaccount_sp (Transact-SQL)
title: sysmail_delete_profileaccount_sp (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_profileaccount_sp
- sysmail_delete_profileaccount_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_profileaccount_sp
ms.assetid: b58d06f2-d6c9-4c8e-95bd-027c50f4621a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d5cc2643440544a3b1e65bc6fbb07df0b95e5594
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89525759"
---
# <a name="sysmail_delete_profileaccount_sp-transact-sql"></a>sysmail_delete_profileaccount_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベース メール プロファイルからアカウントを削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_delete_profileaccount_sp  {   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    {   [ @account_id = ] account_id | [ @account_name = ] 'account_name' }  
```  
  
## <a name="arguments"></a>引数  
`[ @profile_id = ] profile_id` 削除するプロファイルのプロファイル ID。 *profile_id* は **int**,、既定値は NULL です。 *Profile_id*または*profile_name*のいずれかを指定できます。  
  
`[ @profile_name = ] 'profile_name'` 削除するプロファイルのプロファイル名を指定します。 *profile_name* は **sysname**,、既定値は NULL です。 *Profile_id*または*profile_name*のいずれかを指定できます。  
  
`[ @account_id = ] account_id` 削除するアカウント ID。 *account_id* は **int**,、既定値は NULL です。 *Account_id*または*account_name*のいずれかを指定できます。  
  
`[ @account_name = ] 'account_name'` 削除するアカウントの名前を指定します。 *account_name* は **sysname**,、既定値は NULL です。 *Account_id*または*account_name*のいずれかを指定できます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 指定されたアカウントが、指定されたプロファイルに関連付けられていない場合、エラーを返します。  
  
 アカウントを指定し、プロファイルを指定しなかった場合、このストアド プロシージャでは指定したアカウントがすべてのプロファイルから削除されます。 たとえば、既存の SMTP サーバーをシャットダウンする前に、その SMTP サーバーを使用しているアカウントを各プロファイルから個別に削除するのではなく、すべてのプロファイルからまとめて削除できます。  
  
 プロファイルを指定し、アカウントを指定しなかった場合、このストアド プロシージャでは指定したプロファイルからすべてのアカウントが削除されます。 たとえば、プロファイルで使用する SMTP サーバーを変更する場合は、プロファイルからすべてのアカウントを削除し、必要に応じて新しいアカウントを追加すると便利な場合があります。  
  
 ストアドプロシージャ **sysmail_delete_profileaccount_sp** は **msdb** データベースにあり、 **dbo** スキーマが所有しています。 現在のデータベースが **msdb**でない場合は、3つの部分で構成される名前を使用してプロシージャを実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの実行権限は、既定では **sysadmin** 固定サーバーロールのメンバーに与えています。  
  
## <a name="examples"></a>例  
 次の例では、プロファイルの `Audit Account` からアカウントの `AdventureWorks Administrator` を削除します。  
  
```  
EXECUTE msdb.dbo.sysmail_delete_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator',  
    @account_name = 'Audit Account' ;  
```  
  
## <a name="see-also"></a>参照  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [データベースメールアカウントを作成する](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [データベースメール構成オブジェクト](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースメール ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
