---
description: sys.database_event_sessions (Azure SQL Database)
title: database_event_sessions (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 02c2cd71-d35e-4d4c-b844-92b240f768f4
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: a07eab4d6636acaecda5aa2be495c3db70156822
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537420"
---
# <a name="sysdatabase_event_sessions-azure-sql-database"></a>sys.database_event_sessions (Azure SQL Database)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  現在のデータベースに存在するすべてのイベントセッション定義を一覧表示 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] します。  
  
> [!NOTE]
>  という類似のカタログビューは、 `sys.server_event_sessions` にのみ適用さ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] れます。  
  
||  
|-|  
|**に適用さ**れます: [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 、、およびそれ以降のすべてのバージョン。|  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|イベント セッションの一意な ID。 NULL 値は許可されません。|  
|name|**sysname**|イベントセッションを識別するためのユーザー定義の名前。 名前は一意です。 NULL 値は許可されません。|  
|event_retention_mode|**nchar(1)**|イベントの損失を処理する方法を決定します。 既定値は S です。NULL 値は許可されません。 は次のいずれかです。<br /><br /> S. Event_retention_mode_desc = ALLOW_SINGLE_EVENT_LOSS にマップされる<br /><br /> M. Event_retention_mode_desc = ALLOW_MULTIPLE_EVENT_LOSS にマップされる<br /><br /> 北 Event_retention_mode_desc = NO_EVENT_LOSS にマップされる|  
|event_retention_mode_desc|**sysname**|イベントの損失を処理する方法について説明します。 既定値は ALLOW_SINGLE_EVENT_LOSS です。 NULL 値は許可されません。 は次のいずれかです。<br /><br /> ALLOW_SINGLE_EVENT_LOSS。 イベントはセッションから失われることがあります。 1つのイベントは、すべてのイベントバッファーがいっぱいになったときにのみ削除されます。 イベント バッファーがいっぱいのときに単独のイベントを削除することで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のパフォーマンス特性が許容可能な状態になり、処理後のイベント ストリームでの損失を最小限に抑えることができます。<br /><br /> ALLOW_MULTIPLE_EVENT_LOSS。 セッションから完全なイベントバッファーが失われる可能性があります。 失われるイベントの数は、セッションに割り当てられているメモリサイズ、メモリのパーティション分割、およびバッファー内のイベントのサイズによって異なります。 このオプションを使用すると、イベント バッファーがすぐにいっぱいになるときにサーバーのパフォーマンスに与える影響を最小限に抑えることができます。 ただし、多数のイベントがセッションから失われる可能性があります。<br /><br /> NO_EVENT_LOSS。 イベントの削除は許可されません。 このオプションにより、発生したすべてのイベントが保持されます。 このオプションを使用すると、イベントを発生させるすべてのタスクが、イベントバッファー内の領域が使用可能になるまで待機します。 これにより、イベントセッションがアクティブな間、パフォーマンスが低下する可能性があります。|  
|max_dispatch_latency|**int**|イベントをセッション ターゲットに渡す前にメモリにバッファリングする時間 (ミリ秒単位)。 有効な値は、1 ~ 2147483648、-1 です。 値-1 は、ディスパッチの待機時間が無限であることを示します。 NULL 値が許可されます。|  
|max_memory|**int**|イベントのバッファリングのためにセッションに割り当てられたメモリの量。 既定値は 4 MB です。 NULL 値が許可されます。|  
|max_event_size|**int**|イベント セッション バッファーに収まらないイベント用に確保するメモリの量。 計算されたバッファー サイズを max_event_size が超える場合、サイズが max_event_size のバッファーが追加で 2 つイベント セッションに割り当てられます。 NULL 値が許可されます。|  
|memory_partition_mode|**nchar(1)**|イベントバッファーが作成されるメモリ内の場所。 既定のパーティション モードは G です。NULL 値は許可されません。 memory_partition_mode は次のいずれかです。<br /><br /> G : NONE<br /><br /> C-PER_CPU<br /><br /> N-PER_NODE|  
|memory_partition_mode_desc|**sysname**|既定値は NONE です。 NULL 値は許可されません。 は次のいずれかです。<br /><br /> NONE。 1 つのバッファー セットが SQL Server インスタンス内で作成されます。<br /><br /> PER_CPU。 CPU ごとにバッファーのセットが作成されます。<br /><br /> PER_NODE。 NUMA (non-uniform memory access) ノードごとに、一連のバッファーが作成されます。|  
|track_causality|**bit**|因果関係の追跡を有効または無効にします。 1 (ON) に設定すると、追跡が有効になり、異なるサーバー接続上の関連イベントを関連付けることができます。 既定の設定は 0 (オフ) です。 NULL 値は許可されません。|  
|startup_state|**bit**|値は、サーバーの起動時にセッションを自動的に開始するかどうかを決定します。 既定値は 0 です。 NULL 値は許可されません。 次のいずれか:<br /><br /> 0 (オフ)。 サーバーの起動時にセッションは開始されません。<br /><br /> 1 (ON)。 サーバーの起動時にイベント セッションが開始されます。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
  
