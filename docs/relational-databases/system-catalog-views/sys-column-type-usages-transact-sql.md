---
description: sys.column_type_usages (Transact-sql)
title: sys.column_type_usages (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- column_type_usages
- sys.column_type_usages_TSQL
- column_type_usages_TSQL
- sys.column_type_usages
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_type_usages catalog view
ms.assetid: 1ead375e-f662-4837-903f-8947496c51e4
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 89c75790423de750c30af2859bac3f1972668a49
ms.sourcegitcommit: 15c7cd187dcff9fc91f2daf0056b12ed3f0403f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2021
ms.locfileid: "102465134"
---
# <a name="syscolumn_type_usages-transact-sql"></a>sys.column_type_usages (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ユーザー定義型の列ごとに 1 行のデータを保持します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|この列が所属するオブジェクトの ID。|  
|**column_id**|**int**|列の ID。 は、オブジェクト内で一意です。|  
|**user_type_id**|**int**|ユーザー定義型の ID。<br /><br /> 型の名前を返すには、この列の [型](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) のカタログビューに結合します。|  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;スカラー型のカタログビュー ](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server システム カタログに対するクエリに関してよく寄せられる質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.yml)  
  
  
