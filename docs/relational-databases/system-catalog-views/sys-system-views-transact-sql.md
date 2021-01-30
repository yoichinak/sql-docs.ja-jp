---
description: sys.system_views (Transact-sql)
title: sys.system_views (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.system_views_TSQL
- system_views
- system_views_TSQL
- sys.system_views
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_views catalog view
ms.assetid: a526c410-e7b5-4075-8103-e1f3c6837c3c
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: e0dcaebcf38e4aa3b1cbee41d5528f8d10a991cf
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99189280"
---
# <a name="syssystem_views-transact-sql"></a>sys.system_views (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  に付属しているシステムビューごとに1行の値を格納 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] します。 すべてのシステムビューは、 **sys** または **INFORMATION_SCHEMA** という名前のスキーマに含まれています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|\<inherited columns>||このビューが継承する列の一覧については、「 [sys. objects &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)」を参照してください。|  
|**is_replicated**|**bit**|1 = ビューはレプリケートされます。|  
|**has_replication_filter**|**bit**|1 = ビューにレプリケーション フィルターがあります。|  
|**has_opaque_metadata**|**bit**|1 = ビューに対して指定された VIEW_METADATA オプションです。 詳細については、「[CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)」を参照してください。|  
|**has_unchecked_assembly_data**|**bit**|1 = テーブルには、最後の ALTER ASSEMBLY 中に定義が変更されたアセンブリに依存する永続化されたデータが含まれています。 次の DBCC CHECKDB または DBCC CHECKTABLE が正常に完了した後、は0にリセットされます。|  
|**with_check_option**|**bit**|1 = WITH CHECK OPTION がビュー定義で指定されています。|  
|**is_date_correlation_view**|**bit**|1 = ビューは、 **datetime** 列間の相関関係情報を格納するためにシステムによって自動的に作成されました。 DATE_CORRELATION_OPTIMIZATION を ON に設定することにより、このビューの作成が有効になりました。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [DBCC CHECKDB &#40;Transact-sql&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)   
 [DBCC CHECKTABLE &#40;Transact-sql&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)   
 [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
  
