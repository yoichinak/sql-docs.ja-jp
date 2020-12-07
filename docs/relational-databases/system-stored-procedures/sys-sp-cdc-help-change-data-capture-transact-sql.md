---
description: sys.sp_cdc_help_change_data_capture (Transact-sql)
title: sys.sp_cdc_help_change_data_capture (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_help_change_data_capture_TSQL
- sys.sp_cdc_help_change_data_capture_TSQL
- sp_cdc_help_change_data_capture
- sys.sp_cdc_help_change_data_capture
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], querying metadata
- sys.sp_cdc_help_change_data_capture
- sp_cdc_help_change_data_capture
ms.assetid: 91fd41f5-1b4d-44fe-a3b5-b73eff65a534
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 13f78f25cd02ccf9c698518b5aa10f7fda0b7694
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809824"
---
# <a name="syssp_cdc_help_change_data_capture-transact-sql"></a>sys.sp_cdc_help_change_data_capture (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベースで変更データキャプチャが有効になっている各テーブルについて、変更データキャプチャの構成を返します。 各ソーステーブルに対して最大で2つの行を返すことができます。キャプチャインスタンスごとに1つの行です。 変更データ キャプチャは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディッションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](../../sql-server/editions-and-components-of-sql-server-2016.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.sp_cdc_help_change_data_capture   
  [ [ @source_schema = ] 'source_schema' ]  
  [, [ @source_name = ] 'source_name' ]  
```  
  
## <a name="arguments"></a>引数  
 [ @source_schema =] '*source_schema*'  
 ソーステーブルが属しているスキーマの名前を指定します。 *source_schema* は **sysname**,、既定値は NULL です。 *Source_schema*が指定されている場合は、 *source_name*も指定する必要があります。  
  
 NULL 以外の場合は、 *source_schema* が現在のデータベースに存在している必要があります。  
  
 *Source_schema*が null 以外の場合、 *source_name*も null 以外である必要があります。  
  
 [ @source_name =] '*source_name*'  
 ソーステーブルの名前を指定します。 *source_name* は **sysname**,、既定値は NULL です。 *Source_name*が指定されている場合は、 *source_schema*も指定する必要があります。  
  
 NULL 以外の場合は、 *source_name* が現在のデータベースに存在している必要があります。  
  
 *Source_name*が null 以外の場合、 *source_schema*も null 以外である必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|source_schema|**sysname**|ソース テーブルのスキーマ名です。|  
|source_table|**sysname**|ソーステーブルの名前。|  
|capture_instance|**sysname**|キャプチャ インスタンスの名前です。|  
|object_id|**int**|ソーステーブルに関連付けられている変更テーブルの ID。|  
|source_object_id|**int**|ソーステーブルの ID。|  
|start_lsn|**binary(10)**|変更テーブルをクエリする際の下端を表すログ シーケンス番号 (LSN) です。<br /><br /> NULL = 低いエンドポイントが確立されていません。|  
|end_lsn|**binary(10)**|変更テーブルに対してクエリを実行するための高エンドポイントを表す LSN。 で [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] は、この列は常に NULL です。|  
|supports_net_changes|**bit**|Net change サポートが有効になっています。|  
|has_drop_pending|**bit**|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] では使用されません。|  
|role_name|**sysname**|変更データへのアクセスを制御するデータベース ロールの名前です。<br /><br /> NULL = ロールは使用されません。|  
|index_name|**sysname**|ソーステーブル内の行を一意に識別するために使用されるインデックスの名前。|  
|filegroup_name|**sysname**|変更テーブルが存在するファイルグループの名前。<br /><br /> NULL = 変更テーブルは、データベースの既定のファイルグループにあります。|  
|create_date|**datetime**|キャプチャインスタンスが有効になった日付。|  
|index_column_list|**nvarchar(max)**|ソーステーブル内の行を一意に識別するために使用されるインデックス列の一覧です。|  
|captured_column_list|**nvarchar(max)**|キャプチャ対象のソース列のリスト。|  
  
## <a name="remarks"></a>注釈  
 *Source_schema*と*source_name*が既定で null に設定されているか、明示的に null が設定されている場合、このストアドプロシージャは、呼び出し元が選択したアクセス権を持つすべてのデータベースキャプチャインスタンスに関する情報を返します。 *Source_schema*および*source_name*が NULL 以外の場合は、特定の名前が有効になっているテーブルに関する情報のみが返されます。  
  
## <a name="permissions"></a>アクセス許可  
 *Source_schema*と*source_name*が NULL の場合、結果セットに含める有効なテーブルは、呼び出し元の承認によって決まります。 呼び出し元は、キャプチャインスタンスのすべてのキャプチャ対象列に対する SELECT 権限を持っている必要があります。また、テーブル情報が含まれるように定義されているすべてのゲートロールのメンバーシップも必要です。 Db_owner データベースロールのメンバーは、定義されているすべてのキャプチャインスタンスに関する情報を表示できます。 特定の有効なテーブルの情報が要求された場合、同じ選択およびメンバーシップの条件が名前付きテーブルに適用されます。  
  
## <a name="examples"></a>例  
  
### <a name="a-returning-change-data-capture-configuration-information-for-a-specified-table"></a>A. 指定したテーブルについて変更データ キャプチャの構成情報を取得する  
 次の例は、`HumanResources.Employee` テーブルを対象に変更データ キャプチャの構成を取得します。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_help_change_data_capture   
    @source_schema = N'HumanResources',   
    @source_name = N'Employee';  
GO  
```  
  
### <a name="b-returning-change-data-capture-configuration-information-for-all-tables"></a>B. すべてのテーブルについて変更データ キャプチャの構成情報を取得する  
 次の例では、呼び出し元がアクセスを許可されている変更データを含む、データベース内のすべての有効なテーブルの構成情報を返します。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_help_change_data_capture;  
GO  
```  
  
