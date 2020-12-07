---
description: sys.sp_cdc_add_job (Transact-SQL)
title: sp_cdc_add_job (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_add_job_TSQL
- sys.sp_cdc_add_job
- sys.sp_cdc_add_job_TSQL
- sp_cdc_add_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_add_job
ms.assetid: c4458738-ed25-40a6-8294-a26ca5a05bd9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c8a1285df9bf4d7e17e074e3c22f0ff37241c400
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545845"
---
# <a name="syssp_cdc_add_job-transact-sql"></a>sys.sp_cdc_add_job (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベースに、変更データキャプチャのクリーンアップジョブまたはキャプチャジョブを作成します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.sp_cdc_add_job [ @job_type = ] 'job_type'  
    [ , [ @start_job = ] start_job ]   
    [ , [ @maxtrans = ] max_trans ]   
    [ , [ @maxscans = ] max_scans ]   
    [ , [ @continuous = ] continuous ]   
    [ , [ @pollinginterval = ] polling_interval ]   
    [ , [ @retention ] = retention ]   
    [ , [ @threshold ] = 'delete_threshold' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @job_type = ] 'job\_type'` 追加するジョブの種類。 *job_type* は **nvarchar (20)** であり、NULL にすることはできません。 有効な入力は **' capture '** と **' cleanup '** です。  
  
`[ @start_job = ] start_job` ジョブが追加された直後にジョブを開始するかどうかを示すフラグです。 *start_job* の部分は **bit** で、既定値は1です。  
  
`[ @maxtrans ] = max_trans` 各スキャンサイクルで処理するトランザクションの最大数。 *max_trans* は **int** で、既定値は500です。 指定する場合、値は正の整数である必要があります。  
  
 *max_trans* は、キャプチャジョブに対してのみ有効です。  
  
`[ @maxscans ] = max\_scans_` ログからすべての行を抽出するために実行するスキャンサイクルの最大数。 *max_scans* は **int** で、既定値は10です。  
  
 *max_scan* は、キャプチャジョブに対してのみ有効です。  
  
`[ @continuous ] = continuous_` キャプチャジョブを連続的に実行するか (1)、1回だけ実行するか (0) を示します。 *continuous* は **bit** で、既定値は1です。  
  
 *Continuous* = 1 の場合、 [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md)ジョブによってログがスキャンされ、最大 (*max_trans* \* *max_scans*) トランザクションが処理されます。 次に、 *polling_interval* で指定された秒数だけ待機してから、次のログスキャンを開始します。  
  
 *Continuous* = 0 の場合、 **sp_cdc_scan**ジョブはログの*max_scans*スキャンまで実行され、各スキャン中に*max_trans*トランザクションまで処理された後、終了します。  
  
 *continuous* は、キャプチャジョブに対してのみ有効です。  
  
`[ @pollinginterval ] = polling\_interval_` ログスキャンサイクルの間隔を秒数で指定します。 *polling_interval* は **bigint** で、既定値は5です。  
  
 *polling_interval* は、 *continuous* が1に設定されている場合にのみ、キャプチャジョブに対して有効です。 指定する場合、値は0以上で24時間未満 (最大: 86399 秒) にする必要があります。 値 0 を指定した場合、ログ スキャンの間に待機時間はありません。  
  
`[ @retention ] = retention_` 変更データ行が変更テーブルに保持される時間 (分単位)。 *リテンション期間* は **bigint** で、既定値は 4320 (72 時間) です。 最大値は 52494800 (100 年) です。 指定する場合、値は正の整数である必要があります。  
  
 *リテンション期間* はクリーンアップジョブに対してのみ有効です。  
  
`[ @threshold = ] 'delete\_threshold'` クリーンアップ時に1つのステートメントを使用して削除できる削除エントリの最大数。 *delete_threshold* は **bigint** で、既定値は5000です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 クリーンアップジョブは、データベースの最初のテーブルで変更データキャプチャが有効になっている場合に、既定値を使用して作成されます。 キャプチャ ジョブは、データベースの最初のテーブルの変更データ キャプチャを有効にしたとき、そのデータベースにトランザクション パブリケーションが存在しなかった場合に、既定値を使って作成されます。 トランザクション パブリケーションが存在する場合、トランザクション ログ リーダーを使ってキャプチャ メカニズムが実現されます。別個のキャプチャ ジョブは必要ありません (使用することもできません)。  
  
 クリーンアップ ジョブとキャプチャ ジョブは既定で作成されるため、このストアド プロシージャが必要となるのは、ジョブを明示的に削除した後で、再び作成する必要が生じた場合だけです。  
  
 ジョブの名前は**cdc です。** _\<database\_name\>_** \_ クリーンアップ**または**cdc。** _\<database\_name\>_** \_ capture**。ここで *<database_name>* は現在のデータベースの名前です。 同じ名前のジョブが既に存在する場合、名前にはピリオド (**.**) と一意の識別子 (例: cdc) が付加されます。 **AdventureWorks_capture。A1ACBDED-13FC-428C-8302-10100EF74F52**。  
  
 クリーンアップジョブまたはキャプチャジョブの現在の構成を表示するには、 [sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)を使用します。 ジョブの構成を変更するには、 [sp_cdc_change_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md)を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Db_owner**固定データベースロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-creating-a-capture-job"></a>A. キャプチャ ジョブを作成する  
 次の例では、キャプチャ ジョブを作成します。 明示的に削除された既存のクリーンアップ ジョブを改めて作成するという状況を想定しています。 ジョブは既定値を使って作成されます。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_add_job @job_type = N'capture';  
GO  
```  
  
### <a name="b-creating-a-cleanup-job"></a>B. クリーンアップジョブの作成  
 次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースにクリーンアップ ジョブを作成します。 パラメーター `@start_job` は 0 に、`@retention` は 5760 分 (96 時間) に設定します。 明示的に削除された既存のクリーンアップ ジョブを改めて作成するという状況を想定しています。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_add_job  
     @job_type = N'cleanup'  
    ,@start_job = 0  
    ,@retention = 5760;  
```  
  
## <a name="see-also"></a>参照  
 [dbo. cdc_jobs &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sp_cdc_enable_table &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [変更データ キャプチャについて &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
