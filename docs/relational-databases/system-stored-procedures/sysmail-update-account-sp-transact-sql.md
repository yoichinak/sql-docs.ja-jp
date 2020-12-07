---
description: sysmail_update_account_sp (Transact-SQL)
title: sysmail_update_account_sp (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_account_sp
- sysmail_update_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_account_sp
ms.assetid: ba2fdccc-5ed4-40ef-a479-79497b4d61aa
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: fe446ee69a7bf3f7ac6600b2cb521f4f9d89ffa1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485525"
---
# <a name="sysmail_update_account_sp-transact-sql"></a>sysmail_update_account_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  既存のデータベース メール アカウントの情報を変更します。  
 
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_update_account_sp [ [ @account_id = ] account_id ] [ , ] [ [ @account_name = ] 'account_name' ] ,  
    [ @email_address = ] 'email_address' ,   
    [ @display_name = ] 'display_name' ,   
    [ @replyto_address = ] 'replyto_address' ,  
    [ @description = ] 'description' ,   
    [ @mailserver_name = ] 'server_name' ,   
    [ @mailserver_type = ] 'server_type' ,   
    [ @port = ] port_number ,   
    [ @timeout = ] 'timeout' ,  
    [ @username = ] 'username' ,  
    [ @password = ] 'password' ,  
    [ @use_default_credentials = ] use_default_credentials ,  
    [ @enable_ssl = ] enable_ssl   
```  
  
## <a name="arguments"></a>引数  
`[ @account_id = ] account_id` 更新するアカウント ID。 *account_id* は **int**,、既定値は NULL です。 少なくとも1つの *account_id* または *account_name* を指定する必要があります。 両方が指定されている場合、プロシージャはアカウントの名前を変更します。  
  
`[ @account_name = ] 'account_name'` 更新するアカウントの名前。 *account_name* は **sysname**,、既定値は NULL です。 少なくとも1つの *account_id* または *account_name* を指定する必要があります。 両方が指定されている場合、プロシージャはアカウントの名前を変更します。  
  
`[ @email_address = ] 'email_address'` メッセージの送信先となる新しい電子メールアドレス。 このアドレスは、インターネット電子メールアドレスである必要があります。 アドレスのサーバー名は、このアカウントからメールを送信するためにデータベースメール使用するサーバーです。 *email_address* は **nvarchar (128)**,、既定値は NULL です。  
  
`[ @display_name = ] 'display_name'` このアカウントからの電子メールメッセージに使用する新しい表示名。 *display_name* は **nvarchar (128)**,、既定値はありません。  
  
`[ @replyto_address = ] 'replyto_address'` このアカウントからの電子メールメッセージの返信先ヘッダーで使用する新しいアドレス。 *replyto_address* は **nvarchar (128)**,、既定値はありません。  
  
`[ @description = ] 'description'` アカウントの新しい説明。 *説明* は **nvarchar (256)**,、既定値は NULL です。  
  
`[ @mailserver_name = ] 'server_name'` このアカウントに使用する SMTP メールサーバーの新しい名前を指定します。 を実行するコンピューターは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *SERVER_NAME* を IP アドレスに解決できる必要があります。 *server_name* は **sysname**であり、既定値はありません。  
  
`[ @mailserver_type = ] 'server_type'` メールサーバーの新しい種類。 *server_type* は **sysname**であり、既定値はありません。 **' SMTP '** の値のみがサポートされています。  
  
`[ @port = ] port_number` メールサーバーの新しいポート番号。 *port_number* は **int**,、既定値はありません。  
  
`[ @timeout = ] 'timeout'` SmtpClient のタイムアウトパラメーター。1つの電子メールメッセージを送信します。 *タイムアウト* は秒単位の **int** で、既定値はありません。  
  
`[ @username = ] 'username'` メールサーバーへのログオンに使用する新しいユーザー名を指定します。 *ユーザー名* は **sysname**で、既定値はありません。  
  
`[ @password = ] 'password'` メールサーバーへのログオンに使用する新しいパスワード。 *パスワード* は **sysname**,、既定値はありません。  
  
`[ @use_default_credentials = ] use_default_credentials` サービスの資格情報を使用して SMTP サーバーにメールを送信するかどうかを指定し [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ます。 **use_default_credentials** はビット,、既定値はありません。 このパラメーターが1の場合、データベースメールはの資格情報を使用し [!INCLUDE[ssDE](../../includes/ssde-md.md)] ます。 このパラメーターが0の場合、データベースメールは、SMTP サーバーの認証に** \@ ユーザー名**と** \@ パスワード**を使用します。 ** \@ ユーザー名**と** \@ パスワード**が NULL の場合は、匿名認証が使用されます。 このパラメーターを指定する前に、SMTP 管理者に相談してください。  
  
`[ @enable_ssl = ] enable_ssl` データベースメールトランスポート層セキュリティ (TLS) を使用して通信を暗号化するかどうかを指定します。これは、以前 Secure Sockets Layer (SSL) と呼ばれていました。 このオプションは、SMTP サーバーで TLS が必要な場合に使用します。 **enable_ssl** はビット,、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 アカウント名とアカウント id の両方を指定すると、アカウントの情報を更新するだけでなく、アカウント名も変更されます。 アカウント名の変更は、アカウント名のエラーを修正する場合に利用できます。  
  
 ストアドプロシージャ **sysmail_update_account_sp** は **msdb** データベースにあり、 **dbo** スキーマが所有しています。 現在のデータベースが **msdb**でない場合は、3つの部分で構成される名前を使用してプロシージャを実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-changing-the-information-for-an-account"></a>A. アカウントの情報を変更する  
 次の例では、msdb データベースのアカウントを更新し `AdventureWorks Administrator` ます。 **msdb** アカウントの情報は、指定された値に設定されます。  
  
```  
EXECUTE msdb.dbo.sysmail_update_account_sp  
     @account_name = 'AdventureWorks Administrator'  
    ,@description = 'Mail account for administrative e-mail.'  
    ,@email_address = 'dba@Adventure-Works.com'  
    ,@display_name = 'AdventureWorks Automated Mailer'  
    ,@replyto_address = NULL  
    ,@mailserver_name = 'smtp.Adventure-Works.com'  
    ,@mailserver_type = 'SMTP'  
    ,@port = 25  
    ,@timeout = 60  
    ,@username = NULL  
    ,@password = NULL  
    ,@use_default_credentials = 0  
    ,@enable_ssl = 0;  
```  
  
### <a name="b-changing-the-name-of-an-account-and-the-information-for-an-account"></a>B. アカウントの名前とアカウントの情報を変更する  
 次の例では、アカウント ID `125` の名前を変更し、アカウント情報を更新します。 アカウントの新しい名前は `Backup Mail Server` です。  
  
```  
EXECUTE msdb.dbo.sysmail_update_account_sp  
     @account_id = 125  
    ,@account_name = 'Backup Mail Server'  
    ,@description = 'Mail account for administrative e-mail.'  
    ,@email_address = 'dba@Adventure-Works.com'  
    ,@display_name = 'AdventureWorks Automated Mailer'  
    ,@replyto_address = NULL  
    ,@mailserver_name = 'smtp-backup.Adventure-Works.com'  
    ,@mailserver_type = 'SMTP'  
    ,@port = 25  
    ,@timeout = 60  
    ,@username = NULL  
    ,@password = NULL  
    ,@use_default_credentials = 0  
    ,@enable_ssl = 0;  
```  
  
## <a name="see-also"></a>参照  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [データベースメールアカウントを作成する](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースメール ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
