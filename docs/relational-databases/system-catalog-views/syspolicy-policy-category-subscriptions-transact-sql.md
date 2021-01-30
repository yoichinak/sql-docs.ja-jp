---
description: syspolicy_policy_category_subscriptions (Transact-sql)
title: syspolicy_policy_category_subscriptions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- syspolicy_policy_category_subscriptions_TSQL
- syspolicy_policy_category_subscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_group_subscriptions view
ms.assetid: b3b3a7d7-0b78-46c0-9755-045f7a5692b9
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 4e4b4b82b4b306da1902781fe5b7d15fdf7f1c36
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99180773"
---
# <a name="syspolicy_policy_category_subscriptions-transact-sql"></a>syspolicy_policy_category_subscriptions (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのポリシー ベースの管理サブスクリプションごとに 1 つの行を表示します。 各行には、ターゲットとポリシーカテゴリのペアが記述されています。 次の表では、syspolicy_policy_group_subscriptions ビュー内の列について説明します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|policy_category_subscription_id|**int**|このレコードの識別子。|  
|target_type|**sysname**|このサブスクリプションの対象であるデータベース オブジェクトの種類。|  
|target_object|**sysname**|対象オブジェクトの名前。|  
|policy_category_id|**int**|ターゲットに適用されるポリシーカテゴリの ID。|  
  
## <a name="remarks"></a>コメント  
 このビューには、ポリシーカテゴリにサブスクライブされているターゲットが表示されます。  
  
## <a name="permissions"></a>アクセス許可  
 msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。  
  
## <a name="see-also"></a>参照  
 [ポリシー ベースの管理を使用したサーバーの管理](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [ポリシーベースの管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
