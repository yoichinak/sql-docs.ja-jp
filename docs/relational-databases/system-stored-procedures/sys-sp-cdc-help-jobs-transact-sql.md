---
description: sp_cdc_help_jobs (Transact-sql)
title: sp_cdc_help_jobs (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_help_jobs
- sys.sp_cdc_help_jobs_TSQL
- sp_cdc_help_jobs_TSQL
- sys.sp_cdc_help_jobs
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_help_jobs
ms.assetid: 9399b4bc-8293-408f-b3cb-f904e0657fb5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6a051301d812b06ab2170519cb54ea6f528490b7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544716"
---
# <a name="syssp_cdc_help_jobs-transact-sql"></a>sp_cdc_help_jobs (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベースを対象に、変更データ キャプチャのすべてのクリーンアップ ジョブまたはキャプチャ ジョブについての情報をレポートします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.sp_cdc_help_jobs  
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|ジョブの ID。|  
|**job_type**|**nvarchar (20)**|ジョブの種類。|  
|**maxtrans**|**int**|各スキャンサイクルで処理するトランザクションの最大数。<br /><br /> **maxtrans** はキャプチャジョブでのみ有効です。|  
|**maxscans**|**int**|ログからすべての行を抽出するために実行する最大スキャン サイクル数。<br /><br /> **maxscans** は、キャプチャジョブに対してのみ有効です。|  
|**連続**|**bit**|キャプチャ ジョブを連続的に実行するか (1)、1 回だけ実行するか (0) を示すフラグ。 詳細については、「 [sys. sp_cdc_add_job &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)」を参照してください。<br /><br /> **continuous** は、キャプチャジョブに対してのみ有効です。|  
|**pollinginterval**|**bigint**|ログ スキャン サイクル間の秒数。<br /><br /> **pollinginterval** はキャプチャジョブに対してのみ有効です。|  
|**保有**|**bigint**|変更行が変更テーブルに保持される時間 (分単位)。<br /><br /> **リテンション期間** はクリーンアップジョブに対してのみ有効です。|  
|**threshold**|**bigint**|クリーンアップ時に1つのステートメントを使用して削除できる削除エントリの最大数。|  
  
## <a name="permissions"></a>アクセス許可  
 **Db_owner**固定データベースロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例は、`AdventureWorks2012` データベースに定義されているキャプチャ ジョブおよびクリーンアップ ジョブについての情報を返します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_help_jobs;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [dbo. cdc_jobs &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
