---
description: sys.check_constraints (Transact-sql)
title: sys.check_constraints (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.check_constraints
- sys.check_constraints_TSQL
- check_constraints_TSQL
- check_constraints
dev_langs:
- TSQL
helpviewer_keywords:
- sys.check_constraints catalog view
ms.assetid: 940ebc5e-44ba-4dae-8b29-da94f2d1d6c4
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f1248a45505b06ca40255c77f093aa36ee0b2909
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99188842"
---
# <a name="syscheck_constraints-transact-sql"></a>sys.check_constraints (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  CHECK 制約であるオブジェクトごとに1行の値を保持 **します。 type** = ' C '。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<Columns inherited from sys.objects>**||このビューが継承する列の一覧については、「 [sys. objects &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)」を参照してください。|  
|**is_disabled**|**bit**|CHECK 制約は無効です。|  
|**is_not_for_replication**|**bit**|NOT FOR REPLICATION オプションを使用して作成された CHECK 制約です。|  
|**is_not_trusted**|**bit**|CHECK 制約がシステムによってすべての行に対して検証されていません。|  
|**parent_column_id**|**int**|0は、テーブルレベルの CHECK 制約を示します。<br /><br /> 0以外の値は、これが、指定された ID 値を持つ列に対して定義された列レベルの CHECK 制約であることを示します。|  
|**カスタム**|**nvarchar(max)**|この CHECK 制約を定義する SQL 式です。|  
|**uses_database_collation**|**bit**|1 = 制約の定義は、正しい評価のために、データベースの既定の照合順序に依存します。それ以外の場合は0です。 このような依存関係によって、データベースの既定の照合順序を変更できなくなります。|  
|**is_system_named**|**bit**|1 = システムによって名前が生成されました。<br /><br /> 0 = ユーザーによって指定された名前。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
