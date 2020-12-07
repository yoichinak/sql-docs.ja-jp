---
description: sp_mergemetadataretentioncleanup (Transact-sql)
title: sp_mergemetadataretentioncleanup (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergemetadataretentioncleanup
- sp_mergemetadataretentioncleanup_TSQL
helpviewer_keywords:
- sp_mergemetadataretentioncleanup
ms.assetid: 4e8d6343-2a38-421d-a3f3-c37d437a0f88
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6f18a4f9357e3af6d9b120195dd13e187de95fd3
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535125"
---
# <a name="sp_mergemetadataretentioncleanup-transact-sql"></a>sp_mergemetadataretentioncleanup (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)、 [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)、 [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)、 [MSmerge_past_partition_mappings](../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md)、および[MSmerge_current_partition_mappings](../../relational-databases/system-tables/msmerge-current-partition-mappings.md)システムテーブル内のメタデータの手動クリーンアップを実行します。 このストアド プロシージャは、トポロジ内の各パブリッシャーおよびサブスクライバーで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_mergemetadataretentioncleanup [ [ @num_genhistory_rows = ] num_genhistory_rows OUTPUT ]  
    [ , [ @num_contents_rows = ] num_contents_rows OUTPUT ]   
    [ , [ @num_tombstone_rows = ] num_tombstone_rows OUTPUT ]   
    [ , [ @aggressive_cleanup_only = ] aggressive_cleanup_only ]  
```  
  
## <a name="arguments"></a>引数  
`[ @num_genhistory_rows = ] num_genhistory_rows OUTPUT`[MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)テーブルからクリーンアップされた行の数を返します。 *num_genhistory_rows* は **int**,、既定値は **0**です。  
  
`[ @num_contents_rows = ] num_contents_rows OUTPUT`[MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)テーブルからクリーンアップされた行の数を返します。 *num_contents_rows* は **int**,、既定値は **0**です。  
  
`[ @num_tombstone_rows = ] num_tombstone_rows OUTPUT`[MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)テーブルからクリーンアップされた行の数を返します。 *num_tombstone_rows* は **int**,、既定値は **0**です。  
  
`[ @aggressive_cleanup_only = ] aggressive_cleanup_only` 内部でのみ使用します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
  
> [!IMPORTANT]  
>  データベースに複数のパブリケーションが存在し、それらのパブリケーションのいずれかが無期限のパブリケーション保有期間を使用する場合、 **sp_mergemetadataretentioncleanup** を実行しても、データベースのマージレプリケーション変更追跡メタデータはクリーンアップされません。 このため、無期限のパブリケーション保有期間は注意して使用してください。 パブリケーションに無期限の保有期間が設定されているかどうかを確認するには、パブリッシャーで[transact-sql&#41;を実行 &#40;sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)を実行し、**保有**期間に**0**を指定して結果セット内のすべてのパブリケーションを確認します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_mergemetadataretentioncleanup**を実行できるのは、 **db_owner**固定データベースロールのメンバー、またはパブリッシュされたデータベースのパブリケーションアクセスリスト内のユーザーだけです。  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
