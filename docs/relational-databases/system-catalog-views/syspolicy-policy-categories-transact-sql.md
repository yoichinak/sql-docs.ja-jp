---
description: syspolicy_policy_categories (Transact-SQL)
title: syspolicy_policy_categories (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_categories
- syspolicy_policy_categories_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_groups view
ms.assetid: 65f080c7-771f-4cf6-a7a0-88882c637f8d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: d7d5a115beb4f3f4ec543a8ae4861462cf750648
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419856"
---
# <a name="syspolicy_policy_categories-transact-sql"></a>syspolicy_policy_categories (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  インスタンスのポリシーベースの管理のポリシーカテゴリごとに1つの行を表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。 ポリシーカテゴリは、多数のポリシーがある場合にポリシーを整理するのに役立ちます。 次の表では、syspolicy_policy_groups ビュー内の列について説明します。  
 
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|policy_category_id|**int**|ポリシー カテゴリの識別子です。|  
|name|**sysname**|ポリシーカテゴリの名前。|  
|mandate_database_subscriptions|**bit**|明示的なサブスクリプションを持たないインスタンス内のすべてのデータベースにポリシーカテゴリを適用するか (1)、明示的なサブスクリプション (0) を使用してポリシーカテゴリをデータベースに適用する必要があるかどうかを示します。|  
  
## <a name="remarks"></a>解説  
 ポリシーベースの管理ポリシーグループの一覧を表示します。  
  
## <a name="permissions"></a>アクセス許可  
 msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。  
  
## <a name="see-also"></a>参照  
 [ポリシーベースの管理を使用してサーバーを管理する](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [ポリシーベースの管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
