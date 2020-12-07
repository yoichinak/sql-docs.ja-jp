---
description: sys.sysremotelogins (Transact-sql)
title: sys.sysremotelogins (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysremotelogins
- sysremotelogins_TSQL
- sys.sysremotelogins
- sys.sysremotelogins_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysremotelogins system table
- sys.sysremotelogins compatibility view
ms.assetid: b7ffcfa6-aed8-41d4-8b70-845439ab813d
author: rothja
ms.author: jroth
ms.openlocfilehash: 39cf5ae09d0857acf7d0d89b2be789162a751b64
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482055"
---
# <a name="syssysremotelogins-transact-sql"></a>sys.sysremotelogins (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  のインスタンス上でリモートストアドプロシージャを呼び出すことが許可されているリモートユーザーごとに1行のレコードを格納 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**remoteserverid**|**smallint**|リモートサーバーの識別。|  
|**remoteusername**|**sysname**|リモートサーバー上のユーザーのログイン名。|  
|**status**|**smallint**|0 を返します。|  
|**sid**|**varbinary (85)**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ユーザーのセキュリティ ID。|  
|**changedate**|**datetime**|リモートユーザーが追加された日付と時刻。|  
  
## <a name="see-also"></a>参照  
 [システムビューへのシステムテーブルのマッピング &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
