---
description: syspolicy_policy_execution_history_details (Transact-SQL)
title: syspolicy_policy_execution_history_details (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_execution_history_details
- syspolicy_policy_execution_history_details_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_execution_history_details view
ms.assetid: 97ef6573-5e8b-4ba5-8ae0-7901e79a9683
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ecb084ff03931bc82a7a07e19f66949d8a834343
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423396"
---
# <a name="syspolicy_policy_execution_history_details-transact-sql"></a>syspolicy_policy_execution_history_details (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  実行された条件式、式のターゲット、各実行の結果、および発生した場合はエラーの詳細が表示されます。 次の表では、syspolicy_execution_history_details ビューの列について説明します。  
  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|detail_id|**bigint**|このレコードの識別子。 各レコードは、ポリシー内で1つの条件式を評価または適用する試行を表します。 複数の対象に適用された場合、条件ごと、対象ごとに明細レコードが作成されます。|  
|history_id|**bigint**|履歴イベントの識別子。 各履歴イベントは、ポリシーを実行しようとする1つの試行を表します。 条件には複数の条件式や複数の対象が含まれる場合があるため、1 つの history_id に対して複数の詳細レコードが作成されることもあります。 [History_id] 列を使用して、このビューを [syspolicy_policy_execution_history](../../relational-databases/system-catalog-views/syspolicy-policy-execution-history-transact-sql.md) ビューに結合します。|  
|target_query_expression|**nvarchar(max)**|ポリシーおよび syspolicy_policy_execution_history ビューの対象。|  
|execution_date|**datetime**|この詳細レコードが作成された日時。|  
|結果|**bit**|この対象と条件式の評価が成功したか失敗したかを表します。<br /><br /> 0 (成功) または 1 (失敗)。|  
|result_detail|**nvarchar(max)**|結果メッセージ。 ファセットによって提供される場合にのみ使用できます。|  
|exception_message|**nvarchar(max)**|例外が発生した場合は、例外によって生成されたメッセージ。|  
|exception|**nvarchar(max)**|例外が発生した場合の説明。|  
  
## <a name="remarks"></a>解説  
 ポリシー ベースの管理のトラブルシューティングを行う場合に、失敗した対象と条件式の組み合わせ、失敗した日時、および関連するエラーを調べるには、syspolicy_policy_execution_history_details ビューに対してクエリを実行します。  
  
 次のクエリでは、ビューとビューを組み合わせて、 `syspolicy_policy_execution_history_details` `syspolicy_policy_execution_history_details` `syspolicy_policies` ポリシーの名前、条件の名前、およびエラーの詳細を表示します。  
  
```  
SELECT Pol.name AS Policy,   
Cond.name AS Condition,   
PolHistDet.target_query_expression,   
PolHistDet.execution_date,   
PolHistDet.result,   
PolHistDet.result_detail,   
PolHistDet.exception_message,   
PolHistDet.exception   
FROM msdb.dbo.syspolicy_policies AS Pol  
JOIN msdb.dbo.syspolicy_conditions AS Cond  
    ON Pol.condition_id = Cond.condition_id  
JOIN msdb.dbo.syspolicy_policy_execution_history AS PolHist  
    ON Pol.policy_id = PolHist.policy_id  
JOIN msdb.dbo.syspolicy_policy_execution_history_details AS PolHistDet  
    ON PolHist.history_id = PolHistDet.history_id  
WHERE PolHistDet.result = 0 ;  
```  
  
## <a name="permissions"></a>アクセス許可  
 msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。  
  
## <a name="see-also"></a>参照  
 [ポリシーベースの管理を使用してサーバーを管理する](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [ポリシーベースの管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
