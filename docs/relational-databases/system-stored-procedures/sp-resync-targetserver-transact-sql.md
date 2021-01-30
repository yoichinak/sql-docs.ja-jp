---
description: sp_resync_targetserver (Transact-sql)
title: sp_resync_targetserver (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sp_resync_targetserver
- sp_resync_targetserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_resync_targetserver
ms.assetid: 40e44df7-d3e3-44ee-b149-08aba629a21f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3bd9b8b4b73cf79fc1adc9dcff8fd4754c944e35
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99194369"
---
# <a name="sp_resync_targetserver-transact-sql"></a>sp_resync_targetserver (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定されたターゲット サーバー内のマルチサーバー ジョブをすべて再同期します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_resync_targetserver  
     [ @server_name = ] 'server'  
```  
  
## <a name="arguments"></a>引数  
`[ @server_name = ] 'server'` 再同期するサーバーの名前。 *server* のデータ型は **sysname** で、既定値はありません。 **All** を指定した場合、すべての対象サーバーが再同期されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 **Sp_post_msx_operation** アクションの結果を報告します。  
  
## <a name="remarks"></a>コメント  
 **sp_resync_targetserver** 対象サーバーの現在の命令セットを削除し、ダウンロードする対象サーバーの新しいセットを投稿します。 新しいセットは、すべてのマルチサーバージョブを削除する命令で構成され、その後、サーバーで現在対象となっている各ジョブの挿入が行われます。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの実行権限は、既定では **sysadmin** 固定サーバー ロールのメンバーに与えられています。  
  
## <a name="examples"></a>例  
 次の例では、`SEATTLE1` ターゲット サーバーを再同期します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_resync_targetserver  
    N'SEATTLE1' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_help_downloadlist &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-downloadlist-transact-sql.md)   
 [sp_post_msx_operation &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
