---
description: sp_article_validation (Transact-sql)
title: sp_article_validation (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_article_validation_TSQL
- sp_article_validation
helpviewer_keywords:
- sp_article_validation
ms.assetid: 44e7abcd-778c-4728-a03e-7e7e78d3ce22
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 111b11b9563373f972ba6d30338e67075f992bed
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536739"
---
# <a name="sp_article_validation-transact-sql"></a>sp_article_validation (Transact-sql)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  指定されたアーティクルに対する検証の要求を開始します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行され、サブスクライバー側でサブスクリプションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_article_validation [ @publication = ] 'publication'  
    [ , [ @article = ] 'article' ]  
    [ , [ @rowcount_only = ] type_of_check_requested ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @subscription_level = ] subscription_level ]  
    [ , [ @reserved = ] reserved ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` アーティクルが存在するパブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。  
  
`[ @article = ] 'article'` 検証するアーティクルの名前を指定します。 *アーティクル* は **sysname**で、既定値はありません。  
  
`[ @rowcount_only = ] type_of_check_requested` テーブルの行数のみを返すかどうかを指定します。 *type_of_check_requested* は **smallint**,、既定値は **1**です。  
  
 **0**の場合は、rowcount と互換性のある7.0 のチェックサムを実行し [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
 **1**の場合は、行数チェックのみを実行します。  
  
 **2**の場合は、行数とバイナリチェックサムを実行します。  
  
`[ @full_or_fast = ] full_or_fast` 行数を計算するために使用されるメソッドです。 *full_or_fast* は **tinyint**で、次のいずれかの値を指定できます。  
  
|**Value**|**説明**|  
|---------------|---------------------|  
|**0**|COUNT(*) を使用してフル カウントを実行します。|  
|**1**|Sysindexes から高速カウントを実行し **ます**。 **Sysindexes**内の行のカウントは、実際のテーブルの行をカウントするよりも高速です。 ただし、 **sysindexes** は遅延して更新され、行数が正確ではない可能性があります。|  
|**2** (既定値)|最初に fast メソッドを試行して、条件付き高速カウントを実行します。 Fast メソッドが相違点を示している場合、は完全なメソッドに戻ります。 *Expected_rowcount*が NULL で、ストアドプロシージャを使用して値を取得している場合は、常に完全なカウント (*) が使用されます。|  
  
`[ @shutdown_agent = ] shutdown_agent` 検証の完了後すぐにディストリビューションエージェントをシャットダウンするかどうかを指定します。 *shutdown_agent* は **ビット**,、既定値は **0**です。 **0**の場合、ディストリビューションエージェントはシャットダウンされません。 **1**の場合、アーティクルの検証後にディストリビューションエージェントがシャットダウンされます。  
  
`[ @subscription_level = ] subscription_level` 一連のサブスクライバーによって検証が選択されるかどうかを指定します。 *subscription_level* は **ビット**,、既定値は **0**です。 **0**の場合、すべてのサブスクライバーに検証が適用されます。 **1**の場合、検証は、現在開いているトランザクション内の**sp_marksubscriptionvalidation**を呼び出すことによって指定されたサブスクライバーのサブセットにのみ適用されます。  
  
`[ @reserved = ] reserved` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @publisher = ] 'publisher'` 以外のパブリッシャーを指定し [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *publisher* は **sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  パブリッシャーの検証を要求するときは、*パブリッシャー*を使用しないでください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_article_validation** は、トランザクションレプリケーションで使用します。  
  
 **sp_article_validation** によって、指定されたアーティクルで検証情報が収集され、検証要求がトランザクションログに送信されます。 ディストリビューション エージェントは、この要求を受け取ると、要求に含まれている検証の情報をサブスクライバー テーブルと比較します。 検証の結果は、レプリケーション モニターおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの警告に表示されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_article_validation**を実行できるのは、検証対象のアーティクルのソーステーブルに対する SELECT ALL 権限を持つユーザーだけです。  
  
## <a name="see-also"></a>参照  
 [レプリケートされたデータの検証](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_marksubscriptionvalidation &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md)   
 [sp_publication_validation &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [sp_table_validation &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
