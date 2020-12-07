---
description: sysmail_add_profileaccount_sp (Transact-SQL)
title: sysmail_add_profileaccount_sp (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_profileaccount_sp
- sysmail_add_profileaccount_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_profileaccount_sp
ms.assetid: 7cbf430f-1997-45ea-9707-0086184de744
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 209240de58b09e48c4d35f145640f1edf97f1c4a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538538"
---
# <a name="sysmail_add_profileaccount_sp-transact-sql"></a>sysmail_add_profileaccount_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベースメールプロファイルにデータベースメールアカウントを追加します。 [Sysmail_add_account_sp &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sysmail-add-account-sp-transact-sql.md)を使用してデータベースアカウントを作成した後、 **sysmail_add_profileaccount_sp**を実行します。 [transact-sql sysmail_add_profile_sp ](../../relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql.md)&#40;を使用してデータベースプロファイルが作成されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_add_profileaccount_sp { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    { [ @account_id = ] account_id | [ @account_name = ] 'account_name' }  
    [ , [ @sequence_number = ] sequence_number ]  
```  
  
## <a name="arguments"></a>引数  
`[ @profile_id = ] profile_id` アカウントを追加するプロファイル id。 *profile_id* は **int**,、既定値は NULL です。 *Profile_id*または*profile_name*のいずれかを指定する必要があります。  
  
`[ @profile_name = ] 'profile_name'` アカウントを追加するプロファイル名を指定します。 *profile_name* は **sysname**,、既定値は NULL です。 *Profile_id*または*profile_name*のいずれかを指定する必要があります。  
  
`[ @account_id = ] account_id` プロファイルに追加するアカウント id。 *account_id* は **int**,、既定値は NULL です。 *Account_id*または*account_name*のいずれかを指定する必要があります。  
  
`[ @account_name = ] 'account_name'` プロファイルに追加するアカウントの名前。 *account_name* は **sysname**,、既定値は NULL です。 *Account_id*または*account_name*のいずれかを指定する必要があります。  
  
`[ @sequence_number = ] sequence_number` プロファイル内のアカウントのシーケンス番号。 *sequence_number* は **int**,、既定値はありません。 シーケンス番号によって、プロファイルで使用されるアカウントの順序が決まります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 プロファイルとアカウントの両方が既に存在している必要があります。 両方またはいずれかが存在しないと、このストアド プロシージャはエラーを返します。  
  
 このストアドプロシージャは、指定されたプロファイルに既に関連付けられているアカウントのシーケンス番号を変更しないことに注意してください。 アカウントのシーケンス番号の更新の詳細については、「 [sysmail_update_profileaccount_sp &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sysmail-update-profileaccount-sp-transact-sql.md)」を参照してください。  
  
 シーケンス番号によって、データベース メールではプロファイル内のアカウントがどの順番で使用されるかが決まります。 新しい電子メール メッセージの場合、データベース メールでは、一番小さなシーケンス番号の付いたアカウントから処理が開始されます。 そのアカウントが失敗すると、データベース メールでは、このアカウントよりも大きいシーケンス番号を持つアカウントに処理が移ります。このように、データベース メールによってメッセージが正常に送信されるか、一番大きなシーケンス番号のアカウントが失敗するまで順に処理されます。 最も番号が大きいアカウントで失敗した場合、 *sysmail_configure_sp* の **AccountRetryDelay**パラメーターで構成した時間、メールの送信が一時停止されます。その後、最も番号が小さいアカウントからメールの送信プロセスが再開されます。 *sysmail_configure_sp* の **AccountRetryAttempts**パラメーターは、指定されたプロファイルの各アカウントを使用して外部メール プロセスが電子メール メッセージを送信する回数を構成します。  
  
 同じシーケンス番号を持つアカウントが複数存在する場合、データベースメールは、指定された電子メールメッセージに対してこれらのアカウントのいずれかのみを使用します。 この場合、そのシーケンス番号に対してどのアカウントが使用されるか、またメッセージごとに同じアカウントが使用されるかついては、データベース メールでは保証されません。  
  
 ストアドプロシージャ **sysmail_add_profileaccount_sp** は **msdb** データベースにあり、 **dbo** スキーマが所有しています。 現在のデータベースが **msdb**でない場合は、3つの部分で構成される名前を使用してプロシージャを実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの実行権限は、既定では **sysadmin** 固定サーバーロールのメンバーに与えています。  
  
## <a name="examples"></a>例  
 次の例では、プロファイルを `AdventureWorks Administrator` アカウントに関連付け `Audit Account` ます。 監査アカウントのシーケンス番号は1です。  
  
```  
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator',  
    @account_name = 'Audit Account',  
    @sequence_number = 1 ;  
```  
  
## <a name="see-also"></a>参照  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [データベースメールアカウントを作成する](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [データベースメール構成オブジェクト](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースメール ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
