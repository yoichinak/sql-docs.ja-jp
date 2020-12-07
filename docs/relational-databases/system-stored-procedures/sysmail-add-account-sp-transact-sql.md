---
description: sysmail_add_account_sp (Transact-SQL)
title: sysmail_add_account_sp (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_account_sp
- sysmail_add_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_account_sp
ms.assetid: 65e15e2e-107c-49c3-b12c-f4edf0eb1617
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 85625e9b8e5a3c1acf5bbc8152b90789f33665ff
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551102"
---
# <a name="sysmail_add_account_sp-transact-sql"></a>sysmail_add_account_sp (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  SMTP アカウントに関する情報を保持する新しいデータベースメールアカウントを作成します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_add_account_sp  [ @account_name = ] 'account_name',  
    [ @email_address = ] 'email_address' ,  
    [ [ @display_name = ] 'display_name' , ]  
    [ [ @replyto_address = ] 'replyto_address' , ]  
    [ [ @description = ] 'description' , ]  
    [ @mailserver_name = ] 'server_name'   
    [ , [ @mailserver_type = ] 'server_type' ]  
    [ , [ @port = ] port_number ]  
    [ , [ @username = ] 'username' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @use_default_credentials = ] use_default_credentials ]  
    [ , [ @enable_ssl = ] enable_ssl ]  
    [ , [ @account_id = ] account_id OUTPUT ]  
```  
  
## <a name="arguments"></a>引数  
`[ @account_name = ] 'account_name'` 追加するアカウントの名前。 *account_name* は **sysname**であり、既定値はありません。  
  
`[ @email_address = ] 'email_address'` メッセージの送信元の電子メールアドレス。 このアドレスは、インターネット電子メールアドレスである必要があります。 *email_address* は **nvarchar (128)**,、既定値はありません。 たとえば、エージェントのアカウントは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SqlAgent \@ Adventure-Works.com**のアドレスから電子メールを送信できます。  
  
`[ @display_name = ] 'display_name'` このアカウントからの電子メールメッセージに使用する表示名。 *display_name* は **nvarchar (128)**,、既定値は NULL です。 たとえば、エージェントのアカウントには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電子メールメッセージに **自動メーラー SQL Server エージェント** 名前が表示される場合があります。  
  
`[ @replyto_address = ] 'replyto_address'` このアカウントからのメッセージに対する応答の送信先アドレス。 *replyto_address* は **nvarchar (128)**,、既定値は NULL です。 たとえば、エージェントのアカウントへの返信は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース管理者 **danw \@ Adventure-Works.com**に送られます。  
  
`[ @description = ] 'description'` アカウントの説明を示します。 *説明* は **nvarchar (256)**,、既定値は NULL です。  
  
`[ @mailserver_name = ] 'server_name'` このアカウントに使用する SMTP メールサーバーの名前または IP アドレスを指定します。 を実行するコンピューターは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *SERVER_NAME* を IP アドレスに解決できる必要があります。 *server_name* は **sysname**であり、既定値はありません。  
  
`[ @mailserver_type = ] 'server_type'` 電子メールサーバーの種類。 *server_type* は **sysname**で、既定値は **' SMTP '** です。  
  
`[ @port = ] port_number` 電子メールサーバーのポート番号。 *port_number* は **int**,、既定値は25です。  
  
`[ @username = ] 'username'` 電子メールサーバーへのログオンに使用するユーザー名を指定します。 *username* は **nvarchar (128)**,、既定値は NULL です。 このパラメーターが NULL の場合、データベースメールはこのアカウントに対して認証を使用しません。 メールサーバーで認証を必要としない場合は、ユーザー名に NULL を使用します。  
  
`[ @password = ] 'password'` 電子メールサーバーへのログオンに使用するパスワードです。 *パスワード* は **nvarchar (128)**,、既定値は NULL です。 ユーザー名を指定しない限り、パスワードを入力する必要はありません。  
  
`[ @use_default_credentials = ] use_default_credentials` の資格情報を使用して SMTP サーバーにメールを送信するかどうかを指定し [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ます。 **use_default_credentials** はビット,、既定値は0です。 このパラメーターが1の場合、データベースメールはの資格情報を使用し [!INCLUDE[ssDE](../../includes/ssde-md.md)] ます。 このパラメーターが0の場合、データベースメールは** \@ ユーザー名**と** \@ パスワード**パラメーターが存在する場合はそれを送信し、それ以外の場合は** \@ ユーザー名**と** \@ パスワード**のパラメーターを指定せずにメールを送信します。  
  
`[ @enable_ssl = ] enable_ssl` データベースメール Secure Sockets Layer を使用して通信を暗号化するかどうかを指定します。 **Enable_ssl** はビット,、既定値は0です。  
  
`[ @account_id = ] account_id OUTPUT` 新しいアカウントのアカウント id を返します。 *account_id* は **int**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 データベースメールには、 ** \@ email_address**、 ** \@ display_name**、および** \@ replyto_address**に個別のパラメーターが用意されています。 ** \@ Email_address**パラメーターは、メッセージの送信元のアドレスです。 ** \@ Display_name**パラメーターは、電子メールメッセージの [**差出人**] フィールドに表示される名前です。 ** \@ Replyto_address**パラメーターは、電子メールメッセージへの返信が送信されるアドレスです。 たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントで使用するアカウントでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントでのみ使用される電子メール アドレスから電子メール メッセージを送信できます。 そのアドレスからのメッセージにはフレンドリ名が表示されるので、受信者はエージェントがメッセージを送信したことを簡単に判断でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 受信者がメッセージに返信した場合、その返信は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントで使用されるアドレスではなくデータベース管理者に送られます。 このシナリオでは、アカウントは **SqlAgent@Adventure-Works.com** 電子メールアドレスとしてを使用します。 表示名は **SQL Server エージェント自動メーラ**に設定されます。 このアカウントは、 **danw@Adventure-Works.com** アドレスの返信としてを使用するので、このアカウントから送信されたメッセージへの返信は、エージェントの電子メールアドレスではなく、データベース管理者に送られ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 これら3つのパラメーターに個別の設定を指定することにより、データベースメールによって、必要に応じてメッセージを構成できます。  
  
 ** \@ Mailserver_type**パラメーターでは、値 **' SMTP '** がサポートされています。  
  
 ** \@ Use_default_credentials**が1の場合、メールはの資格情報を使用して SMTP サーバーに送信され [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ます。 ** \@ Use_default_credentials**が0で、 ** \@ ユーザー名**と** \@ パスワード**がアカウントに指定されている場合、アカウントは SMTP 認証を使用します。 ** \@ ユーザー名**と** \@ パスワード**は、アカウントが SMTP サーバーに使用する資格情報であり、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] またはコンピューターがあるネットワークの資格情報ではありません。  
  
 ストアドプロシージャ **sysmail_add_account_sp** は **msdb** データベースにあり、 **dbo** スキーマが所有しています。 現在のデータベースが **msdb**でない場合は、3つの部分で構成される名前を使用してプロシージャを実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの実行権限は、既定では **sysadmin** 固定サーバーロールのメンバーに与えています。  
  
## <a name="examples"></a>例  
 次の例では、という名前のアカウントを作成し `AdventureWorks Administrator` ます。 アカウントは電子メールアドレスを使用 `dba@Adventure-Works.com` し、SMTP メールサーバーにメールを送信し `smtp.Adventure-Works.com` ます。 このアカウントから送信された電子メールメッセージ `AdventureWorks Automated Mailer` は、メッセージの [ **差出人** ] 行に表示されます。 メッセージへの返信は `danw@Adventure-Works.com` に転送されます。  
  
```  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
```  
  
## <a name="see-also"></a>参照  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [データベースメールアカウントを作成する](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースメール ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
