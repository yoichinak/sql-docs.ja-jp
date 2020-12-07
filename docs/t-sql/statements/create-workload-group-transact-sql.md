---
description: CREATE WORKLOAD GROUP (Transact-SQL)
title: CREATE WORKLOAD GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/27/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD GROUP
- WORKLOAD_GROUP_TSQL
- CREATE WORKLOAD GROUP
- CREATE_WORKLOAD_GROUP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE WORKLOAD GROUP statement
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current'
ms.openlocfilehash: 51db0074dda0a311dfbea84f51144d8b48ab90ce
ms.sourcegitcommit: d35d0901296580bfceda6e0ab2e14cf2b7e99a0f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2020
ms.locfileid: "92496888"
---
# <a name="create-workload-group-transact-sql"></a>CREATE WORKLOAD GROUP (Transact-SQL)

[!INCLUDE[select-product](../../includes/select-product.md)]

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

:::row:::
    :::column:::
        **_\* SQL Server \*_** &nbsp;
    :::column-end:::
    :::column:::
        [SQL Managed Instance](create-workload-group-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](create-workload-group-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="sql-server-and-sql-managed-instance"></a>SQL Server と SQL Managed Instance

[!INCLUDE [CREATE WORKLOAD GROUP](../../includes/create-workload-group.md)]
  
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](create-workload-group-transact-sql.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        **_\* SQL Managed Instance \*_** &nbsp;
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](create-workload-group-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="sql-server-and-sql-managed-instance"></a>SQL Server と SQL Managed Instance

[!INCLUDE [CREATE WORKLOAD GROUP](../../includes/create-workload-group.md)]

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](create-workload-group-transact-sql.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        [SQL Managed Instance](create-workload-group-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        **_\* Azure Synapse<br />Analytics \*_** &nbsp;
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="azure-synapse-analytics"></a>Azure Synapse Analytics

ワークロード グループを作成します。 ワークロード グループは、一連の要求用のコンテナーであり、システムでワークロード管理を構成する方法の基礎となります。 ワークロード グループでは、ワークロードの分離のためのリソースの予約、リソースの格納、要求ごとのリソースの定義、実行ルールへの準拠を行う機能が提供されます。 ステートメントが完了すると、設定が有効になります。

:::image type="icon" source="../../database-engine/configure-windows/media/topic-link.gif"::: [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。

```syntaxsql
CREATE WORKLOAD GROUP group_name
 WITH
 (   MIN_PERCENTAGE_RESOURCE = value 
   , CAP_PERCENTAGE_RESOURCE = value 
   , REQUEST_MIN_RESOURCE_GRANT_PERCENT = value
  [ [ , ] REQUEST_MAX_RESOURCE_GRANT_PERCENT = value ]
  [ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH } ]
  [ [ , ] QUERY_EXECUTION_TIMEOUT_SEC = value ] )
  [ ; ]

```

*group_name*</br>
ワークロード グループを識別する名前を指定します。 *group_name* は、sysname です。 これは長さを最大で 128 文字とすることができ、インスタンス内では一意である必要があります。

*MIN_PERCENTAGE_RESOURCE* = value</br>
他のワークロード グループと共有されない、このワークロード グループに対して保証される最小リソース割り当てを指定します。 *value* は 0 から 100 の範囲の整数です。 すべてのワークロード グループでの min_percentage_resource の合計は、100 を超えることはできません。 min_percentage_resource の値を cap_percentage_resource より大きくすることはできません。 サービス レベルごとに有効な最小値があります。 詳細については、「[有効な値](#effective-values)」を参照してください。

*CAP_PERCENTAGE_RESOURCE* = value</br>
ワークロード グループ内のすべての要求に対するリソースの最大使用率を指定します。 value に対して許可される整数の範囲は 1 から 100 です。 cap_percentage_resource の値は、min_percentage_resource よりも大きくする必要があります。 cap_percentage_resource の有効な値は、他のワークロード グループで min_percentage_resource が 0 より大きく構成されている場合に減らすことができます。

*REQUEST_MIN_RESOURCE_GRANT_PERCENT* = value</br>
要求ごとに割り当てられるリソースの最小量を設定します。 *value* は 0.75 から 100.00 の 10 進数の範囲の必須パラメーターです。 request_min_resource_grant_percent の値は、0.25 の倍数である必要があります。また、min_percentage_resource の係数であり、cap_percentage_resource よりも小さくする必要があります。 サービス レベルごとに有効な最小値があります。 詳細については、「[有効な値](#effective-values)」を参照してください。

次に例を示します。

```sql
CREATE WORKLOAD GROUP wgSample 
WITH
  ( MIN_PERCENTAGE_RESOURCE = 26                -- integer value
    , REQUEST_MIN_RESOURCE_GRANT_PERCENT = 3.25 -- factor of 26 (guaranteed a minimum of 8 concurrency)
    , CAP_PERCENTAGE_RESOURCE = 100 )
```

request_min_resource_grant_percent のガイドラインとして、リソース クラスに使用される値を検討してください。  次の表には、Gen2 のリソース割り当てが含まれています。

|リソース クラス|リソースの割合|
|---|---|
|Smallrc|3%|
|Mediumrc|10%|
|Largerc|22%|
|Xlargerc|70%|
|||

*REQUEST_MAX_RESOURCE_GRANT_PERCENT* = value</br>         
要求ごとに割り当てられるリソースの最大量を設定します。 *value* は省略可能な 10 進数のパラメーターで、既定値は request_min_resource_grant_percent と同じ値です。 *value* は request_min_resource_grant_percent 以上である必要があります。 request_max_resource_grant_percent の値が request_min_resource_grant_percent より大きく、システム リソースが使用可能な場合は、追加のリソースが要求に割り当てられます。

*IMPORTANCE* = { LOW \| BELOW_NORMAL \| NORMAL \| ABOVE_NORMAL \| HIGH }</br>        
ワークロード グループに対する要求の既定の重要度を指定します。 重要度は次のいずれかで、NORMAL が既定値です。

- LOW
- BELOW_NORMAL
- NORMAL (既定値)
- ABOVE_NORMAL
- HIGH

ワークロード グループでの重要度セットは、ワークロード グループ内のすべての要求に対する既定の重要度です。 ユーザーは、分類子レベルで重要度を設定することもできます。これにより、ワークロード グループの重要度の設定をオーバーライドできます。 これにより、ワークロード グループ内の要求の重要度を区別して、予約されていないリソースにすばやくアクセスできるようになります。 ワークロード グループ全体で min_percentage_resource の合計が 100 未満の場合は、重要度に基づいて割り当てられた予約されていないリソースがあります。

*QUERY_EXECUTION_TIMEOUT_SEC* = value</br>     
クエリが取り消されるまでに実行できる最大時間を秒単位で指定します。 *value* は、0 または正の整数にする必要があります。 value の既定の設定が 0 の場合は、クエリはタイムアウトしません。クエリが実行状態になると、QUERY_EXECUTION_TIMEOUT_SEC がカウントされます。クエリがキューに入れられたときではありません。

## <a name="remarks"></a>解説

リソース クラスに対応するワークロード グループは、旧バージョンとの互換性のために自動的に作成されます。 これらのシステム定義のワークロード グループは削除できません。 さらに 8 つのユーザー定義のワークロード グループを作成できます。

ワークロード グループが 0 より大きい `min_percentage_resource` を使用して作成されている場合、`CREATE WORKLOAD GROUP` ステートメントは、ワークロード グループを作成するのに十分なリソースが確保されるまでキューに格納されます。

## <a name="effective-values"></a>有効な値

`min_percentage_resource`、`cap_percentage_resource`、`request_min_resource_grant_percent`、`request_max_resource_grant_percent` の各パラメーターは、現在のサービス レベルおよびその他のワークロード グループの構成のコンテキストで調整された有効な値が含まれます。

サービス レベルに応じてクエリごとに必要最低限のリソースがあるため、`request_min_resource_grant_percent` パラメーターには有効な値が含まれます。  たとえば、最も低いサービス レベル (DW100c) では、要求ごとに最小 25% のリソースが必要です。  ワークロード グループが 3% の `request_min_resource_grant_percent` と `request_max_resource_grant_percent` で構成されている場合、インスタンスが開始されると、両方のパラメーターの有効な値が 25% に調整されます。  インスタンスが DW1000c にスケールアップされる場合、両方のパラメーターに対して構成された有効な値は 3% になります。そのサービス レベルでサポートされている最小値が 3% であるためです。  インスタンスが DW1000c よりも高くスケーリングされた場合、両方のパラメーターに対して構成された有効な値は 3% のままになります。  さまざまなサービス レベルの有効な値の詳細については、以下の表を参照してください。

|サービス レベル|REQUEST_MIN_RESOURCE_GRANT_PERCENT の有効な最小値|同時クエリの最大数|
|---|---|---|
|DW100c|25%|4|
|DW200c|12.5%|8|
|DW300c|8%|12|
|DW400c|6.25%|16|
|DW500c|5%|20|
|DW1000c|3%|32|
|DW1500c|3%|32|
|DW2000c|2%|48|
|DW2500c|2%|48|
|DW3000c|1.5%|64|
|DW5000c|1.5%|64|
|DW6000c|0.75%|128|
|DW7500c|0.75%|128|
|DW10000c|0.75%|128|
|DW15000c|0.75%|128|
|DW30000c|0.75%|128|
||||

`min_percentage_resource` パラメーターは有効な `request_min_resource_grant_percent` 以上である必要があります。 `min_percentage_resource` が有効な `min_percentage_resource` 未満に構成されたワークロード グループには、実行時にゼロに調整された値が含まれています。 この場合、`min_percentage_resource` 用に構成されたリソースは、すべてのワークロード グループとの間で共有できます。 たとえば、DW1000c で実行されている `min_percentage_resource` が 10% であるワークロード グループ `wgAdHoc` には、有効な 10% の `min_percentage_resource` が含まれます (DW1000c でサポートされている最小値は 3% です)。 DW100c の `wgAdhoc` には、有効な 0% の min_percentage_resource が含まれます。 `wgAdhoc` 用に構成された 10% は、すべてのワークロード グループとの間で共有されます。

`cap_percentage_resource` パラメーターにも有効な値があります。 ワークロード グループ `wgAdhoc` が 100% の `cap_percentage_resource` で構成されていて、別のワークロード グループ `wgDashboards` が 25% の `min_percentage_resource` で作成されている場合、`wgAdhoc` の有効な `cap_percentage_resource` は 75% になります。

ワークロード グループの実行時の値を理解する最も簡単な方法は、システム ビュー [sys.dm_workload_management_workload_groups_stats](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md) に対してクエリを実行することです。

## <a name="permissions"></a>アクセス許可

`CONTROL DATABASE` 権限が必要です。

## <a name="see-also"></a>関連項目

- [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](drop-workload-group-transact-sql.md)
- [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](alter-workload-group-transact-sql.md)
- [sys.workload_management_workload_groups](../../relational-databases/system-catalog-views/sys-workload-management-workload-groups-transact-sql.md)
- [sys.dm_workload_management_workload_groups_stats](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md)
- [クイック スタート: T-SQL を使用してワークロードの分離を構成する](/azure/sql-data-warehouse/quickstart-configure-workload-isolation-tsql)

::: moniker-end
