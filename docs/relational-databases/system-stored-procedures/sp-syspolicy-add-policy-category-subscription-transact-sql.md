---
description: sp_syspolicy_add_policy_category_subscription (Transact-SQL)
title: sp_syspolicy_add_policy_category_subscription (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sp_syspolicy_add_policy_category_subscription
- sp_syspolicy_add_policy_category_subscription_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_add_policy_category_subscription
ms.assetid: 4284f550-9a3f-4726-8181-15e407fbf08f
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 279cec943ce0e93556442c3ec29c2139764e078c
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99195965"
---
# <a name="sp_syspolicy_add_policy_category_subscription-transact-sql"></a>sp_syspolicy_add_policy_category_subscription (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ポリシー カテゴリのサブスクリプションを、指定したデータベースに追加します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syspolicy_add_policy_category_subscription [ @target_type = ] 'target_type'  
    , [ @target_object = ] 'target_object'  
    , [ @policy_category = ] 'policy_category'  
    [ , [ @policy_category_subscription_id = ] policy_category_subscription_id OUTPUT ]  
```  
  
## <a name="arguments"></a>引数  
`[ @target_type = ] 'target_type'` カテゴリサブスクリプションの対象の種類を示します。 *target_type* は **sysname** であり、必須であり、' DATABASE ' に設定する必要があります。  
  
`[ @target_object = ] 'target_object'` カテゴリをサブスクライブするデータベースの名前を指定します。 *target_object* は **sysname** であり、必須です。  
  
`[ @policy_category = ] 'policy_category'` サブスクライブするポリシーカテゴリの名前を指定します。 *policy_category* は **sysname** であり、必須です。  
  
 *Policy_category* の値を取得するには、msdb.dbo.syspolicy_policy_categories システムビューに対してクエリを実行します。  
  
`[ @policy_category_subscription_id = ] policy_category_subscription_id` カテゴリサブスクリプションの識別子を示します。 *policy_category_subscription_id* は **INT**,、出力として返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>コメント  
 sp_syspolicy_add_policy_category_subscription は msdb システム データベースのコンテキストで実行する必要があります。  
  
 存在しないポリシー カテゴリを指定すると、新しいポリシー カテゴリが作成され、ストアド プロシージャの実行時にすべてのデータベースに対してサブスクリプションが要求されます。 新しいカテゴリに要求されたサブスクリプションをクリアすると、そのサブスクリプションは、 *target_object* で指定したデータベースにのみ適用されます。 要求されたサブスクリプションの設定を変更する方法の詳細については、「[sp_syspolicy_update_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-transact-sql.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャは、ストアド プロシージャの現在の所有者のコンテキストで実行されます。  
  
## <a name="examples"></a>例  
 次の例では、'Table Naming Policies' という名前のポリシー カテゴリをサブスクライブするように指定したデータベースを構成します。  
  
```  
EXEC msdb.dbo.sp_syspolicy_add_policy_category_subscription @target_type = N'DATABASE'  
, @target_object = N'AdventureWorks2012'  
, @policy_category = N'Table Naming Policies';  
  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のポリシーベースの管理ストアドプロシージャ ](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_update_policy_category_subscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-subscription-transact-sql.md)   
 [sp_syspolicy_unsubscribe_from_policy_category &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-unsubscribe-from-policy-category-transact-sql.md)  
  
  
