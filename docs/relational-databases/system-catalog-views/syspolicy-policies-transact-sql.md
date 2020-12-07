---
description: syspolicy_policies (Transact-sql)
title: syspolicy_policies (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_policies_TSQL
- syspolicy_policies
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policies view
ms.assetid: aecf35bb-187e-4f80-870f-48081b88974e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e56ab498d2502bcb7130ab2406a390d8bbd1055a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419806"
---
# <a name="syspolicy_policies-transact-sql"></a>syspolicy_policies (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのポリシー ベースの管理ポリシーごとに 1 つの行を表示します。 syspolicy_policies は、msdb データベースの dbo スキーマに属しています。 次の表では、syspolicy_policies ビューの列について説明します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|policy_id|**int**|ポリシーの識別子。|  
|name|**sysname**|ポリシーの名前。|  
|condition_id|**int**|このポリシーによって適用またはテストされた条件の ID。|  
|root_condition_id|**int**|内部使用のみ。|  
|date_created|**datetime**|ポリシーが作成された日時。|  
|execution_mode|**int**|ポリシーの評価モード。 使用できる値は次のとおりです。<br /><br /> 0 = 要求時<br /><br /> このモードでは、ユーザーが直接指定した場合にポリシーが評価されます。<br /><br /> 1 = 変更時: 回避<br /><br /> この自動モードでは、DDL トリガーを使用してポリシー違反が防止されます。<br /><br /> 2 = 変更時: ログのみ<br /><br /> この自動モードでは、イベント通知を使用して、関連する変更が発生したときにポリシーを評価し、ポリシー違反をログに記録します。<br /><br /> 4 = スケジュールに基づいて<br /><br /> この自動モードでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを使用してポリシーが定期的に評価されます。 モードでは、ポリシー違反がログに記録されます。<br /><br /> 注: 値3は有効な値ではありません。|  
|policy_category|**int**|このポリシーが属するポリシー ベースの管理のポリシー カテゴリの ID。 既定のポリシー グループの場合は NULL です。|  
|schedule_uid|**uniqueidentifier**|execution_mode が "スケジュールで実行" の場合にスケジュールの ID が格納されます。それ以外の場合は NULL です。|  
|description|**nvarchar(max)**|ポリシーの説明。 この説明の列は省略可能であり、NULL の場合もあります。|  
|help_text|**nvarchar (4000)**|help_link に属するハイパーリンク テキスト。|  
|help_link|**nvarchar (2083)**|ポリシー作成者によってポリシーに割り当てられた追加のヘルプハイパーリンク。|  
|object_set_id|**int**|ポリシーが評価するオブジェクト セットの ID。|  
|is_enabled|**bit**|ポリシーが現在有効になっている (1) か、無効 (0) かを示します。|  
|job_id|**uniqueidentifier**|execution_mode が "スケジュールで実行" の場合に、ポリシーを実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブの ID が格納されます。|  
|created_by|**sysname**|ポリシーを作成したログイン。|  
|modified_by|**sysname**|ポリシーを最後に変更したログイン。 変更されていない場合は NULL になります。|  
|date_modified|**datetime**|ポリシーが作成された日時。 変更されていない場合は NULL になります。|  
  
## <a name="remarks"></a>解説  
 ポリシーベースの管理のトラブルシューティングを行うときは、 [syspolicy_conditions](../../relational-databases/system-catalog-views/syspolicy-conditions-transact-sql.md) ビューに対してクエリを実行し、ポリシーが有効になっているかどうかを確認します。 このビューには、ポリシーを作成または最後に変更したユーザーも表示されます。  
  
## <a name="permissions"></a>アクセス許可  
 msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。  
  
## <a name="see-also"></a>参照  
 [ポリシーベースの管理を使用してサーバーを管理する](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [ポリシーベースの管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
