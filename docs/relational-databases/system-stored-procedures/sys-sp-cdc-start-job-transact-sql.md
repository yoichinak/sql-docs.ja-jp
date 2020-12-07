---
description: sp_cdc_start_job (Transact-sql)
title: sp_cdc_start_job (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_start_job
- sp_cdc_start_job_TSQL
- sys.sp_cdc_start_job_TSQL
- sys.sp_cdc_start_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_start_job
ms.assetid: cf443a67-7705-4799-9f39-0e3a6a8a0708
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7cf53ef2241dbeef0fc499050c594e8efe735580
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541086"
---
# <a name="syssp_cdc_start_job-transact-sql"></a>sp_cdc_start_job (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベースの変更データキャプチャのクリーンアップジョブまたはキャプチャジョブを開始します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.sp_cdc_start_job [ [ @job_type = ] 'job_type' ]  
```  
  
## <a name="arguments"></a>引数  
`[ [ @job_type = ] 'job_type' ]` 追加するジョブの種類。 *job_type* は **nvarchar (20)** で、既定値は **capture**です。 有効な入力は **キャプチャ** と **クリーンアップ**です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 管理者は sys.sp_cdc_start_job を使用してキャプチャ ジョブまたはクリーンアップ ジョブのいずれかを明示的に開始できます。  
  
## <a name="permissions"></a>アクセス許可  
 db_owner 固定データベース ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-starting-a-capture-job"></a>A. キャプチャジョブの開始  
 次の例では、`AdventureWorks2012` データベースのキャプチャ ジョブを開始します。 既定のジョブの種類は**capture**であるため、 *job_type*に値を指定する必要はありません。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_start_job;  
GO  
```  
  
### <a name="b-starting-a-cleanup-job"></a>B. クリーンアップジョブの開始  
 次の例では、データベースのクリーンアップジョブを開始し `AdventureWorks2012` ます。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_start_job @job_type = N'cleanup';  
```  
  
## <a name="see-also"></a>参照  
 [dbo. cdc_jobs &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sp_cdc_stop_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-stop-job-transact-sql.md)  
  
  
