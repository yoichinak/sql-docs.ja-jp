---
description: MSpeer_request (Transact-sql)
title: MSpeer_request (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_request
- MSpeer_request_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_request system table
ms.assetid: ed048c46-7a2f-4ad0-bc7c-c2d65e83b4fb
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5b4c0352e9e0b0fab04be0dbbc1ff2a62d691c48
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545587"
---
# <a name="mspeer_request-transact-sql"></a>MSpeer_request (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  MSpeer_request テーブルは、ピアツーピアレプリケーションで、特定のパブリケーションに対する状態要求を追跡するために使用されます。 このテーブルは、パブリケーションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|id|**int**|要求を識別します。|  
|パブリケーション (publication)|**sysname**|ステータス要求が開始されたパブリケーションの名前。|  
|sent_date|**datetime**|状態要求が開始された日付と時刻|  
|description|**nvarchar (4000)**|個々の状態要求を識別するために使用できるユーザー定義の情報。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
