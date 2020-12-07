---
description: sys. 期間 (Transact-sql)
title: sys. 期間 (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 25e66ed3-2270-4c5c-9f5a-2c0f165a57ca
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c091649234826080054de942ed96272055a1b595
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810326"
---
# <a name="sysperiods-transact-sql"></a>sys. 期間 (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  期間が定義されているテーブルごとに1行の値を返します。  
  
|列ヘッダー|データ型|説明|  
|-------------------|---------------|-----------------|  
|name|**sysname**|期間の名前|  
|period_type|**tinyint**|期間の種類を表す数値。<br /><br /> 1 = システム期間|  
|period_type_desc|**nvarchar(60)**|列の型の説明テキスト。<br /><br /> SYSTEM_TIME_PERIOD|  
|object_id|**int**|Period_type 列を含むテーブルの id|  
|start_column_id|**int**|下限の期間の境界を定義する列の id|  
|end_column_id|**int**|上限期間の境界を定義する列の id|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [システムビュー &#40;Transact-sql&#41;](../../t-sql/language-reference.md)   
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.all_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.system_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)   
 [SQL Server システムカタログに対するクエリについてよく寄せられる質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [テンポラル テーブル](../../relational-databases/tables/temporal-tables.md)  
  
