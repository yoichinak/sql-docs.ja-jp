---
description: sp_cdc_get_ddl_history (Transact-sql)
title: sp_cdc_get_ddl_history (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_get_ddl_history
- sp_cdc_get_ddl_history_TSQL
- sys.sp_cdc_get_ddl_history_TSQL
- sys.sp_cdc_get_ddl_history
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], querying metadata
- sp_cdc_get_ddl_history
- sys.sp_cdc_get_ddl_history
ms.assetid: 4dee5e2e-d7e5-4fea-8037-a4c05c969b3a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b00c56c4324c4e25e9a19dd71d342dfcaafcc76d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547296"
---
# <a name="syssp_cdc_get_ddl_history-transact-sql"></a>sp_cdc_get_ddl_history (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定されたキャプチャインスタンスに関連付けられているデータ定義言語 (DDL) の変更履歴を返します。これは、そのキャプチャインスタンスに対して変更データキャプチャが有効になってからです。 変更データ キャプチャは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディッションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.sp_cdc_get_ddl_history [ @capture_instance = ] 'capture_instance'  
```  
  
## <a name="arguments"></a>引数  
 [ @capture_instance =] '*capture_instance*'  
 ソーステーブルに関連付けられたキャプチャインスタンスの名前を指定します。 *capture_instance* は **sysname** であり、NULL にすることはできません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|source_schema|**sysname**|ソース テーブルのスキーマ名です。|  
|source_table|**sysname**|ソーステーブルの名前。|  
|capture_instance|**sysname**|キャプチャ インスタンスの名前です。|  
|required_column_update|**bit**|DDL の変更で、ソース列に対して行われたデータ型の変更を反映するために、変更テーブルの列を更新する必要があったことを示します。|  
|ddl_command|**nvarchar(max)**|ソース テーブルに適用された DDL ステートメントです。|  
|ddl_lsn|**binary(10)**|DDL の変更に関連付けられているログシーケンス番号 (LSN)。|  
|ddl_time|**datetime**|DDL の変更に関連付けられた時刻です。|  
  
## <a name="remarks"></a>解説  
 ソーステーブルの列の追加や削除、既存の列のデータ型の変更など、ソーステーブルに対する DDL の変更は、 [ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md) テーブルに保持されます。 このストアド プロシージャでは、こうした変更をレポートできます。 cdc.ddl_history のエントリは、キャプチャ プロセスで、ログから DDL トランザクションが読み取られた時点で作成されます。  
  
## <a name="permissions"></a>アクセス許可  
 データベースのすべてのキャプチャ インスタンスの行を取得するには、db_owner 固定データベース ロールのメンバーシップが必要です。 他のすべてのユーザーに対して、ソーステーブルのすべてのキャプチャ対象列に対する SELECT 権限が必要です。また、キャプチャインスタンスのゲートロールが定義されている場合は、そのデータベースロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、ソーステーブルに列を追加し、 `HumanResources.Employee` そのストアドプロシージャを実行して、 `sys.sp_cdc_get_ddl_history` キャプチャインスタンスに関連付けられているソーステーブルに適用される DDL の変更を報告し `HumanResources_Employee` ます。  
  
```  
USE AdventureWorks2012;  
GO  
ALTER TABLE HumanResources.Employee  
ADD Test_Column int NULL;  
GO  
-- Pause 10 seconds to allow the event to be logged.   
WAITFOR DELAY '00:00:10';  
GO   
EXECUTE sys.sp_cdc_get_ddl_history   
    @capture_instance = 'HumanResources_Employee';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_cdc_help_change_data_capture &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  
