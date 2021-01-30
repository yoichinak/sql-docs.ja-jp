---
description: syspolicy_system_health_state (Transact-SQL)
title: syspolicy_system_health_state (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- syspolicy_system_health_state_TSQL
- syspolicy_system_health_state
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_system_health_state view
ms.assetid: 00815106-9fe4-481d-a9e1-a256101887f4
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 245ce67d7ee94eca468c9cda775cff15f0b520a0
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99180758"
---
# <a name="syspolicy_system_health_state-transact-sql"></a>syspolicy_system_health_state (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ポリシーベースの管理ポリシーと対象のクエリ式の組み合わせごとに1つの行を表示します。 サーバーのポリシー正常性をプログラムで確認するには、syspolicy_system_health_state ビューを使用します。 次の表では、syspolicy_system_health_state ビュー内の列について説明します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|health_state_id|**bigint**|ポリシー正常性状態レコードの識別子。|  
|policy_id|**int**|ポリシーの識別子。|  
|last_run_date|**datetime**|ポリシーが最後に実行された日時。|  
|target_query_expression_with_id|**nvarchar (400)**|Id 変数に割り当てられた値を持つターゲット式。ポリシーの評価対象となるターゲットを定義します。|  
|target_query_expression|**nvarchar(max)**|ポリシーの評価対象となるターゲットを定義する対象。|  
|結果|**bit**|ポリシーに関して、このターゲットのヘルス状態:<br /><br /> 0 = 失敗<br /><br /> 1 = 成功|  
  
## <a name="remarks"></a>コメント  
 syspolicy_system_health_state ビューには、対象のクエリ式の最新の正常性状態が、アクティブ (有効) なポリシーごとに表示されます。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] オブジェクト エクスプローラーと [オブジェクト エクスプローラーの詳細] ページでは、このビューのポリシー正常性が集計され、重大な正常性状態が表示されます。  
  
## <a name="permissions"></a>アクセス許可  
 msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。  
  
## <a name="see-also"></a>参照  
 [ポリシー ベースの管理を使用したサーバーの管理](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [ポリシーベースの管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
