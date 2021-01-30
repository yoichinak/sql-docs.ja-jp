---
description: sp_unregistercustomresolver (Transact-SQL)
title: sp_unregistercustomresolver (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- sp_unregistercustomresolver_TSQL
- sp_unregistercustomresolver
helpviewer_keywords:
- sp_unregistercustomresolver
ms.assetid: 08bd20c8-c6be-4be2-be9f-2b5e1d7bee43
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1a8bb2c7384312d9782bdb6169d17ace6eae7c6f
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99202339"
---
# <a name="sp_unregistercustomresolver-transact-sql"></a>sp_unregistercustomresolver (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  以前に登録されたビジネスロジックモジュールの登録を解除します。 ビジネスロジックは、COM コンポーネントまたは .NET Framework アセンブリのいずれかの形式にすることができ [!INCLUDE[msCoName](../../includes/msconame-md.md)] ます。 このストアド プロシージャは、カスタム ビジネス ロジックが登録されたディストリビューターで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_unregistercustomresolver [ @article_resolver = ] 'article_resolver'   
```  
  
## <a name="arguments"></a>引数  
`[ @article_resolver = ] 'article_resolver'` 登録を解除するカスタムビジネスロジックの名前を指定します。 *article_resolver* は **nvarchar (255)**,、既定値はありません。 削除されるビジネスロジックが COM コンポーネントの場合、このパラメーターはコンポーネントのフレンドリ名です。 ビジネス ロジックが .NET Framework アセンブリの場合、このパラメーターはアセンブリの名前になります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_unregistercustomresolver** は、マージレプリケーションで使用します。  
  
 レプリケーショントポロジ内の任意のサーバーで [sp_enumcustomresolvers](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) を使用して、トポロジで使用可能な登録済みカスタムビジネスロジックモジュールまたは COM 競合回避モジュールの一覧を返します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_unregistercustomresolver** を実行できるのは、固定サーバーロール **sysadmin** または固定データベースロール **db_owner** のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_lookupcustomresolver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [sp_registercustomresolver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
