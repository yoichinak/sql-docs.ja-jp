---
description: sp_syspolicy_configure (Transact-sql)
title: sp_syspolicy_configure (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_configure
- sp_syspolicy_configure_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_configure
ms.assetid: 70c10922-9345-4190-ba69-808a43f760da
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 820952e0829014efc3669759dabf5d1dfc208d91
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473588"
---
# <a name="sp_syspolicy_configure-transact-sql"></a>sp_syspolicy_configure (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ポリシー ベースの管理を有効にするかどうかなど、ポリシー ベースの管理の設定を構成します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syspolicy_configure [ @name = ] 'name'  
    , [ @value = ] value  
```  
  
## <a name="arguments"></a>引数  
`[ @name = ] 'name'` 構成する設定の名前を指定します。 *名前* は **sysname**であり、必須であり、NULL または空の文字列にすることはできません。  
  
 *名前* には、次のいずれかの値を指定できます。  
  
-   'Enabled' : ポリシー ベースの管理を有効にするかどうかを指定します。  
  
-   'HistoryRetentionInDays' : ポリシー評価履歴を保持する日数を指定します。 0 に設定した場合、履歴は自動的には削除されません。  
  
-   ' LogOnSuccess '-ポリシーベースの管理ログが成功したポリシー評価をログに記録するかどうかを指定します。  
  
`[ @value = ] value`*Name*に指定された値に関連付けられている値を指定します。 *値* が **sql_variant**であり、が必要です。  
  
-   *名前*に ' Enabled ' を指定した場合は、次のいずれかの値を使用できます。  
  
    -   0 = ポリシー ベースの管理を無効にします。  
  
    -   1 = ポリシー ベースの管理を有効にします。  
  
-   *名前*に ' HistoryRententionInDays ' を指定する場合は、日数を整数値として指定します。  
  
-   *名前*に "logonsuccess" を指定した場合は、次のいずれかの値を使用できます。  
  
    -   0 = 失敗したポリシー評価のみをログに記録します。  
  
    -   1 = 成功したポリシー評価と失敗したポリシー評価の両方をログに記録します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 msdb システム データベースのコンテキストで sp_syspolicy_configure を実行する必要があります。  
  
 これらの設定の現在の値を表示するには、msdb.dbo.syspolicy_configuration システムビューに対してクエリを実行します。  
  
## <a name="permissions"></a>アクセス許可  
 PolicyAdministratorRole 固定データベース ロールのメンバーシップが必要です。  
  
> [!IMPORTANT]  
>  資格情報が昇格される可能性について: PolicyAdministratorRole ロールに割り当てられているユーザーは、サーバー トリガーを作成して、[!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスの動作に影響する可能性があるポリシーの実行をスケジュールできます。 たとえば、PolicyAdministratorRole ロールに割り当てられているユーザーは、ほとんどのオブジェクトが[!INCLUDE[ssDE](../../includes/ssde-md.md)]で作成されないようにすることができるポリシーを作成できます。 このような資格情報が昇格される可能性があるため、Policy管理者ロールロールは、の構成の制御によって信頼されているユーザーのみに付与する必要があり [!INCLUDE[ssDE](../../includes/ssde-md.md)] ます。  
  
## <a name="examples"></a>例  
 次の例では、ポリシーベースの管理を有効にします。  
  
```  
EXEC msdb.dbo.sp_syspolicy_configure @name = N'Enabled'  
, @value = 1;  
  
GO  
```  
  
 次の例では、ポリシー履歴の保有期間を14日間に設定します。  
  
```  
EXEC msdb.dbo.sp_syspolicy_configure @name = N'HistoryRetentionInDays'  
, @value = 14;  
  
GO  
```  
  
 次の例では、成功したポリシー評価と失敗したポリシー評価の両方をログに記録するようにポリシー ベースの管理を構成します。  
  
```  
EXEC msdb.dbo.sp_syspolicy_configure @name = N'LogOnSuccess'  
, @value = 1;  
  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のポリシーベースの管理ストアドプロシージャ ](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_set_config_enabled &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-config-enabled-transact-sql.md)   
 [sp_syspolicy_set_config_history_retention &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-config-history-retention-transact-sql.md)   
 [sp_syspolicy_set_log_on_success &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-log-on-success-transact-sql.md)  
  
  
