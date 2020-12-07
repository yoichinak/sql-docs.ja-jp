---
description: sp_syscollector_run_collection_set (Transact-SQL)
title: sp_syscollector_run_collection_set (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_run_collection_set_TSQL
- sp_syscollector_run_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_run_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: 7bbaee48-dfc7-45c0-b11f-c636b6a7e720
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 19d13692fda89e3596388269ef9a860615c3fb4b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544760"
---
# <a name="sp_syscollector_run_collection_set-transact-sql"></a>sp_syscollector_run_collection_set (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  コレクターが既に有効になっており、コレクション セットが非キャッシュ コレクション モード用に構成されている場合、コレクション セットを開始します。  
  
> [!NOTE]  
>  キャッシュコレクションモード用に構成されているコレクションセットに対して実行する場合、この手順は失敗します。  
  
 sp_syscollector_run_collection_set を使用すると、ユーザーはオンデマンドのデータ スナップショットを取得できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syscollector_run_collection_set [[ @collection_set_id = ] collection_set_id ]  
          , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @collection_set_id = ] collection_set_id` コレクションセットの一意なローカル識別子を設定します。 *collection_set_id* は **int** で、 *name* が NULL の場合は値が必要です。  
  
`[ @name = ] 'name'` コレクションセットの名前を指定します。 *名前* は **sysname** であり、 *collection_set_id* が NULL の場合は値を持つ必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 *Collection_set_id*または*名前*には値を指定する必要があります。どちらも NULL にすることはできません。  
  
 この手順では、コレクションを開始し、指定されたコレクションセットのジョブをアップロードします。また、コレクションセットの** \@ collection_mode**が非キャッシュ (1) に設定されている場合は、直ちにコレクションエージェントジョブを開始します。 詳細については、「 [sp_syscollector_create_collection_set &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)」を参照してください。  
  
 sp_sycollector_run_collection_set は、スケジュールを持たないコレクション セットの実行にも使用できます。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行するには、 **dc_operator** (EXECUTE 権限を持つ) 固定データベースロールのメンバーシップが必要です。  
  
## <a name="example"></a>例  
 対応する ID を使ってコレクション セットを開始します。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_run_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)  
  
  
