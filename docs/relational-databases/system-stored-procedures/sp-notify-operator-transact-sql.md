---
description: sp_notify_operator (Transact-SQL)
title: sp_notify_operator (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_notify_operator_TSQL
- sp_notify_operator
dev_langs:
- TSQL
helpviewer_keywords:
- sp_notify_operator
ms.assetid: c440f5c9-9884-4196-b07c-55d87afb17c3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 946a2adf54435499ae72d12ed10e984892295533
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541635"
---
# <a name="sp_notify_operator-transact-sql"></a>sp_notify_operator (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベースメールを使用して、オペレーターに電子メールメッセージを送信します。  
  
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_notify_operator  
    [ @profile_name = ] 'profilename' ,  
    [ @id = ] id ,  
    [ @name = ] 'name' ,  
    [ @subject = ] 'subject' ,  
    [ @body = ] 'message' ,  
    [ @file_attachments = ] 'attachment'  
    [ @mail_database = ] 'mail_host_database'  
```  
  
## <a name="arguments"></a>引数  
`[ @profile_name = ] 'profilename'` メッセージの送信に使用するデータベースメールプロファイルの名前。 *profilename* は **nvarchar (128)** です。 *Profilename*が指定されていない場合は、既定のデータベースメールプロファイルが使用されます。  
  
`[ @id = ] id` メッセージの送信先となるオペレーターの識別子。 *id* は **int**,、既定値は NULL です。 *Id*または*名前*のいずれかを指定する必要があります。  
  
`[ @name = ] 'name'` メッセージを送信するオペレーターの名前。 *名前* は **nvarchar (128)**,、既定値は NULL です。 *Id*または*名前*のいずれかを指定する必要があります。  
  
> **注:** メッセージを受信するには、オペレーターの電子メールアドレスを定義しておく必要があります。  
  
`[ @subject = ] 'subject'` 電子メールメッセージの件名。 *サブジェクト* は **nvarchar (256)** で、既定値はありません。  
  
`[ @body = ] 'message'` 電子メールメッセージの本文。 *メッセージ* は **nvarchar (max)** で、既定値はありません。  
  
`[ @file_attachments = ] 'attachment'` 電子メールメッセージに添付するファイルの名前。 *添付ファイル* は **nvarchar (512)**,、既定値はありません。  
  
`[ @mail_database = ] 'mail_host_database'` メールホストデータベースの名前を指定します。 *mail_host_database* は **nvarchar (128)** です。 *Mail_host_database*が指定されていない場合、既定では**msdb**データベースが使用されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 ここでは、指定したメッセージが、指定したオペレーターの電子メール アドレスに送信されます。 オペレーターに電子メール アドレスが構成されていない場合、エラーが返されます。  
  
 通知をオペレーターに送信する前に、データベースメールとメールホストデータベースを構成する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、 **sysadmin** 固定サーバーロールのメンバーは、このストアドプロシージャを実行できます。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
## <a name="examples"></a>例  
 次の例では、データベース メール プロファイル `François Ajenstat` を使用して、電子メールをオペレーター `AdventureWorks Administrator` に送信します。 電子メールの件名は `Test Notification` です。 電子メール メッセージには、"This is a test of notification via e-mail." という文が記載されています。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_notify_operator  
   @profile_name = N'AdventureWorks Administrator',  
   @name = N'François Ajenstat',  
   @subject = N'Test Notification',  
   @body = N'This is a test of notification via e-mail.' ;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [Transact-sql&#41;&#40;のストアドプロシージャの SQL Server エージェント ](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_operator &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_help_operator &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [sp_delete_operator &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)  
  
  
