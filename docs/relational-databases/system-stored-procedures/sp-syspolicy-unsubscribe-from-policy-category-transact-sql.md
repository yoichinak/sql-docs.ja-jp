---
description: sp_syspolicy_unsubscribe_from_policy_category (Transact-sql)
title: sp_syspolicy_unsubscribe_from_policy_category (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sp_syspolicy_unsubscribe_from_policy_category_TSQL
- sp_syspolicy_unsubscribe_from_policy_category
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_unsubscribe_from_policy_category
ms.assetid: 47abab63-e605-40e8-a54e-2241e2e01afd
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: be5008e3b86cd752bc7cfe5794b07ca875e62952
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99161302"
---
# <a name="sp_syspolicy_unsubscribe_from_policy_category-transact-sql"></a>sp_syspolicy_unsubscribe_from_policy_category (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベースのポリシーカテゴリのサブスクリプションを削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syspolicy_unsubscribe_from_policy_category [ @policy_category = ] 'policy_category'  
```  
  
## <a name="arguments"></a>引数  
`[ @policy_category = ] 'policy_category'` 削除するポリシーカテゴリのサブスクリプションの名前を指定します。 *policy_category* は **sysname** であり、必須です。  
  
 *Policy_category* の値を取得するには、msdb.dbo.syspolicy_policy_categories システムビューに対してクエリを実行します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>コメント  
 sp_syspolicy_unsubscribe_from_policy_category は、ポリシー カテゴリのサブスクリプションを削除するデータベースのコンテキストで実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 db_owner 固定データベース ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、指定したデータベースの 'Finance' ポリシーのカテゴリに対するサブスクリプションを削除します。  
  
```  
USE <database_name>;  
  
EXEC sys.sp_syspolicy_unsubscribe_from_policy_category @policy_category = N'Finance';  
  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のポリシーベースの管理ストアドプロシージャ ](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_subscribe_to_policy_category &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-subscribe-to-policy-category-transact-sql.md)  
  
  
