---
description: sp_defaultlanguage (Transact-sql)
title: sp_defaultlanguage (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_defaultlanguage
- sp_defaultlanguage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_defaultlanguage
ms.assetid: 908d01cc-e704-45d9-9e85-d2df6da3e6f5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5eb94ea64b22f233d1c7c1e5d508fc0704f931ab
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549870"
---
# <a name="sp_defaultlanguage-transact-sql"></a>sp_defaultlanguage (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの既定の言語を変更します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) を使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_defaultlanguage [ @loginame = ] 'login'   
     [ , [ @language = ] 'language' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @loginame = ] 'login'` ログイン名を指定します。 *login* は **sysname**,、既定値はありません。 *ログイン* には、既存 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のログインまたは Windows ユーザーまたはグループを指定できます。  
  
`[ @language = ] 'language'` ログインの既定の言語を設定します。 *language* は **sysname**,、既定値は NULL です。 *言語* は、サーバーで有効な言語である必要があります。 *Language*が指定されていない場合、 *language*はサーバーの既定の言語に設定されます。既定の言語は、 **sp_configure**構成変数の**既定の言語**によって定義されます。 サーバーの既定の言語を変更しても、既存のログインの既定の言語は変更されません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_defaultlanguage** は ALTER LOGIN を呼び出します。この場合、追加のオプションがサポートされます。 他のログインの既定値の変更については、「 [ALTER login &#40;transact-sql&#41;](../../t-sql/statements/alter-login-transact-sql.md)」を参照してください。  
  
 SET LANGUAGE ステートメントを使用して、現在のセッションの言語を変更します。 @LANGUAGE現在の言語設定を表示するには、@ 関数を使用します。  
  
 ログインの既定の言語がサーバーから削除された場合、ログインはサーバーの既定の言語を取得します。 **sp_defaultlanguage** は、ユーザー定義のトランザクション内では実行できません。  
  
 サーバーにインストールされている言語に関する情報は、 **sys.sys言語** カタログビューに表示されます。  
  
## <a name="permissions"></a>アクセス許可  
 ALTER ANY LOGIN 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、`ALTER LOGIN` を使用して、ログイン `Fathima` の既定の言語をアラビア語に変更します。 可能であればこの方法の使用をお勧めします。  
  
```  
ALTER LOGIN Fathima WITH DEFAULT_LANGUAGE = Arabic;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [@@LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/functions/language-transact-sql.md)   
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [sys.sys言語 &#40;Transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
