---
description: sp_droplinkedsrvlogin (Transact-sql)
title: sp_droplinkedsrvlogin (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droplinkedsrvlogin_TSQL
- sp_droplinkedsrvlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droplinkedsrvlogin
ms.assetid: 75a4a040-72d5-4d29-8304-de0aa481ad4b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 30e4d997e79d0e66a75fdff8ea6c162ab7bf7634
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536535"
---
# <a name="sp_droplinkedsrvlogin-transact-sql"></a>sp_droplinkedsrvlogin (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  を実行しているローカルサーバー上のログインと、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リンクサーバー上のログインとの間の既存のマッピングを削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_droplinkedsrvlogin [ @rmtsrvname= ] 'rmtsrvname' ,   
   [ @locallogin= ] 'locallogin'  
```  
  
## <a name="arguments"></a>引数  
`[ @rmtsrvname = ] 'rmtsrvname'` ログインマッピングが適用されるリンクサーバーの名前を指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *rmtsrvname* は **sysname**,、既定値はありません。 *rmtsrvname* は既に存在している必要があります。  
  
`[ @locallogin = ] 'locallogin'`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]リンクサーバー *rmtsrvname*へのマッピングを持つローカルサーバー上のログインを指定します。 *locallogin* は **sysname**,、既定値はありません。 *Locallogin*から*rmtsrvname*へのマッピングが既に存在している必要があります。 NULL の場合、 **sp_addlinkedserver**によって作成された既定のマッピングは、ローカルサーバー上のすべてのログインをリンクサーバー上のログインにマップします。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 ログインの既存のマッピングが削除されると、ローカルサーバーは、そのログインに代わってリンクサーバーに接続するときに、 **sp_addlinkedserver** によって作成された既定のマッピングを使用します。 既定のマッピングを変更するには、 **sp_addlinkedsrvlogin**を使用します。  
  
 既定のマッピングも削除された場合、 **sp_addlinkedsrvlogin**を使用して、リンクサーバーへのログインマッピングが明示的に指定されているログインだけが、リンクサーバーにアクセスできます。  
  
 ユーザー定義のトランザクション内から**sp_droplinkedsrvlogin**を実行することはできません。  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する ALTER ANY LOGIN 権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-removing-the-login-mapping-for-an-existing-user"></a>A. 既存のユーザーのログイン マッピングを削除する  
 次の例では、ログイン `Mary` に関するローカル サーバーとリンク サーバー `Accounts` のマッピングを削除します。 その結果、ログイン `Mary` は既定のログイン マッピングを使用します。  
  
```  
EXEC sp_droplinkedsrvlogin 'Accounts', 'Mary';  
```  
  
### <a name="b-removing-the-default-login-mapping"></a>B. 既定のログインマッピングを削除しています  
 次の例では、リンクサーバーでを実行して作成された既定のログインマッピングを削除し `sp_addlinkedserver` `Accounts` ます。  
  
```  
EXEC sp_droplinkedsrvlogin 'Accounts', NULL;  
```  
  
## <a name="see-also"></a>参照  
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
