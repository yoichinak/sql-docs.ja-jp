---
description: sp_help_maintenance_plan (Transact-sql)
title: sp_help_maintenance_plan (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_maintenance_plan_TSQL
- sp_help_maintenance_plan
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_maintenance_plan
ms.assetid: e972a510-960e-41d6-93c5-c71cd581a585
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 99fe08406840229ded741160f855ed60f11e977a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89527696"
---
# <a name="sp_help_maintenance_plan-transact-sql"></a>sp_help_maintenance_plan (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定したメンテナンス プランに関する情報を返します。 プランが指定されていない場合、このストアドプロシージャは、すべてのメンテナンスプランに関する情報を返します。  
  
> **注:** このストアドプロシージャは、データベースメンテナンスプランで使用されます。 この機能は、このストアドプロシージャを使用しないメンテナンスプランに置き換えられました。 このプロシージャは、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からアップグレードしたプログラムでデータベース メンテナンス プランを管理する場合に使用します。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_maintenance_plan [ [ @plan_id = ] 'plan_id' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @plan_id = ] 'plan\_id'` メンテナンスプランのプラン ID を指定します。 *plan_id* は **UNIQUEIDENTIFIER**です。 既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
 *Plan_id*が指定されている場合、 **sp_help_maintenance_plan**は Plan、Database、Job という3つのテーブルを返します。  
  
### <a name="plan-table"></a>プランテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|メンテナンスプラン ID。|  
|**plan_name**|**sysname**|メンテナンスプランの名前。|  
|**date_created**|**datetime**|メンテナンスプランが作成された日付。|  
|**責任**|**sysname**|メンテナンスプランの所有者。|  
|**max_history_rows**|**int**|システムテーブルのメンテナンスプランの履歴を記録するために割り当てられる行の最大数。|  
|**remote_history_server**|**int**|履歴レポートが書き込まれるリモートサーバーの名前。|  
|**max_remote_history_rows**|**int**|履歴レポートを書き込むことができるリモートサーバー上のシステムテーブルに割り当てられた行の最大数。|  
|**user_defined_1**|**int**|既定値は NULL です。|  
|**user_defined_2**|**nvarchar (100)**|既定値は NULL です。|  
|**user_defined_3**|**datetime**|既定値は NULL です。|  
|**user_defined_4**|**uniqueidentifier**|既定値は NULL です。|  
  
### <a name="database-table"></a>データベース テーブル  
  
|列名|説明|  
|-----------------|-----------------|  
|**database_name**|メンテナンスプランに関連付けられているすべてのデータベースの名前。 *database_name* は **sysname** です。|  
  
### <a name="job-table"></a>ジョブテーブル  
  
|列名|説明|  
|-----------------|-----------------|  
|**job_id**|メンテナンスプランに関連付けられているすべてのジョブの ID。 *job_id* は **uniqueidentifier**です。|  
  
## <a name="remarks"></a>解説  
 **sp_help_maintenance_plan** は **msdb** データベースにあります。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_help_maintenance_plan**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="examples"></a>例  
 この例では、メンテナンスプランの FAD6F2AB-3571-11D3-9D4A-00C04FB925FC について説明します。  
  
```  
EXECUTE   sp_help_maintenance_plan   
   N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC';  
```  
  
## <a name="see-also"></a>参照  
 [メンテナンス プラン](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [データベースメンテナンスプランのストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
