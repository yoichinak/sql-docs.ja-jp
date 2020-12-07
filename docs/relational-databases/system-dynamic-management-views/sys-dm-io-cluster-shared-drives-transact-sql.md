---
description: dm_io_cluster_shared_drives (Transact-sql)
title: dm_io_cluster_shared_drives (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_io_cluster_shared_drives_TSQL
- sys.dm_io_cluster_shared_drives
- dm_io_cluster_shared_drives_TSQL
- dm_io_cluster_shared_drives
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_io_cluster_shared_drives dynamic management view
ms.assetid: c8fcced8-c780-49dc-99bd-6beb3ca532c4
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 52582d7377ab7a8df39e7b752a4e7842d8c6c1fc
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89532709"
---
# <a name="sysdm_io_cluster_shared_drives-transact-sql"></a>dm_io_cluster_shared_drives (Transact-sql)
[!INCLUDE [sql-asdbmi-pdw](../../includes/applies-to-version/sql-asdbmi-pdw.md)]

  現在のサーバーインスタンスがクラスター化されたサーバーの場合、このビューは各共有ドライブのドライブ名を返します。 現在のサーバーインスタンスがクラスター化されたインスタンスでない場合は、空の行セットが返されます。  
  
> [!NOTE]  
>  これをから呼び出すには [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 、 **dm_pdw_nodes_io_cluster_shared_drives**という名前を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**DriveName**|**nchar(2)**|クラスターの共有ディスクアレイに参加している個々のディスクを表すドライブ (ドライブ文字) の名前。 NULL 値は許可されません。|  
|**pdw_node_id**|**int**|**適用対象**: ssPDW<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="remarks"></a>解説  
 クラスタリングが有効になっている場合、フェールオーバークラスターインスタンスは、インスタンスが別のノードにフェールオーバーした後にアクセスできるように、共有ディスク上にデータファイルとログファイルを配置する必要があります。 このビューの各行は、クラスター化された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで使用される 1 つの共有ディスクを表します。 このビューによって一覧表示されたディスクのみを使用して、のこのインスタンスのデータファイルまたはログファイルを格納でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 このビューに表示されているディスクは、そのインスタンスに関連付けられているクラスターリソースグループ内のディスクです。  
  
> [!NOTE]  
>  このビューは、今後のリリースで非推奨とされる予定です。 代わりに、 [dm_io_cluster_valid_path_names &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql.md) を使用することをお勧めします。  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、sys.dm_io_cluster_shared_drives を使用して、クラスター サーバー インスタンスの共有デバイスを特定します。  
  
```  
SELECT * FROM sys.dm_io_cluster_shared_drives;  
```  
  
 結果セットは次のようになります。  
  
 DriveName  
  
 --------\-  
  
 m  
  
 n  
  
## <a name="see-also"></a>参照  
 [dm_io_cluster_valid_path_names &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql.md)   
 [dm_os_cluster_nodes &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [fn_servershareddrives &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-servershareddrives-transact-sql.md)   
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  
