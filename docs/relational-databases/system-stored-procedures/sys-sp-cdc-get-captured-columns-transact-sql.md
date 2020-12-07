---
description: sys.sp_cdc_get_captured_columns (Transact-sql)
title: sys.sp_cdc_get_captured_columns (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_get_captured_columns
- sys.sp_cdc_get_captured_columns
- sys.sp_cdc_get_captured_columns_TSQL
- sp_cdc_get_captured_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_get_captured_columns
- sp_cdc_get_captured_columns
- change data capture [SQL Server], querying metadata
ms.assetid: d9e680be-ab9b-4e0c-b63a-90658f241df8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9f19017dd72dc51f2fd79010b85c251c3c64ed22
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91811056"
---
# <a name="syssp_cdc_get_captured_columns-transact-sql"></a>sys.sp_cdc_get_captured_columns (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定したキャプチャ インスタンスによって追跡されるキャプチャ対象のソース列について、変更データ キャプチャのメタデータ情報を返します。 変更データ キャプチャは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディッションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](../../sql-server/editions-and-components-of-sql-server-2016.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.sp_cdc_get_captured_columns   
    [ @capture_instance = ] 'capture_instance'  
```  
  
## <a name="arguments"></a>引数  
 [ @capture_instance =] '*capture_instance*'  
 ソーステーブルに関連付けられたキャプチャインスタンスの名前を指定します。 *capture_instance* は **sysname** であり、NULL にすることはできません。  
  
 テーブルのキャプチャインスタンスに関するレポートを作成するには、 [sys.sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md) ストアドプロシージャを実行します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|source_schema|**sysname**|ソース テーブルのスキーマ名です。|  
|source_table|**sysname**|ソーステーブルの名前。|  
|capture_instance|**sysname**|キャプチャ インスタンスの名前です。|  
|column_name|**sysname**|キャプチャされたソース列の名前。|  
|column_id|**int**|ソーステーブル内の列の ID。|  
|column_ordinal|**int**|ソース テーブル内での列の位置です。|  
|data_type|**sysname**|列のデータ型。|  
|character_maximum_length|**int**|文字ベースの列の最大文字長。それ以外の場合は NULL。|  
|numeric_precision|**tinyint**|数値ベースの場合は、列の有効桁数です。それ以外の場合は、NULL です。|  
|numeric_precision_radix|**smallint**|数値ベースの場合は、列の有効桁数の基数です。それ以外の場合は、NULL です。|  
|numeric_scale|**int**|数値ベースの場合は、列の小数点以下桁数です。それ以外の場合は、NULL です。|  
|datetime_precision|**smallint**|Datetime ベースの場合は、列の有効桁数です。それ以外の場合は NULL。|  
  
## <a name="remarks"></a>注釈  
 Sys.sp_cdc_get_captured_columns を使用して、キャプチャインスタンスクエリ関数 [cdc.fn_cdc_get_all_changes_<capture_instance>](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) または [cdc.fn_cdc_get_net_changes_ ](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)<capture_instance>に対してクエリを実行することによって返されたキャプチャ対象列の列情報を取得します。 列名、Id、および位置は、キャプチャインスタンスの有効期間中は一定のままです。 追跡対象テーブルの基になるソース列のデータ型が変更された場合にのみ、列のデータ型が変化します。 ソーステーブルに対して追加または削除された列は、既存のキャプチャインスタンスのキャプチャ対象列には影響しません。  
  
 [Sys.sp_cdc_get_ddl_history](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)を使用して、ソーステーブルに適用されるデータ定義言語 (ddl) ステートメントに関する情報を取得します。 DDL の変更によって追跡対象ソース列の構造が変更された場合、そのような DDL の変更がすべて結果セットとして返されます。  
  
## <a name="permissions"></a>アクセス許可  
 db_owner 固定データベース ロールのメンバーシップが必要です。 他のすべてのユーザーに対して、ソーステーブルのすべてのキャプチャ対象列に対する SELECT 権限が必要です。また、キャプチャインスタンスのゲートロールが定義されている場合は、そのデータベースロールのメンバーシップが必要です。 呼び出し元にソースデータを表示するアクセス許可がない場合、関数はエラー 22981 (オブジェクトが存在しないか、アクセスが拒否されました。) を返します。  
  
## <a name="examples"></a>例  
 次の例は、`HumanResources_Employee` キャプチャ インスタンスに存在するキャプチャ対象列の情報を返します。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_get_captured_columns   
    @capture_instance = N'HumanResources_Employee';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sys.sp_cdc_help_change_data_capture &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
