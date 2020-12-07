---
description: ALTER WORKLOAD GROUP (Transact-SQL)
title: ALTER WORKLOAD GROUP (Transact-SQL)
ms.custom: ''
ms.date: 05/05/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_WORKLOAD_GROUP_TSQL
- ALTER WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER WORKLOAD GROUP statement
ms.assetid: 957addce-feb0-4e54-893e-5faca3cd184c
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current'
ms.openlocfilehash: acbd75ed614f6f7a2c018fb537b01528fe166e80
ms.sourcegitcommit: d35d0901296580bfceda6e0ab2e14cf2b7e99a0f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2020
ms.locfileid: "92496967"
---
# <a name="alter-workload-group-transact-sql"></a>ALTER WORKLOAD GROUP (Transact-SQL)

[!INCLUDE[select-product](../../includes/select-product.md)]

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

:::row:::
    :::column:::
        **_\* SQL Server \*_** &nbsp;
    :::column-end:::
    :::column:::
        [SQL Managed Instance](alter-workload-group-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](alter-workload-group-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="sql-server-and-sql-managed-instance"></a>SQL Server と SQL Managed Instance

[!INCLUDE [ALTER WORKLOAD GROUP](../../includes/alter-workload-group.md)]
  
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](alter-workload-group-transact-sql.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        **_\* SQL Managed Instance \*_** &nbsp;
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](alter-workload-group-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="sql-server-and-sql-managed-instance"></a>SQL Server と SQL Managed Instance

[!INCLUDE [ALTER WORKLOAD GROUP](../../includes/alter-workload-group.md)]

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](alter-workload-group-transact-sql.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        [SQL Managed Instance](alter-workload-group-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        **_\* Azure Synapse<br />Analytics \*_** &nbsp;
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="azure-synapse-analytics"></a>Azure Synapse Analytics

既存のワークロード グループを変更します。

実行中の要求とキューに置かれた要求を含むシステムで `ALTER WORKLOAD GROUP` がどのように動作するかの詳細については、以下の「`ALTER WORKLOAD GROUP` の動作」のセクションを参照してください。 

[CREATE WORKLOAD GROUP](create-workload-group-transact-sql.md) に適用される制限は `ALTER WORKLOAD GROUP` にも適用されます。  パラメーターを変更する前に、クエリ [sys.workload_management_workload_groups](../../relational-databases/system-catalog-views/sys-workload-management-workload-groups-transact-sql.md) を使用して、値が許容範囲内にあることを確認してください。

## <a name="syntax"></a>構文

```syntaxsql
ALTER WORKLOAD GROUP group_name
 WITH
 ([       MIN_PERCENTAGE_RESOURCE = value ]
  [ [ , ] CAP_PERCENTAGE_RESOURCE = value ]
  [ [ , ] REQUEST_MIN_RESOURCE_GRANT_PERCENT = value ]
  [ [ , ] REQUEST_MAX_RESOURCE_GRANT_PERCENT = value ] 
  [ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }]
  [ [ , ] QUERY_EXECUTION_TIMEOUT_SEC = value ] )
  [ ; ]
  ```

## <a name="arguments"></a>引数

group_name  
変更されている、既存のユーザー定義のワークロード グループの名前です。  group_name は変更できません。 

MIN_PERCENTAGE_RESOURCE = value  
Value は 0 から 100 の範囲の整数です。  min_percentage_resource を変更するときは、min_percentage_resource の合計がすべてのワークロード グループ全体で 100 を超えてはいけません。  min_percentage_resource を変更するには、コマンドが完了する前に、実行中のすべてのクエリがワークロードグループ内で完了する必要があります。  詳細については、このドキュメントの「ALTER WORKLOAD GROUP の動作」のセクションを参照してください。

CAP_PERCENTAGE_RESOURCE = value  
Value は 1 から 100 の範囲の整数です。  cap_percentage_resource の値は、min_percentage_resource よりも大きくする必要があります。  cap_percentage_resource を変更するには、コマンドが完了する前に、実行中のすべてのクエリがワークロードグループ内で完了する必要があります。  詳細については、このドキュメントの「ALTER WORKLOAD GROUP の動作」のセクションを参照してください。 

REQUEST_MIN_RESOURCE_GRANT_PERCENT = value  
Value は、0.75 から 100.00 の範囲の 10 進数です。  request_min_resource_grant_percent の値は、min_percentage_resource の係数である必要があり、cap_percentage_resource よりも小さくする必要があります。 
  
REQUEST_MAX_RESOURCE_GRANT_PERCENT = value  
Value は 10 進数で request_min_resource_grant_percent 以上である必要があります。

IMPORTANCE = { LOW \|  BELOW_NORMAL \| NORMAL \| ABOVE_NORMAL \| HIGH }  
ワークロード グループに対する要求の既定の重要度を変更します。

QUERY_EXECUTION_TIMEOUT_SEC = value  
クエリが取り消されるまでに実行できる最大時間を秒単位で変更します。 Value は、0 または正の整数にする必要があります。 value の既定の設定が 0 の場合は、無制限を示します。   

## <a name="permissions"></a>アクセス許可

CONTROL DATABASE アクセス許可が必須です

## <a name="example"></a>例

次の例では、カタログ ビューの wgDataLoads の値を確認し、値を変更しています。

```sql
SELECT *
FROM sys.workload_management_workload_groups  
WHERE [name] = 'wgDataLoads'

ALTER WORKLOAD GROUP wgDataLoads WITH
( MIN_PERCENTAGE_RESOURCE            = 40
 ,CAP_PERCENTAGE_RESOURCE            = 80
 ,REQUEST_MIN_RESOURCE_GRANT_PERCENT = 10 )
 ```

## <a name="alter-workload-group-behavior"></a>ALTER WORKLOAD GROUP の動作

どの時点でも、システムには 3 種類の要求があります
- まだ分類されていない要求。
- オブジェクトのロックまたはシステム リソースのために分類され、待機している要求。
- 分類され、実行中の要求。

変更するワークロード グループのプロパティによって、設定が有効になるタイミングは異なります。

**重要度または query_execution_timeout** 重要度と query_execution_timeout のプロパティの場合、分類されていない要求は、新しい構成値を取得します。  待機中および実行中の要求は、古い構成で実行されます。  `ALTER WORKLOAD GROUP` の要求は、ワークロード グループでクエリが実行されているかどうかに関係なく、直ちに実行されます。

**Request_min_resource_grant_percent または request_max_resource_grant_percent** request_min_resource_grant_percent または request_max_resource_grant_percent の場合、実行中の要求は古い構成で実行されます。  待機中の要求と分類されていない要求は、新しい構成値を取得します。  `ALTER WORKLOAD GROUP` の要求は、ワークロード グループでクエリが実行されているかどうかに関係なく、直ちに実行されます。

**Min_percentage_resource または cap_percentage_resource** min_percentage_resource および cap_percentage_resource の場合、実行中の要求は古い構成で実行されます。  待機中の要求と分類されていない要求は、新しい構成値を取得します。 

min_percentage_resource と cap_percentage_resource を変更するには、変更されているワークロード グループ内で実行中の要求をドレインする必要があります。  min_percentage_resource を減らすと、解放されたリソースが共有プールに返され、他のワークロード グループからの要求で使用できるようになります。  逆に、min_percentage_resource を増やすと、共有プールから必要なリソースのみを使用する要求が完了するまで待機します。  ワークロード グループの変更操作では、共有プールで実行されるのを待機している他の要求よりも、共有リソースへのアクセスが優先されます。  min_percentage_resource の合計が 100% を超えると、ALTER WORKLOAD GROUP の要求はすぐに失敗します。 

**ロック動作** ワークロード グループを変更するには、すべてのワークロード グループに対するグローバルなロックが必要です。  ワークロード グループを変更する要求は、既に送信済みのワークロード グループの作成/ドロップ要求の後ろのキューに格納されます。  変更ステートメントのバッチを一度に送信すると、そのバッチは、送信された順序で処理されます。  

## <a name="see-also"></a>関連項目

- [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](create-workload-group-transact-sql.md)
- [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](drop-workload-group-transact-sql.md)
- [sys.workload_management_workload_groups](../../relational-databases/system-catalog-views/sys-workload-management-workload-groups-transact-sql.md)
- [sys.dm_workload_management_workload_groups_stats](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md)
- [クイック スタート: T-SQL を使用してワークロードの分離を構成する](/azure/sql-data-warehouse/quickstart-configure-workload-isolation-tsql)

::: moniker-end
