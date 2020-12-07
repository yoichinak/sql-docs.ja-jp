---
description: sp_help_downloadlist (Transact-SQL)
title: sp_help_downloadlist (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_downloadlist_TSQL
- sp_help_downloadlist
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_downloadlist
ms.assetid: 745b265b-86e8-4399-b928-c6969ca1a2c8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2196e6fbbbd0089c7e65592bfc4ebfd17bb14239
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549732"
---
# <a name="sp_help_downloadlist-transact-sql"></a>sp_help_downloadlist (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定されたジョブの **sysdownloadlist** システムテーブル内のすべての行、またはジョブが指定されていない場合はすべての行を一覧表示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_downloadlist { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }   
     [ , [ @operation = ] 'operation' ]   
     [ , [ @object_type = ] 'object_type' ]   
     [ , [ @object_name = ] 'object_name' ]   
     [ , [ @target_server = ] 'target_server' ]   
     [ , [ @has_error = ] has_error ]   
     [ , [ @status = ] status ]   
     [ , [ @date_posted = ] date_posted ]  
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id` 情報を返すジョブの識別番号を指定します。 *job_id* は **uniqueidentifier**,、既定値は NULL です。  
  
`[ @job_name = ] 'job_name'` ジョブの名前。 *job_name* は **sysname**,、既定値は NULL です。  
  
> [!NOTE]  
>  *Job_id*または*job_name*のいずれかを指定する必要がありますが、両方を指定することはできません。  
  
`[ @operation = ] 'operation'` 指定されたジョブの有効な操作です。 *操作* は **varchar (64)**,、既定値は NULL の場合、これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**不具合**|マスター **SQLServerAgent** サービスからの参加を解除する対象サーバーを要求するサーバー操作。|  
|**DELETE**|ジョブ全体を削除するジョブ操作。|  
|**INSERT**|ジョブ全体の追加、または既存のジョブの更新を行うジョブ操作。 この操作には、すべてのジョブステップとスケジュールが含まれます (該当する場合)。|  
|**再参加**|ターゲット サーバーで参加情報の再送信を行うためのサーバー操作。この情報にはマルチサーバー ドメインのポーリング間隔やタイム ゾーンも含まれます。 ターゲットサーバーは、 **MSXOperator** の詳細も再ダウンロードします。|  
|**SET-POLL**|ターゲット サーバーがマルチサーバー ドメインを呼び出す間隔を秒単位で設定するサーバー操作。 *値*を指定すると、必要な間隔の値として解釈され、 **10** ~ **28800**の値を指定できます。|  
|**着手**|ジョブ実行の開始を要求するジョブ操作。|  
|**停止**|ジョブの実行の停止を要求するジョブ操作。|  
|**SYNC-TIME**|対象サーバーがマルチサーバードメインとシステムクロックを同期させるサーバー操作。 これはコストのかかる操作なので、この操作は限られた頻度で実行します。|  
|**UPDATE**|ジョブステップまたはスケジュールではなく、ジョブの **sysjobs** 情報のみを更新するジョブ操作。 は、 **sp_update_job**によって自動的に呼び出されます。|  
  
`[ @object_type = ] 'object_type'` 指定されたジョブのオブジェクトの種類です。 *object_type* は **varchar (64)**,、既定値は NULL です。 *object_type* には、ジョブまたはサーバーを指定できます。 有効な *object_type*値の詳細については、「 [transact-sql&#41;&#40;sp_add_category ](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md)」を参照してください。  
  
`[ @object_name = ] 'object_name'` オブジェクトの名前。 *object_name* は **sysname**,、既定値は NULL です。 *Object_type*が job の場合は、 *object_name*がジョブ名になります。 *Object_type*が server の場合、 *object_name*はサーバー名です。  
  
`[ @target_server = ] 'target_server'` 対象サーバーの名前。 *target_server* は **nvarchar (128)**,、既定値は NULL です。  
  
`[ @has_error = ] has_error` ジョブがエラーを認識するかどうかを指定します。 *has_error* は **tinyint**,、既定値は NULL の場合は、エラーを確認する必要がないことを示します。 **1** は、すべてのエラーを確認する必要があることを示します。  
  
`[ @status = ] status` ジョブの状態。 *状態* は **tinyint**,、既定値は NULL です。  
  
`[ @date_posted = ] date_posted` 指定した日付と時刻以降に行われたすべてのエントリが結果セットに含まれる日付と時刻。 *date_posted* は **datetime**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|命令の一意な整数識別番号。|  
|**source_server**|**nvarchar(30)**|命令の送信元のサーバーのコンピューター名。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バージョン7.0 では、これは常にマスター (MSX) サーバーのコンピューター名です。|  
|**operation_code**|**nvarchar (4000)**|命令の操作コード。|  
|**object_name**|**sysname**|命令によって影響を受けるオブジェクト。|  
|**object_id**|**uniqueidentifier**|命令によって影響を受けるオブジェクトの識別番号 (ジョブオブジェクトの場合は**job_id** 、サーバーオブジェクトの場合は 0x00)、または **operation_code**に固有のデータ値。|  
|**target_server**|**nvarchar(30)**|この命令をダウンロードする対象サーバー。|  
|**error_message**|**nvarchar(1024)**|この命令の処理中に問題が発生した場合の、ターゲット サーバーからのエラー メッセージ (存在する場合)。<br /><br /> 注: すべてのエラーメッセージは、対象サーバーによるすべてのダウンロードをブロックします。|  
|**date_posted**|**datetime**|命令がテーブルにポストされた日付。|  
|**date_downloaded**|**datetime**|ターゲット サーバーが命令をダウンロードした日付。|  
|**status**|**tinyint**|ジョブの状態:<br /><br /> **0** = まだダウンロードされていません<br /><br /> **1** = ダウンロードが正常に完了しました。|  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの実行権限は、既定では **sysadmin** 固定サーバー ロールのメンバーに与えられています。  
  
## <a name="examples"></a>例  
 次の例では、`sysdownloadlist` 内の `NightlyBackups` ジョブに関する行を一覧表示します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_downloadlist  
    @job_name = N'NightlyBackups',  
    @operation = N'UPDATE',   
    @object_type = N'JOB',   
    @object_name = N'NightlyBackups',  
    @target_server = N'SEATTLE2',   
    @has_error = 1,   
    @status = NULL,   
    @date_posted = NULL ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
