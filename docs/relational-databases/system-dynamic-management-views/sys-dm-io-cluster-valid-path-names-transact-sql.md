---
description: dm_io_cluster_valid_path_names (Transact-sql)
title: dm_io_cluster_valid_path_names (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_io_cluster_valid_path_names
- dm_io_cluster_valid_path_names_TSQL
- sys.dm_io_cluster_valid_path_names_TSQL
- dm_io_cluster_valid_path_names
dev_langs:
- TSQL
helpviewer_keywords:
- dm_io_cluster_valid_path_names
- sys.dm_io_cluster_valid_path_names
- cluster valid path names
- csv name
- cluster shared volume names
ms.assetid: 5bc8a0e5-6c72-425b-8c58-f276eb9add2c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 18a1e01e893486a7ce32f1c3510fb52d5fd7ec0e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89532145"
---
# <a name="sysdm_io_cluster_valid_path_names-transact-sql"></a>dm_io_cluster_valid_path_names (Transact-sql)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  SQL Server フェールオーバー クラスター インスタンスに対応するクラスター化ボリュームを含む、すべての有効な共有ディスクに関する情報を返します。 インスタンスがクラスター化されていない場合は、空の行セットが返されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**path_name**|**Nvarchar (512)**|データベースおよびログファイルのルートディレクトリとして使用できるボリュームマウントポイントまたはドライブパス。 NULL 値は許可されません。|  
|**cluster_owner_node**|**Nvarchar (64)**|ドライブの現在の所有者。 クラスター共有ボリューム (CSV) の場合、所有者はメタデータサーバーをホストしているノードです。 NULL 値は許可されません。|  
|**is_cluster_shared_volume**|**ビット**|このパスを含むドライブがクラスター化ボリュームの場合は 1 を返します。それ以外の場合は 0 を返します。|  
  
## <a name="remarks"></a>解説  
 SQL Server フェールオーバークラスターインスタンス (FCI) は、FCI のすべてのノード間でデータとログファイルの保存に共有ストレージを使用する必要があります。 このビューに表示されているディスクは、インスタンスに関連付けられているクラスターリソースグループに含まれていて、データまたはログファイルの格納に使用できる唯一のディスクです。  
  
> [!NOTE]  
>  今後のリリースでは、このビューによって [dm_io_cluster_shared_drives &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md) が置き換えられます。  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、sys.dm_io_cluster_valid_path_names を使用して、クラスター サーバー インスタンスの共有デバイスを特定します。  
  
```  
SELECT * FROM sys.dm_io_cluster_valid_path_names;  
```  
  
## <a name="see-also"></a>参照  
 [dm_os_cluster_nodes &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [dm_io_cluster_shared_drives &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md)   
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

