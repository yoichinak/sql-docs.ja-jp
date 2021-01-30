---
description: sp_syspolicy_set_config_history_retention (Transact-sql)
title: sp_syspolicy_set_config_history_retention (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sp_syspolicy_set_config_history_retention_TSQL
- sp_syspolicy_set_config_history_retention
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_set_config_history_retention
ms.assetid: 2574898a-e724-4447-b96c-ff778471339d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: a7f5df1b06ee2f0ecacc4f90e732f86f1ef58f08
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99203182"
---
# <a name="sp_syspolicy_set_config_history_retention-transact-sql"></a>sp_syspolicy_set_config_history_retention (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ポリシー ベースの管理のポリシーの評価履歴を保持する日数を指定します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syspolicy_set_config_history_retention [ @value = ] value  
```  
  
## <a name="arguments"></a>引数  
`[ @value = ] value` ポリシーベースの管理履歴を保持する日数を指定します。 *値* は **sqlvariant** です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>コメント  
 msdb システム データベースのコンテキストで sp_syspolicy_set_config_history_retention を実行する必要があります。  
  
 *値* が0に設定されている場合、履歴は自動的には削除されません。  
  
 履歴の保有期間の現在の値を表示するには、次のクエリを実行します。  
  
```  
SELECT current_value FROM msdb.dbo.syspolicy_configuration  
WHERE name = 'HistoryRetentionInDays'  
```  
  
## <a name="permissions"></a>アクセス許可  
 PolicyAdministratorRole 固定データベース ロールのメンバーシップが必要です。  
  
> [!IMPORTANT]  
>  資格情報が昇格される可能性について: PolicyAdministratorRole ロールに割り当てられているユーザーは、サーバー トリガーを作成して、[!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスの動作に影響する可能性があるポリシーの実行をスケジュールできます。 たとえば、PolicyAdministratorRole ロールに割り当てられているユーザーは、ほとんどのオブジェクトが[!INCLUDE[ssDE](../../includes/ssde-md.md)]で作成されないようにすることができるポリシーを作成できます。 このような資格情報が昇格される可能性があるため、Policy管理者ロールロールは、の構成の制御によって信頼されているユーザーのみに付与する必要があり [!INCLUDE[ssDE](../../includes/ssde-md.md)] ます。  
  
## <a name="examples"></a>例  
 次の例では、ポリシーの評価履歴の保有期間を 28 日に設定します。  
  
```  
EXEC msdb.dbo.sp_syspolicy_set_config_history_retention @value = 28;  
  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のポリシーベースの管理ストアドプロシージャ ](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_configure &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-configure-transact-sql.md)  
  
  
