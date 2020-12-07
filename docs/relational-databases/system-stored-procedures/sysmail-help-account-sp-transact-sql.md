---
description: sysmail_help_account_sp (Transact-SQL)
title: sysmail_help_account_sp (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_account_sp_TSQL
- sysmail_help_account_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_account_sp
ms.assetid: 87c7c39c-8e05-4e68-9272-45f908809c3b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 711b0d317b600b455fc4d3d0d80e17e1a9ddf7c3
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541054"
---
# <a name="sysmail_help_account_sp-transact-sql"></a>sysmail_help_account_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベース メール アカウントに関する、パスワード以外の情報を一覧表示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_help_account_sp [ [ @account_id = ] account_id | [ @account_name = ] 'account_name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @account_id = ] account_id` 情報を一覧表示するアカウントのアカウント ID。 *account_id* は **int**,、既定値は NULL です。  
  
`[ @account_name = ] 'account_name'` 情報を一覧表示するアカウントの名前。 *account_name* は **sysname**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 次に示す列を含む結果セットを返します。  
  
| 列名 | データ型 | 説明 |
| ----------- | --------- | ----------- |
|**account_id**|**int**|アカウントの ID。|  
|**name**|**sysname**|アカウントの名前。|  
|**description**|**nvarchar (256)**|アカウントの説明。|  
|**email_address**|**nvarchar(128)**|メッセージの送信元の電子メールアドレス。|  
|**display_name**|**nvarchar(128)**|アカウントの表示名。|  
|**replyto_address**|**nvarchar(128)**|このアカウントからのメッセージに対する返信アドレス。|  
|**servertype**|**sysname**|アカウントの電子メールサーバーの種類。|  
|**server**|**sysname**|アカウントの電子メールサーバーの名前。|  
|**port**|**int**|電子メールサーバーが使用するポート番号。|  
|**username**|**nvarchar(128)**|電子メールサーバーが認証を使用する場合は、電子メールサーバーへのサインインに使用するユーザー名。 **Username**が NULL の場合、データベースメールはこのアカウントに対して認証を使用しません。|  
|**use_default_credentials**|**bit**|の資格情報を使用して SMTP サーバーにメールを送信するかどうかを指定し [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ます。 **use_default_credentials** はビット,、既定値はありません。 このパラメーターが1の場合、データベースメールはサービスの資格情報を使用し [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ます。 このパラメーターが0の場合、データベースメールは、SMTP サーバーの認証に** \@ ユーザー名**と** \@ パスワード**を使用します。 ** \@ ユーザー名**と** \@ パスワード**が NULL の場合、データベースメールは匿名認証を使用します。 このパラメーターを指定する前に、SMTP 管理者に問い合わせてください。|  
|**enable_ssl**|**bit**|データベースメールトランスポート層セキュリティ (TLS) を使用して通信を暗号化するかどうかを指定します。これは、以前 Secure Sockets Layer (SSL) と呼ばれていました。 このオプションは、SMTP サーバーで TLS が必要な場合に使用します。 **enable_ssl** はビット,、既定値はありません。 1データベースメール TLS を使用して通信を暗号化することを示します。 0は、データベースメールが TLS 暗号化を使用せずにメールを送信することを示します。|  
  
## <a name="remarks"></a>解説  
 *Account_id*または*account_name*が指定されていない場合、 **sysmail_help_account**は、Microsoft SQL Server インスタンス内のすべてのデータベースメールアカウントに関する情報を一覧表示します。  
  
 ストアドプロシージャ **sysmail_help_account_sp** は **msdb** データベースにあり、 **dbo** スキーマが所有しています。 現在のデータベースが **msdb**でない場合は、3つの部分で構成される名前を使用してプロシージャを実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの実行権限は、既定では **sysadmin** 固定サーバーロールのメンバーに与えています。  
  
## <a name="examples"></a>例  
 **A. すべてのアカウントの情報を一覧表示する**  
  
 次の例では、インスタンス内のすべてのアカウントのアカウント情報を一覧表示します。  
  
```  
EXECUTE msdb.dbo.sysmail_help_account_sp ;  
```  
  
 次に結果セットを示します。行の長さは編集されています。  
  
```  
account_id  name                         description                             email_address             display_name                     replyto_address servertype servername                port        username use_default_credentials enable_ssl  
----------- ---------------------------- --------------------------------------- ------------------------- -------------------------------- --------------- ---------- ------------------------- ----------- -------- ----------------------- ----------  
148         AdventureWorks Administrator Mail account for administrative e-mail. dba@Adventure-Works.com   AdventureWorks Automated Mailer  NULL            SMTP       smtp.Adventure-Works.com  25          NULL 0                          0        
149         Audit Account                Account for audit e-mail.               audit@Adventure-Works.com Automated Mailer (Audit)         NULL            SMTP       smtp.Adventure-Works.com  25          NULL 0                          0        
```  
  
 **B. 特定のジョブに関する情報を一覧表示する**  
  
 次の例では、`AdventureWorks Administrator` というアカウントについて、アカウント情報を一覧表示します。  
  
```  
EXECUTE msdb.dbo.sysmail_help_account_sp  
    @account_name = 'AdventureWorks Administrator' ;  
```  
  
 次に結果セットを示します。行の長さは編集されています。  
  
```  
account_id  name                         description                             email_address             display_name                     replyto_address servertype servername                port        username use_default_credentials enable_ssl  
----------- ---------------------------- ------------------------------------------------------ ------------------------- ---------------- ---------- ------------------------- ----------- -------- ----------------------- ----------  
148         AdventureWorks Administrator Mail account for administrative e-mail. dba@Adventure-Works.com   AdventureWorks Automated Mailer  NULL            SMTP       smtp.Adventure-Works.com  25          NULL     0                       0       
```  
  
## <a name="see-also"></a>参照  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [データベースメールアカウントを作成する](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースメール ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
