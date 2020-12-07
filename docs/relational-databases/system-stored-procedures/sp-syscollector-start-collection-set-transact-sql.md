---
description: sp_syscollector_start_collection_set (Transact-sql)
title: sp_syscollector_start_collection_set (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_start_collection_set_TSQL
- sp_syscollector_start_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_start_collection_set
ms.assetid: d8357180-f51e-4681-99f9-0596fe2d2b53
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6dbfb03388d78745e7765d48fa591ffe18b66a33
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89534956"
---
# <a name="sp_syscollector_start_collection_set-transact-sql"></a>sp_syscollector_start_collection_set (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  コレクターが既に有効になっており、コレクションセットが実行されていない場合は、コレクションセットを開始します。 コレクターが有効になっていない場合は、 [sp_syscollector_enable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md) を実行してコレクターを有効にした後、このストアドプロシージャを使用してコレクションセットを開始します。  

  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syscollector_start_collection_set   
    [ [ @collection_set_id = ] collection_set_id ]  
    , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @collection_set_id = ] collection_set_id` コレクションセットの一意なローカル識別子を設定します。 *collection_set_id* は **int** で、既定値は NULL です。 *名前*が NULL の場合、 *collection_set_id*には値が必要です。  
  
`[ @name = ] 'name'` コレクションセットの名前を指定します。 *名前* は **sysname** で、既定値は NULL です。 *collection_set_id*が NULL の場合、*名前*には値を指定する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 sp_syscollector_create_collection_set を msdb システム データベースのコンテキストで実行し、SQL Server エージェントを有効にする必要があります。  
  
 このプロシージャをスケジュールがないコレクション セットに対して実行すると、失敗します。 コレクションセットにスケジュールがない場合 (コレクションモードが非キャッシュに設定されている場合など)、 [sp_syscollector_run_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-run-collection-set-transact-sql.md) ストアドプロシージャを使用してコレクションセットを開始します。  
  
 このプロシージャは、コレクションを有効にし、指定されたコレクション セットのジョブをアップロードして、コレクション セットのコレクション モードがキャッシュ (0) に設定されている場合は、直ちにコレクション エージェント ジョブを開始します。 詳細については、「 [sp_syscollector_create_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)」を参照してください。  
  
 コレクション セットにコレクション アイテムが含まれていない場合、この操作には何も効果がありません。 エラー14685は警告として返されます。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行するには、dc_operator 固定データベース ロールのメンバーシップが必要です。 コレクション セットにプロキシ アカウントがない場合は、sysadmin 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、識別子を使用してコレクションセットを開始します。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_start_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>参照  
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)   
 [syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)  
  
  
