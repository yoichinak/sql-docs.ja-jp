---
description: sp_syspolicy_add_policy_category (Transact-SQL)
title: sp_syspolicy_add_policy_category (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_add_policy_category
- sp_syspolicy_add_policy_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_add_policy_category
ms.assetid: b682fac4-23c6-4662-8d05-c38f3b45507e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2722671523f14177a92084a4d896eec3ccdd6e2b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469168"
---
# <a name="sp_syspolicy_add_policy_category-transact-sql"></a>sp_syspolicy_add_policy_category (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ポリシー ベースの管理で使用できるポリシー カテゴリを追加します。 ポリシーカテゴリを使用すると、ポリシーを整理したり、ポリシーのスコープを設定したりできます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syspolicy_add_policy_category [ @name = ] 'name'  
    [ , [ @mandate_database_subscriptions = ] mandate_database_subscriptions ]  
    , [ @policy_category_id = ] policy_category_id OUTPUT  
```  
  
## <a name="arguments"></a>引数  
`[ @name = ] 'name'` ポリシーカテゴリの名前を指定します。 *名前* は **sysname**であり、必須です。 *名前* を NULL または空の文字列にすることはできません。  
  
`[ @mandate_database_subscriptions = ] mandate_database_subscriptions` データベースサブスクリプションがポリシーカテゴリに対して必須かどうかを決定します。 *mandate_database_subscriptions* は **ビット** 値で、既定値は 1 (有効) です。  
  
`[ @policy_category_id = ] policy_category_id` ポリシーカテゴリの識別子を示します。 *policy_category_id* は **INT**,、出力として返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 sp_syspolicy_add_policy_category は msdb システム データベースのコンテキストで実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 PolicyAdministratorRole 固定データベース ロールのメンバーシップが必要です。  
  
> [!IMPORTANT]  
>  資格情報が昇格される可能性について: PolicyAdministratorRole ロールに割り当てられているユーザーは、サーバー トリガーを作成して、[!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスの動作に影響する可能性があるポリシーの実行をスケジュールできます。 たとえば、PolicyAdministratorRole ロールに割り当てられているユーザーは、ほとんどのオブジェクトが[!INCLUDE[ssDE](../../includes/ssde-md.md)]で作成されないようにすることができるポリシーを作成できます。 このような資格情報が昇格される可能性があるため、Policy管理者ロールロールは、の構成の制御によって信頼されているユーザーのみに付与する必要があり [!INCLUDE[ssDE](../../includes/ssde-md.md)] ます。  
  
## <a name="examples"></a>例  
 次の例では、カテゴリに対するサブスクリプションが必須ではないポリシーカテゴリを作成します。 これは、カテゴリ内のポリシーをオプトインまたはオプトアウトするように個々のデータベースを構成できることを意味します。  
  
```  
DECLARE @policy_category_id int;  
  
EXEC msdb.dbo.sp_syspolicy_add_policy_category  
  @name = N'Table Naming Policies'  
, @mandate_database_subscriptions = 0  
, @policy_category_id = @policy_category_id OUTPUT;  
  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のポリシーベースの管理ストアドプロシージャ ](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_add_policy_category_subscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-add-policy-category-subscription-transact-sql.md)   
 [sp_syspolicy_delete_policy_category &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-delete-policy-category-transact-sql.md)  
  
  
