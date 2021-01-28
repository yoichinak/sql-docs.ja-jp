---
title: メモリ使用率の監視
description: 'SQL Server インスタンスを監視し、メモリ使用率が通常の範囲内であることを確認します。 メモリの使用: 使用可能なバイト数とメモリ: Pages/sec カウンター。'
ms.custom: ''
ms.date: 01/20/2021
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- tuning databases [SQL Server], memory
- monitoring server performance [SQL Server], memory usage
- isolating memory [SQL Server]
- paging rate [SQL Server]
- memory [SQL Server], monitoring usage
- monitoring [SQL Server], memory usage
- low-memory conditions
- database monitoring [SQL Server], memory usage
- available memory [SQL Server]
- page faults [SQL Server]
- monitoring performance [SQL Server], memory usage
- server performance [SQL Server], memory
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 8954573b0c32eef45ec655b27d26e03e72be96ed
ms.sourcegitcommit: 713e5a709e45711e18dae1e5ffc190c7918d52e7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2021
ms.locfileid: "98688767"
---
# <a name="monitor-memory-usage"></a>メモリ使用量の監視
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを定期的に監視し、メモリ使用率が通常の範囲内であることを確認します。 

## <a name="configuring-ssnoversion-max-memory"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の最大メモリの構成

既定では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスは、時間が経過するに従って、サーバー内の使用可能な Windows オペレーティング システムのメモリの多くを消費します。 メモリは、いったん取得されると、メモリ不足が検出されない限り、解放されることはありません。 これは仕様であり、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセス内のメモリ リークを示すものではありません。 ほとんどの用途で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって取得できるメモリの量を制限するには、[**Max Server Memory** オプション](../../database-engine/configure-windows/server-memory-server-configuration-options.md)を使用します。 詳細については、「[メモリ管理アーキテクチャ ガイド](../../relational-databases/memory-management-architecture-guide.md#changes-to-memory-management-starting-with-)」を参照してください。

SQL Server on Linux では、mssql-conf ツールおよび [memory.memorylimitmb 設定](../../linux/sql-server-linux-configure-mssql-conf.md#memorylimit)を使用して、[メモリ制限を設定](../../linux/sql-server-linux-performance-best-practices.md#advanced-configuration)します。  

## <a name="monitor-operating-system-memory"></a>オペレーティング システムのメモリを監視する   
 メモリ不足の状況を監視するには、次の Windows サーバー カウンターを使用します。 多くのオペレーティング システムのメモリ カウンターに対しては、動的管理ビュー [sys.dm_os_process_memory](../system-dynamic-management-views/sys-dm-os-process-memory-transact-sql.md) および [sys.dm_os_sys_memory](../system-dynamic-management-views/sys-dm-os-sys-memory-transact-sql.md) を使用してクエリを実行できます。

-   **Memory:Available Bytes**  
このカウンターは、プロセスで現在使用できるメモリのバイト数を示します。 **Available Bytes** カウンターの値が小さい場合、オペレーティング システムのメモリが全体的に不足していることを示します。 この値のクエリを実行するには、T-SQL 経由で [sys.dm_os_sys_memory](../system-dynamic-management-views/sys-dm-os-sys-memory-transact-sql.md).available_physical_memory_kb を使用します。

-   **Memory:Pages/sec**  
このカウンターは、ハード ページ フォールトが原因でディスクから取得されたページ数、またはページ フォールトが原因でワーキング セット内の領域を解放するためにディスクに書き込まれたページ数を示します。 **Pages/sec** カウンターの値が高い場合、ページングが過剰であることが考えられます。  

-   **Memory:Page Faults/sec** このカウンターは、システム プロセスを含むすべてのプロセスのページ フォールト率を示します。 コンピューターに使用可能なメモリが十分にある場合でも、ディスクへのページングは (したがって、ページ フォールトも)、低い割合で発生するのが一般的です。ただし、ゼロになることはありません。 Microsoft Windows Virtual Memory Manager (VMM) では、プロセスの作業セットのサイズを小さくするときに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と他のプロセスからページを取得します。 この VMM の動作が、ページ フォールトの原因になる場合があります。  

-   **Process:Page Faults/sec** このカウンターは、特定のユーザー プロセスのページ フォールト率を示します。 **Process: Page Faults/sec** を監視して、ディスク アクティビティが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によるページングが原因で発生しているかどうかを判断します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または他のプロセスが過剰なページングの原因であるかどうかを判断するには、**Process:Page Faults/sec** カウンター ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセス インスタンス) を監視します。  
  
 過剰なページングの解決方法の詳細については、オペレーティング システムのマニュアルを参照してください。  
  
## <a name="isolating-memory-used-by-ssnoversion"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によって使用されるメモリの分離 

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のメモリ使用量を監視するには、次の [SQL Server オブジェクト カウンター](use-sql-server-objects.md)を使用します。 多くの SQL Server オブジェクト カウンターには、動的管理ビュー [sys.dm_os_performance_counters](../system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) または [sys.dm_os_process_memory](../system-dynamic-management-views/sys-dm-os-process-memory-transact-sql.md) を使用してクエリを実行することができます。

 既定では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により、使用できるシステム リソースに基づいて、そのメモリ要件が動的に管理されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により多くのメモリが必要な場合は、空き物理メモリが使用可能かどうかを調べるためにオペレーティング システムに問い合わせ、使用可能なメモリを使用します。 OS の空きメモリが不足している場合は、メモリ不足の状態が緩和されるまで、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が **min server memory** の制限に達するまで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってメモリが解放され、オペレーティング システムに戻されます。 ただし、**Min Server Memory** および **Max Server Memory** サーバー構成オプションを使用すると、このオプションをオーバーライドしてメモリを動的に使用できます。 詳細については、「 [サーバー メモリ オプション](../../database-engine/configure-windows/server-memory-server-configuration-options.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用されるメモリの量を監視するには、次のパフォーマンス カウンターを調べます。  
  
-   **SQL Server:Memory Manager:Total Server Memory (KB)**  
このカウンターは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メモリ マネージャーによって、現在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にコミットされているオペレーティング システムのメモリ量を示します。 この数値は、実際のアクティビティの必要に応じて増加すると予想され、SQL Server の起動後に増加します。 このカウンターのクエリを実行するには、[sys.dm_os_sys_info](../system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) 動的管理ビューを使用し、**committed_kb** 列を観察します。

-   **SQL Server:Memory Manager:Target Server Memory (KB)**  
このカウンターは、最近のワークロードに基づいて、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で消費できる最適なメモリ量を示します。 一般的な操作期間後の **Total Server Memory** と比較して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に必要な量のメモリが割り当てられているかどうかを判断します。 一般的な操作後、**Total Server Memory** と **Target Server Memory** は近い値になります。 **Total Server Memory** が **Target Server Memory** より大幅に少ない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスでメモリ不足が発生しているおそれがあります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動後の期間に、**Total Server Memory** が増えるに従って、**Total Server Memory** は **Target Server Memory** よりも少なくなると予想されます。 このカウンターのクエリを実行するには、[sys.dm_os_sys_info](../system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) 動的管理ビューを使用し、**committed_target_kb** 列を観察します。 メモリを構成するためのベスト プラクティスの詳細については、「[サーバー メモリの構成オプション](../../database-engine/configure-windows/server-memory-server-configuration-options.md#manually)」を参照してください。

-   **Process:Working Set**  
このカウンターは、オペレーティング システムに応じて、現在プロセスで使用中の物理メモリの量を示します。 このカウンターの sqlservr.exe インスタンスを確認します。 このカウンターのクエリを実行するには、[sys.dm_os_process_memory](../system-dynamic-management-views/sys-dm-os-process-memory-transact-sql.md) 動的管理ビューを使用し、**physical_memory_in_use_kb** 列を観察します。

-   **Process:Private Bytes**  
このカウンターは、プロセスにより、独自に使用するためにオペレーティング システムに対して要求されたメモリの量を示します。 このカウンターの sqlservr.exe インスタンスを確認します。 このカウンターには、[**Max Server Memory** オプション](../../database-engine/configure-windows/server-memory-server-configuration-options.md)によって制限されないものを含め、sqlservr.exe によって要求されたすべてのメモリ割り当てが含まれるため、このカウンターによって、[**Max Server Memory** オプション](../../database-engine/configure-windows/server-memory-server-configuration-options.md)より大きい値が報告される場合があります。

-   **SQL Server:Buffer Manager:Database Pages**  
このカウンターは、データベースの内容が含まれたバッファー プール内のページの数を示します。 SQL Server プロセス内のバッファー プール以外の他のメモリは含まれません。 このカウンターのクエリを実行するには、[sys.dm_os_performance_counters](../system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) 動的管理ビューを使用します。

-   **SQL Server:Buffer Manager:Buffer Cache Hit Ratio**  
このカウンターは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固有です。 望ましい値は、90 以上です。 90 より大きい値は、データに対するすべての要求の 90% 以上が、ディスクから読み取る必要なく、メモリ内のデータ キャッシュによって満たされたことを示します。 SQL Server バッファー マネージャーの詳細については、[SQL Server バッファー マネージャー オブジェクト](sql-server-buffer-manager-object.md)に関する記事を参照してください。 このカウンターのクエリを実行するには、[sys.dm_os_performance_counters](../system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) 動的管理ビューを使用します。  
 
-   **SQL Server:Buffer Manager:Page life expectancy**  
このカウンターは、最も古いページがバッファー プールに保持される時間を秒単位で測定します。 NUMA アーキテクチャを使用するシステムでは、これは、すべての NUMA ノード全体の平均です。 より大きい、増加する値が最適です。 急激な減少は、バッファー プールの中と外でのデータの非常に大きな変動を示し、ワークロードが、既にメモリ内にあるデータを完全に活用できなかったことを指します。 NUMA ノードごとに、独自のバッファー プール ノードがあります。 複数の NUMA ノードを持つサーバーで、各バッファー プール ノードのページの予測保持期間を表示するには、**SQL Server: Buffer Node: Page life expectancy** を使用します。 このカウンターのクエリを実行するには、[sys.dm_os_performance_counters](../system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) 動的管理ビューを使用します。

  
## <a name="examples"></a>例 

### <a name="determining-current-memory-allocation"></a>現在のメモリ割り当ての確認  
 次のクエリにより、現在割り当てられているメモリに関する情報が返されます。  
  
```  
SELECT
(total_physical_memory_kb/1024) AS Total_OS_Memory_MB,
(available_physical_memory_kb/1024)  AS Available_OS_Memory_MB
FROM sys.dm_os_sys_memory;

SELECT  
(physical_memory_in_use_kb/1024) AS Memory_used_by_Sqlserver_MB,  
(locked_page_allocations_kb/1024) AS Locked_pages_used_by_Sqlserver_MB,  
(total_virtual_address_space_kb/1024) AS Total_VAS_in_MB,
process_physical_memory_low,  
process_virtual_memory_low  
FROM sys.dm_os_process_memory;  
```  

### <a name="determining-current-sql-server-memory-utilization"></a>SQL Server による現在のメモリ使用率の確認   
 次のクエリにより、SQL Server による現在のメモリ使用率に関する情報が返されます。  
```  
SELECT
sqlserver_start_time,
(committed_kb/1024) AS Total_Server_Memory_MB,
(committed_target_kb/1024)  AS Target_Server_Memory_MB
FROM sys.dm_os_sys_info;
```   

### <a name="determining-page-life-expectancy"></a>ページの予測保持期間の確認
 次のクエリでは、**sys.dm_os_performance_counters** を使用して、SQL Server インスタンスの現在の **page life expectancy** 値を、バッファー マネージャー全体のレベルと NUMA ノード別のレベルで観察します。
```
SELECT
CASE instance_name WHEN '' THEN 'Overall' ELSE instance_name END AS NUMA_Node, cntr_value AS PLE_s
FROM sys.dm_os_performance_counters    
WHERE counter_name = 'Page life expectancy';
```

## <a name="see-also"></a>関連項目
- [sys.dm_os_sys_memory (Transact-SQL)](../system-dynamic-management-views/sys-dm-os-sys-memory-transact-sql.md)
- [sys.dm_os_process_memory (Transact-SQL)](../system-dynamic-management-views/sys-dm-os-process-memory-transact-sql.md)
- [sys.dm_os_sys_info (Transact-SQL)](../system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)
- [sys.dm_os_performance_counters (Transact-SQL)](../system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)
- [SQL Server の Memory Manager オブジェクト](sql-server-memory-manager-object.md)
- [SQL Server の Buffer Manager オブジェクト](sql-server-buffer-manager-object.md)   
- [サーバー メモリの構成オプション](../../database-engine/configure-windows/server-memory-server-configuration-options.md)
- [メモリ管理アーキテクチャ ガイド](../../relational-databases/memory-management-architecture-guide.md)
