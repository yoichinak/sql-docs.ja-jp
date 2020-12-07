---
description: sp_syspolicy_delete_policy_execution_history (Transact-SQL)
title: sp_syspolicy_delete_policy_execution_history (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_delete_policy_execution_history
- sp_syspolicy_delete_policy_execution_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_delete_policy_execution_history
ms.assetid: fe651af9-267e-45ec-b4e7-4b0698fb1be3
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 99a17425f74b1ae2f5db7c4a6002e27ca7780f21
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485628"
---
# <a name="sp_syspolicy_delete_policy_execution_history-transact-sql"></a>sp_syspolicy_delete_policy_execution_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ポリシーベースの管理のポリシーの実行履歴を削除します。 このストアド プロシージャを使用して、特定のポリシーまたはすべてのポリシーの実行履歴、および特定の日付までの実行履歴を削除できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syspolicy_delete_policy_execution_history [ @policy_id = ] policy_id ]  
    [ , [ @oldest_date = ] 'oldest_date' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @policy_id = ] policy_id` 実行履歴を削除するポリシーの識別子を指定します。 *policy_id* は **int**であり、が必要です。 NULL にすることができます。  
  
`[ @oldest_date = ] 'oldest_date'` ポリシーの実行履歴を保持する最も古い日付を指定します。 この日付より前の実行履歴は削除されます。 *oldest_date* は **datetime**であり、必須です。 NULL にすることができます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 sp_syspolicy_delete_policy_execution_history は msdb システム データベースのコンテキストで実行する必要があります。  
  
 *Policy_id*の値を取得し、実行履歴の日付を表示するには、次のクエリを使用できます。  
  
```  
SELECT a.name AS N'policy_name', b.policy_id, b.start_date, b.end_date  
FROM msdb.dbo.syspolicy_policies AS a   
INNER JOIN msdb.dbo.syspolicy_policy_execution_history AS b  
ON a.policy_id = b.policy_id  
```  
  
 次の動作は、1つまたは両方の値に NULL を指定した場合に適用されます。  
  
-   すべてのポリシー実行履歴を削除するには、 *policy_id* と *oldest_date*の両方に NULL を指定します。  
  
-   特定のポリシーのポリシー実行履歴をすべて削除するには、 *policy_id*のポリシー識別子を指定し、 *oldest_date*として NULL を指定します。  
  
-   特定の日付より前のすべてのポリシーのポリシー実行履歴を削除するには、 *policy_id*に NULL を指定し、 *oldest_date*の日付を指定します。  
  
 ポリシーの実行履歴をアーカイブするには、オブジェクト エクスプローラーでポリシー履歴ログを開いて、実行履歴をファイルにエクスポートします。 ポリシー履歴ログにアクセスするには、[ **管理**] を展開し、[ **ポリシー管理**] を右クリックして、[ **履歴の表示**] をクリックします。  
  
## <a name="permissions"></a>アクセス許可  
 PolicyAdministratorRole 固定データベース ロールのメンバーシップが必要です。  
  
> [!IMPORTANT]  
>  資格情報が昇格される可能性について: PolicyAdministratorRole ロールに割り当てられているユーザーは、サーバー トリガーを作成して、[!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスの動作に影響する可能性があるポリシーの実行をスケジュールできます。 たとえば、PolicyAdministratorRole ロールに割り当てられているユーザーは、ほとんどのオブジェクトが[!INCLUDE[ssDE](../../includes/ssde-md.md)]で作成されないようにすることができるポリシーを作成できます。 このような資格情報が昇格される可能性があるため、Policy管理者ロールロールは、の構成の制御によって信頼されているユーザーのみに付与する必要があり [!INCLUDE[ssDE](../../includes/ssde-md.md)] ます。  
  
## <a name="examples"></a>例  
 次の例では、ID が 7 のポリシーについて特定の日付より前のポリシーの実行履歴を削除します。  
  
```  
EXEC msdb.dbo.sp_syspolicy_delete_policy_execution_history @policy_id = 7  
, @oldest_date = '2009-02-16 16:00:00.000';  
  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [Transact-sql&#41;&#40;のポリシーベースの管理ストアドプロシージャ ](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_set_config_history_retention &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-config-history-retention-transact-sql.md)   
 [sp_syspolicy_purge_history &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-purge-history-transact-sql.md)  
  
  
