---
description: sp_scriptsubconflicttable (Transact-sql)
title: sp_scriptsubconflicttable (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_scriptsubconflicttable
- sp_scriptsubconflicttable_TSQL
helpviewer_keywords:
- sp_scriptsubconflicttable
ms.assetid: 13867145-3dad-47a4-8d50-a65175418479
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3e8fe3437c1852ffb2ec5817125317fa1a8fa379
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538546"
---
# <a name="sp_scriptsubconflicttable-transact-sql"></a>sp_scriptsubconflicttable (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  キューに登録されたサブスクリプション アーティクルのサブスクライバー上に競合テーブルを作成するためのスクリプトを生成します。 生成されたスクリプトは、サブスクライバー側でサブスクリプション データベースについて実行されます。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_scriptsubconflicttable [@publication =] 'publication'    , [@article =] 'article'  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` アーティクルを含むパブリケーションの名前を指定します。 名前はデータベース内で一意である必要があります。 *publication* は **sysname**,、既定値はありません。  
  
`[ @article = ] 'article'` サブスクリプションアーティクルの名前を指定します。 *アーティクル* は **sysname**で、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**cmdtext**|**nvarchar (4000)**|キューに登録されたサブスクリプション アーティクルのサブスクライバー上に競合テーブルを作成するための [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトを返します。 このスクリプトは、サブスクリプションデータベースのサブスクライバーで実行されます。|  
  
## <a name="remarks"></a>解説  
 **sp_scriptsubconflicttable** は、初期スナップショットが手動で適用されるサブスクリプションを持つサブスクライバーに対して使用します。 競合テーブルは、サブスクライバー側のオプションのテーブルです。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_scriptsubconflicttable**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [キュー更新の競合の検出と解決](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
