---
description: CREATE EXTERNAL RESOURCE POOL (Transact-SQL)
title: CREATE EXTERNAL RESOURCE POOL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning-services
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL RESOURCE POOL
- CREATE EXTERNAL_RESOURCE_POOL_TSQL
- EXTERNAL RESOURCE POOL
- EXTERNAL_RESOURCE_POOL_TSQL
- EXTERNAL RESOURCE
- EXTERNAL_RESOURCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE EXTERNAL RESOURCE POOL statement
ms.assetid: 8cc798ad-c395-461c-b7ff-8c561c098808
author: dphansen
ms.author: davidph
manager: cgronlund
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8a0f2d13c26e6b19b30e551560d11be58ff71e48
ms.sourcegitcommit: c74bb5944994e34b102615b592fdaabe54713047
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90990055"
---
# <a name="create-external-resource-pool-transact-sql"></a>CREATE EXTERNAL RESOURCE POOL (Transact-SQL)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

外部プロセス用のリソースを定義するための外部プールを作成します。 リソース プールは、データベース エンジン インスタンスの物理リソース (メモリと CPU) のサブセットを表します。 Resource Governor を使用すると、サーバー リソースを最大 64 個のリソース プールに分散できます。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] の [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] の場合、外部プールは `rterm.exe`、`BxlServer.exe`、およびそれらにより生成された他のプロセスを管理します。
::: moniker-end

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
[!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] の場合、外部プールは `rterm.exe`、`python.exe`、`BxlServer.exe`、およびそれらにより生成された他のプロセスを管理します。
::: moniker-end
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
 

## <a name="syntax"></a>構文  
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"

```syntaxsql
CREATE EXTERNAL RESOURCE POOL pool_name  
[ WITH (  
    [ MAX_CPU_PERCENT = value ]  
    [ [ , ] MAX_MEMORY_PERCENT = value ]  
    [ [ , ] MAX_PROCESSES = value ]   
    )   
]  
[ ; ]  
  
<CPU_range_spec> ::=    
{ CPU_ID | CPU_ID  TO CPU_ID } [ ,...n ]  
```  
::: moniker-end

::: moniker range="=sql-server-2016||=sql-server-2017||=sqlallproducts-allversions"
```syntaxsql
CREATE EXTERNAL RESOURCE POOL pool_name  
[ WITH (  
    [ MAX_CPU_PERCENT = value ]  
    [ [ , ] AFFINITY CPU =    
            {  
                AUTO   
              | ( <cpu_range_spec> )   
              | NUMANODE = ( <NUMA_node_id> )   
            } ]   
    [ [ , ] MAX_MEMORY_PERCENT = value ]  
    [ [ , ] MAX_PROCESSES = value ]   
    )   
]  
[ ; ]  
  
<CPU_range_spec> ::=    
{ CPU_ID | CPU_ID  TO CPU_ID } [ ,...n ]  
```  
::: moniker-end

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数

*pool_name*  
外部リソース プールのユーザー定義名を指定します。 *pool_name* には、最大 128 文字の英数字を指定できます。 この引数は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内で一意であり、[識別子](../../relational-databases/databases/database-identifiers.md)のルールに従っている必要があります。  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
MAX_CPU_PERCENT =*value*  
CPU の競合がある場合に、外部リソース プールで受け取ることのできる全要求に対する最大平均 CPU 帯域幅。 *value* は整数です。 *value* の許容範囲は 1 ～ 100 です。


MAX_MEMORY_PERCENT =*value*  
この外部リソース プールの要求で使用できる合計サーバー メモリを指定します。 *value* は整数です。 *value* の許容範囲は 1 ～ 100 です。

MAX_PROCESSES =*value*  
外部リソース プールに許されるプロセスの最大数。 0 を指定すると、プールのしきい値は無制限になり、その後はコンピューターのリソースによってのみ拘束されます。
::: moniker-end

::: moniker range="=sql-server-2016||=sql-server-2017||=sqlallproducts-allversions"
MAX_CPU_PERCENT =*value*  
CPU の競合がある場合に、外部リソース プールで受け取ることのできる全要求に対する最大平均 CPU 帯域幅。 *value* は整数です。 *value* の許容範囲は 1 ～ 100 です。

AFFINITY {CPU = AUTO | ( <CPU_range_spec>) | NUMANODE = (\<NUMA_node_range_spec>)} では、外部リソース プールが特定の CPU にアタッチされます。

AFFINITY CPU = **(** <CPU_range_spec> **)** では、指定された CPU_ID によって識別される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPU に外部リソース プールがマップされます。

AFFINITY NUMANODE = **(\<NUMA_node_range_spec> **)** を使用すると、外部リソース プールは、指定した NUMA ノードまたはノードの範囲に対応する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物理 CPU にアフィニティ化されれます。 

MAX_MEMORY_PERCENT =*value*  
この外部リソース プールの要求で使用できる合計サーバー メモリを指定します。 *value* は整数です。 *value* の許容範囲は 1 ～ 100 です。

MAX_PROCESSES =*value*  
外部リソース プールに許されるプロセスの最大数。 0 を指定すると、プールのしきい値は無制限になり、その後はコンピューターのリソースによってのみ拘束されます。
::: moniker-end

## <a name="remarks"></a>解説

[ALTER RESOURCE GOVERNOR RECONFIGURE](../../t-sql/statements/alter-resource-governor-transact-sql.md) ステートメントを実行すると、[!INCLUDE[ssDE](../../includes/ssde-md.md)]はリソース プールを実装します。

リソース プールの一般的な情報については、「[リソース ガバナー リソース プール](../../relational-databases/resource-governor/resource-governor-resource-pool.md)」、「[sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)」、および「[sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)」をご覧ください。

機械学習で使用される外部リソース プールの管理に固有の情報については、「[Resource governance for machine learning in SQL Server (SQL Server での機械学習のリソース管理)](../../machine-learning/administration/resource-governor.md)」をご覧ください。 

## <a name="permissions"></a>アクセス許可

`CONTROL SERVER` 権限が必要です。

## <a name="examples"></a>例

外部プールでは CPU 使用率が 75% に制限されています。 最大メモリは、コンピューターで使用可能なメモリの 30% です。

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
```sql
CREATE EXTERNAL RESOURCE POOL ep_1
WITH (  
    MAX_CPU_PERCENT = 75
    , MAX_MEMORY_PERCENT = 30
);
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```
::: moniker-end

::: moniker range="=sql-server-2016||=sql-server-2017||=sqlallproducts-allversions"
```sql
CREATE EXTERNAL RESOURCE POOL ep_1
WITH (  
    MAX_CPU_PERCENT = 75
    , AFFINITY CPU = AUTO
    , MAX_MEMORY_PERCENT = 30
);
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```
::: moniker-end

## <a name="see-also"></a>関連項目

+ [external scripts enabled サーバー構成オプション](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)
+ [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
+ [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
+ [DROP EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)
+ [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)
+ [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)
+ [リソース ガバナー リソース プール](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
+ [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)
+ [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)
+ [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)
