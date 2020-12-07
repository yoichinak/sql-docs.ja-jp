---
description: sp_helpremotelogin (Transact-sql)
title: sp_helpremotelogin (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpremotelogin_TSQL
- sp_helpremotelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpremotelogin
ms.assetid: 93f50869-2627-4642-899f-8f626f8833f4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4b35458a0c99eb14db60a058ef72e98df529c217
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547986"
---
# <a name="sp_helpremotelogin-transact-sql"></a>sp_helpremotelogin (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ローカルサーバーで定義されている特定のリモートサーバーまたはすべてのリモートサーバーのリモートログインに関する情報をレポートします。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]代わりに、リンク サーバーとリンク サーバー ストアド プロシージャを使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpremotelogin [ [ @remoteserver = ] 'remoteserver' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>引数  
 [ @remoteserver **=** ] **'***remoteserver***'**  
 リモート ログイン情報を返すリモート サーバーを指定します。 *remoteserver* は **sysname**,、既定値は NULL です。 場合 *remoteserver* が指定されていない、ローカルサーバーで定義されているすべてのリモートサーバーに関する情報が返されます。  
  
 [ @remotename **=** ] **'***remote_name***'**  
 リモートサーバー上の特定のリモートログインを指定します。 *remote_name* は **sysname**,、既定値は NULL です。 *Remote_name*が指定されていない場合は、 *remoteserver*に対して定義されたすべてのリモートユーザーに関する情報が返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|server|**sysname**|ローカルサーバーで定義されているリモートサーバーの名前。|  
|local_user_name|**sysname**|サーバーからのリモートログインがマップされているローカルサーバーでログインします。|  
|remote_user_name|**sysname**|local_user_name にマップされているリモート サーバー上のログイン。|  
|options|**sysname**|Trusted = リモートログインは、リモートサーバーからローカルサーバーに接続するときにパスワードを入力する必要はありません。<br /><br /> 信頼されていない (または空白) = リモートサーバーからローカルサーバーに接続するときに、リモートログインにパスワードの入力が求められます。|  
  
## <a name="remarks"></a>解説  
 ローカル サーバーで定義されているリモート サーバーの名前を表示するには、sp_helpserver を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 アクセス許可はチェックされません。  
  
## <a name="examples"></a>例  
  
### <a name="a-reporting-help-on-a-single-server"></a>A. 1台のサーバーに関するヘルプをレポートする  
 次の例では、リモートサーバー上のすべてのリモートユーザーに関する情報を表示し `Accounts` ます。  
  
```  
EXEC sp_helpremotelogin 'Accounts';  
```  
  
### <a name="b-reporting-help-on-all-remote-users"></a>B. すべてのリモート ユーザーに関するヘルプをレポートする  
 次の例では、ローカルサーバーに認識されているすべてのリモートサーバー上のすべてのリモートユーザーに関する情報を表示します。  
  
```  
EXEC sp_helpremotelogin;  
```  
  
## <a name="see-also"></a>参照  
 [sp_addremotelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)   
 [sp_dropremotelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_remoteoption &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-remoteoption-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
