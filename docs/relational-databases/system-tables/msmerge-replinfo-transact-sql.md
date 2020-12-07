---
description: MSmerge_replinfo (Transact-sql)
title: MSmerge_replinfo (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_replinfo_TSQL
- MSmerge_replinfo
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_replinfo system table
ms.assetid: b0924094-c0cc-49c1-869a-65be0d0465a0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ce4bee70ea5ef410512ce399e8d715fbc321e1a6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545610"
---
# <a name="msmerge_replinfo-transact-sql"></a>MSmerge_replinfo (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_replinfo**テーブルには、サブスクリプションごとに1つの行が含まれています。 このテーブルは、サブスクリプションに関する情報を追跡します。 このテーブルは、パブリケーションデータベースとサブスクリプションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**repid**|**uniqueidentifier**|レプリカの一意な ID。|  
|**use_interactive_resolver**|**bit**|調整時にインタラクティブ競合回避モジュールを使用するかどうかを指定します。<br /><br /> **0** = 対話型競合回避モジュールを使用しません。<br /><br /> **1** = 対話型競合回避モジュールを使用します。|  
|**validation_level**|**int**|サブスクリプションに対して実行する検証の種類。 指定される検証レベルは、次のいずれかの値になります。<br /><br /> **0** = 検証なし。<br /><br /> **1** = 行数のみの検証。<br /><br /> **2** = 行数とチェックサムの検証。<br /><br /> **3** = 行数とバイナリチェックサムの検証。|  
|**resync_gen**|**bigint**|サブスクリプションの再同期化で使用される世代番号。 値 **-1** は、サブスクリプションが再同期の対象としてマークされていないことを示します。|  
|**login_name**|**sysname**|サブスクリプションを作成したユーザーの名前。|  
|**hostname**|**sysname**|サブスクリプションのパーティションの生成時に、パラメーター化された行フィルターで使用される値。|  
|**merge_jobid**|**binary(16)**|サブスクリプションのマージ ジョブ ID。|  
|**sync_info**|**int**|内部使用のみ。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
