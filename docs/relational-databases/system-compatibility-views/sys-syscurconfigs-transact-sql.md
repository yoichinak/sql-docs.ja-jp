---
description: sys.syscurconfigs (Transact-SQL)
title: sys.syscurconfigs (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.syscurconfigs
- sys.syscurconfigs_TSQL
- syscurconfigs
- syscurconfigs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.syscurconfigs compatibility view
- syscurconfigs system table
ms.assetid: 454ab849-07a5-4b50-ba0a-6b1b14721f77
author: rothja
ms.author: jroth
ms.openlocfilehash: c5c83219c93c24929b257989a034f283cf2ac5b2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423326"
---
# <a name="syssyscurconfigs-transact-sql"></a>sys.syscurconfigs (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在の各構成オプションのエントリが含まれています。 また、このビューには、構成構造を表す 4 つのエントリも登録されます。 **syscurconfigs** は、ユーザーがクエリを行うときに動的に構築されます。 詳細については、「 [sys.sys&#40;transact-sql&#41;を構成 ](../../relational-databases/system-compatibility-views/sys-sysconfigures-transact-sql.md)する」を参照してください。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**value**|**int**|ユーザーが変更可能な変数の値。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]再構成が実行されている場合にのみ、によって使用されます。|  
|**config**|**smallint**|構成変数番号。|  
|**comment**|**nvarchar (255)**|構成オプションの説明。|  
|**status**|**smallint**|オプションの状態を示すビットマップ。 次の値があります。<br /><br /> 0 = 静的。 設定は、サーバーの再起動時に有効になります。<br /><br /> 1 = 動的。 変数は、再構成ステートメントが実行されたときに有効になります。<br /><br /> 2 = 詳細。 変数は、 **[詳細の表示] オプション** が設定されている場合にのみ表示されます。<br /><br /> 3 = 動的および詳細。|  
  
## <a name="see-also"></a>参照  
 [システムビューへのシステムテーブルのマッピング &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
