---
title: sys.dm_exec_query_optimizer_memory_gateways (Transact-sql)
description: 同時クエリの最適化を調整するために使用されるリソースセマフォの現在の状態を返します。
ms.custom: seo-dt-2019
ms.date: 04/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: wiassaf
ms.technology: performance
ms.topic: language-reference
f1_keywords:
- dm_exec_query_optimizer_memory_gateways_TSQL
- dm_exec_query_optimizer_memory_gateways
- sys.dm_exec_query_optimizer_memory_gateways_TSQL
- sys.dm_exec_query_optimizer_memory_gateways
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_optimizer_memory_gateways dynamic management view
author: josack
ms.author: josack
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1db599449d45263445ae9628e2cfbacfe768f0f1
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "96503509"
---
# <a name="sysdm_exec_query_optimizer_memory_gateways-transact-sql"></a>sys.dm_exec_query_optimizer_memory_gateways (Transact-sql)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

同時クエリの最適化を調整するために使用されるリソースセマフォの現在の状態を返します。

|Column|種類|[説明]|  
|----------|---------------|-----------------|  
|**pool_id**|**int**|Resource Governor の下のリソースプール ID|  
|**name**|**sysname**|コンパイルゲート名 (小規模ゲートウェイ、中規模ゲートウェイ、ビッグゲートウェイ)|
|**max_count**|**int**|同時コンパイルの最大構成数|
|**active_count**|**int**|このゲートで現在アクティブなコンパイルの数|
|**waiter_count**|**int**|このゲート内の待機処理の数|
|**threshold_factor**|**bigint**|クエリの最適化で使用される最大メモリ部分を定義するしきい値係数。  小さいゲートウェイの場合、threshold_factor は、小さいゲートウェイでのアクセスを取得するために1つのクエリに対して最大オプティマイザーメモリ使用量 (バイト単位) を示します。  M とビッグゲートウェイの場合、threshold_factor は、このゲートで使用可能な合計サーバーメモリの部分を示します。 ゲートのメモリ使用量のしきい値を計算するときに除数として使用されます。|
|**threshold**|**bigint**|次のしきい値メモリ (バイト単位)。  このクエリは、メモリ消費量がこのしきい値に達した場合に、このゲートウェイへのアクセスを取得するために必要です。  クエリがこのゲートウェイへのアクセスを取得する必要がない場合は、"-1" になります。|
|**is_active**|**bit**|クエリが現在のゲートを渡す必要があるかどうかを示します。|


## <a name="permissions"></a>アクセス許可  
SQL Server には、サーバーに対する VIEW SERVER STATE 権限が必要です。

Azure SQL Database には、データベースに対する VIEW DATABASE STATE 権限が必要です。


## <a name="remarks"></a>注釈  
SQL Server では、階層化されたゲートウェイアプローチを使用して、許可される同時コンパイルの数を調整します。  小規模、中、大など、3つのゲートウェイが使用されます。 ゲートウェイを使用すると、より大きなコンパイルメモリを必要とするコンシューマーによって、全体的なメモリリソースが枯渇するのを防ぐことができます。

ゲートウェイの結果を遅延コンパイルで待機します。 調整された要求には、コンパイル時の遅延に加えて、RESOURCE_SEMAPHORE_QUERY_COMPILE の待機の種類の累積が関連付けられます。 RESOURCE_SEMAPHORE_QUERY_COMPILE の待機の種類は、クエリがコンパイルに大量のメモリを使用していて、メモリが不足していること、または、特定のゲートウェイで使用可能なユニットがいっぱいになっていることを示している場合があります。 **Sys.dm_exec_query_optimizer_memory_gateways** の出力を使用して、クエリ実行プランをコンパイルするためのメモリが不足しているシナリオのトラブルシューティングを行うことができます。  

## <a name="examples"></a>例  

### <a name="a-viewing-statistics-on-resource-semaphores"></a>A. リソースセマフォの統計の表示  
この SQL Server インスタンスの現在のオプティマイザーメモリゲートウェイの統計はどのようなものですか?

```  
SELECT [pool_id], [name], [max_count], [active_count],
       [waiter_count], [threshold_factor], [threshold],
       [is_active]
FROM sys.dm_exec_query_optimizer_memory_gateways;   

```  

## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](./system-dynamic-management-views.md)   
 [実行関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](./execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[DBCC MEMORYSTATUS コマンドを使用して SQL Server 2005 のメモリ使用率を監視する方法](https://support.microsoft.com/help/907877/how-to-use-the-dbcc-memorystatus-command-to-monitor-memory-usage-on-sql-server-2005) 
[SQL Server 2014 の RESOURCE_SEMAPHORE_QUERY_COMPILE での大規模なクエリのコンパイルの待機](https://support.microsoft.com/help/3024815/large-query-compilation-waits-on-resource-semaphore-query-compile-in-sql-server-2014)
