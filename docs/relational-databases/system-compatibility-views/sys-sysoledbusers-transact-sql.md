---
description: sys.sysoledbusers (Transact-SQL)
title: sys.sysoledbusers (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.sysoledbusers
- sys.sysoledbusers_TSQL
- sysoledbusers
- sysoledbusers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysoledbusers system table
- sys.sysoledbusers compatibility view
ms.assetid: fe924c17-9cad-4b2b-8124-1e0fd82931e3
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 4e8c134ad74b24704696b586bb362ab253dedb84
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99148540"
---
# <a name="syssysoledbusers-transact-sql"></a>sys.sysoledbusers (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

    
> [!IMPORTANT]  
>  この [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] システムテーブルは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、旧バージョンとの互換性を保つためのビューとしてに含まれています。 代わりに、 [カタログビュー](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) を使用することをお勧めします。  
  
 指定したリンク サーバーのユーザーとパスワードのマッピングごとに 1 行のデータを格納します。 **sysoledbusers** は、 **master** データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**rmtsrvid**|**smallint**|サーバーのセキュリティ id 番号 (SID)。|  
|**rmtloginame**|**nvarchar (** 128 **)**|リンクされた **rmtservid** の **loginsid** がマップされるリモートログインの名前。|  
|**rmtpassword**|**nvarchar (** 128 **)**|NULL を返します。|  
|**loginsid**|**varbinary (** 85 **)**|マップされるローカルログインの SID。|  
|**status**|**smallint**|1の場合、マッピングはユーザーの資格情報を使用する必要があります。|  
|**changedate**|**datetime**|マッピング情報が最後に変更された日付。|  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
