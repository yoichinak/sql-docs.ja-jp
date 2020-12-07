---
description: sp_marksubscriptionvalidation (Transact-SQL)
title: sp_marksubscriptionvalidation (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_marksubscriptionvalidation
- sp_marksubscriptionvalidation_TSQL
helpviewer_keywords:
- sp_marksubscriptionvalidation
ms.assetid: e68fe0b9-5993-4880-917a-b0f661f8459b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4c85f1fbfd603cc671368519716764d2642864fe
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541679"
---
# <a name="sp_marksubscriptionvalidation-transact-sql"></a>sp_marksubscriptionvalidation (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在開いているトランザクションを、指定されたサブスクライバーのサブスクリプションレベルの検証トランザクションとしてマークします。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_marksubscriptionvalidation [ @publication = ] 'publication'  
        , [ @subscriber = ] 'subscriber'  
        , [ @destination_db = ] 'destination_db'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。  
  
`[ @subscriber = ] 'subscriber'` サブスクライバーの名前を指定します。 *サブスクライバー* は sysname,、既定値はありません。  
  
`[ @destination_db = ] 'destination_db'` 転送先データベースの名前を指定します。 *destination_db* は **sysname**であり、既定値はありません。  
  
`[ @publisher = ] 'publisher'` 以外のパブリッシャーを指定し [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *publisher* は **sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  パブリッシャーに属するパブリケーションには、*パブリッシャー*を使用しないでください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_marksubscriptionvalidation** は、トランザクションレプリケーションで使用します。  
  
 **sp_marksubscriptionvalidation** は、以外のサブスクライバーをサポートしていません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 以外のパブリッシャーの場合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、明示的なトランザクション内から **sp_marksubscriptionvalidation** を実行することはできません。 これは、パブリッシャーへのアクセスに使用されるリンクサーバー接続では、明示的なトランザクションがサポートされていないためです。  
  
 **sp_marksubscriptionvalidation**は[sp_article_validation &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)と一緒に使用する必要があります。この場合、 *subscription_level*に**1**を指定し、 **sp_marksubscriptionvalidation**の他の呼び出しと共に使用して、他のサブスクライバーの現在開いているトランザクションをマークできます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_marksubscriptionvalidation**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="example"></a>例  
 次のクエリは、サブスクリプションレベルの検証コマンドを通知するために、パブリッシング データベースに適用できます。 これらのコマンドは、指定されたサブスクライバーのディストリビューションエージェントによって取得されます。 最初のトランザクションでアーティクル '**art1**' が検証され、2番目のトランザクションでは '**art2**' が検証されることに注意してください。 また、 [transact-sql&#41;&#40;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)の**sp_marksubscriptionvalidation**と sp_article_validation の呼び出しがトランザクションにカプセル化されていることにも注意してください。 トランザクションごとに [transact-sql&#41;&#40;sp_article_validation ](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) を呼び出すことをお勧めします。 これは、 [sp_article_validation &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) が、トランザクションの間、ソーステーブルに対して共有テーブルロックを保持しているためです。 コンカレンシーを最大限に高めるために、トランザクションは短くしてください。  
  
```  
begin tran  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub', @destination_db = 'SubDB'  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub2', @destination_db = 'SubDB'  
  
exec sp_article_validation @publication = 'pub1', @article = 'art1',  
 @rowcount_only = 0, @full_or_fast = 0, @shutdown_agent = 0,  
 @subscription_level = 1  
  
commit tran  
  
begin tran  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub', @destination_db = 'SubDB'  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub2', @destination_db = 'SubDB'  
  
exec sp_article_validation @publication = 'pub1', @article = 'art2',  
 @rowcount_only = 0, @full_or_fast = 0, @shutdown_agent = 0,  
 @subscription_level = 1  
  
commit tran  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [レプリケートされたデータの検証](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
