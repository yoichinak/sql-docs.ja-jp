---
description: sys.sp_xtp_control_query_exec_stats (Transact-SQL)
title: sp_xtp_control_query_exec_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/13/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_control_query_exec_stats_TSQL
- sys.sp_xtp_control_query_exec_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_control_query_exec_stats
ms.assetid: 4838125d-ad1e-479e-b7d2-42655e8f4f02
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 74e92f12d7003df9a4e0a23ac451d016b84fd5bc
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89525373"
---
# <a name="syssp_xtp_control_query_exec_stats-transact-sql"></a>sys.sp_xtp_control_query_exec_stats (Transact-SQL)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  インスタンスに関するすべてのネイティブ コンパイル ストアド プロシージャ、または特定のネイティブ コンパイル ストアド プロシージャのクエリごとの統計コレクションを有効にします。  
  
 統計コレクションを有効にすると、パフォーマンスが低下します。 1つまたはいくつかのネイティブコンパイルストアドプロシージャのトラブルシューティングのみを行う必要がある場合は、ごく一部のネイティブコンパイルストアドプロシージャに対してのみ統計コレクションを有効にすることができます。  
  
 すべてのネイティブコンパイルストアドプロシージャのプロシージャレベルで統計コレクションを有効にするには、「 [sys. sp_xtp_control_proc_exec_stats &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
sp_xtp_control_query_exec_stats [ [ @new_collection_value = ] collection_value ],  
[ [ @database_id = ] database_id   
[ , [ @xtp_object_id = ] procedure_id ] ,   
[ @old_collection_value] ]  
```  
  
## <a name="arguments"></a>引数  
 @new_collection_value = *値*  
 プロシージャレベルの統計コレクションが on (1) か off (0) かを指定します。  
  
 @new_collection_value は、の起動時に0に設定され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
 @database_id = = *database_id*、 @xtp_object_id = *procedure_id*  
 ネイティブ コンパイル ストアド プロシージャのデータベース ID とオブジェクト ID。 インスタンスに対して統計コレクションが有効になっている場合 ([sp_xtp_control_proc_exec_stats &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md))、ネイティブコンパイルストアドプロシージャの統計情報が収集されます。 インスタンスの統計情報の収集をオフにしても、個々のネイティブコンパイルストアドプロシージャの統計コレクションは無効になりません。  
  
 Transact-sql [&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)、 [sys. プロシージャ ](../../relational-databases/system-catalog-views/sys-procedures-transact-sql.md)を使用して transact-sql&#41;を &#40;DB_ID &#40;[transact-sql&#41;](../../t-sql/functions/db-id-transact-sql.md)を使用するか、transact-sql [OBJECT_ID ](../../t-sql/functions/object-id-transact-sql.md) を &#40;して、データベースとストアドプロシージャの id を取得 &#40;ます。  
  
 @old_collection_value = *値*  
 現在の状態を返します。  
  
## <a name="return-code"></a>リターンコード  
 成功した場合は 0。 エラーの場合は0以外の。  
  
## <a name="permissions"></a>アクセス許可  
 固定 sysadmin ロールのメンバーシップが必要です。  
  
## <a name="code-sample"></a>コード サンプル  
 次のコードサンプルは、インスタンスのすべてのネイティブコンパイルストアドプロシージャの統計コレクションと、特定のネイティブコンパイルストアドプロシージャの統計コレクションを有効にする方法を示しています。  
  
```sql   
DECLARE @c bit  
  
EXEC [sys].[sp_xtp_control_query_exec_stats] @new_collection_value = 1;  
  
EXEC sp_xtp_control_query_exec_stats @old_collection_value=@c output;  
SELECT @c AS 'collection status';  
  
EXEC [sys].[sp_xtp_control_query_exec_stats] @new_collection_value = 1,   
@database_id = 5, @xtp_object_id = 341576255;  
  
EXEC sp_xtp_control_query_exec_stats @database_id = 5,   
@xtp_object_id = 341576255, @old_collection_value=@c output;  
  
SELECT @c AS 'collection status';  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
