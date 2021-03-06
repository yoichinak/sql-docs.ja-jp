---
description: sysarticlecolumns (システム ビュー) (Transact-SQL)
title: sysarticlecolumns (システムビュー) (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- sysarticlecolumns
- sysarticlecolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticlecolumns view
ms.assetid: a8dd8d13-c827-45c4-87ba-802725301382
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1de338795532eb470db25a4510f75dc3d6bf4239
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99160344"
---
# <a name="sysarticlecolumns-system-view-transact-sql"></a>sysarticlecolumns (システム ビュー) (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Sysarticlecolumns** ビューでは、パブリッシュされたアーティクルの列に関する追加情報が公開されます。 このビューは、ディストリビューション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|アーティクルを識別します。|  
|**colid**|**int**|アーティクル内の列を識別します。|  
|**is_udt**|**int**|列がユーザー定義データ型 (UDT) 列であるかどうかを示します。 値 **1** は UDT 列を示します。|  
|**is_xml**|**int**|列が **xml** 列かどうかを示します。 値 **1** は **xml** 列を示します。|  
|**is_max**|**int**|列が大きな値のデータ型の列 (**varchar (max)**、 **nvarchar (max)** 、または **varbinary (max)**) であるかどうかを示します。 値 **1** は大きな値の列を示します。|  
  
## <a name="see-also"></a>参照  
 [sp_articlecolumn (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-sql&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
