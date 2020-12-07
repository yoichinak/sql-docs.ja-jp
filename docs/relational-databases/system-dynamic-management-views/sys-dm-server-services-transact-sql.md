---
description: dm_server_services (Transact-sql)
title: dm_server_services (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 01/07/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_server_services
- sys.dm_server_services
- sys.dm_server_services_TSQL
- dm_server_services_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_server_services dynamic management view
ms.assetid: 3f0defd0-478d-4e7f-96be-8795c9de4e3f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c1b013b97e15fafbc35c1f2120892d9382ea1bc2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546475"
---
# <a name="sysdm_server_services-transact-sql"></a>dm_server_services (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  の現在のインスタンスの SQL Server、フルテキスト、SQL Server Launchpad サービス (SQL Server 2017 +)、および SQL Server エージェントの各サービスに関する情報を返し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 これらのサービスに関するステータス情報を報告するには、この動的管理ビューを使用します。  
  
 
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|servicename|**nvarchar (256)**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]、フルテキスト、または SQL Server エージェントサービスの名前。 null にすることはできません。|  
|startup_type|**int**|サービスの開始モードを示します。 有効な値とそれに対応する説明を次に示します。<br /><br /> 0:その他<br />1: その他<br />2: 自動<br />3: 手動<br />4: 無効<br /><br /> NULL 値が許可されます。|  
|startup_type_desc|**nvarchar (256)**|サービスの開始モードについて説明します。 有効な値とそれに対応する説明を次に示します。<br /><br /> その他: その他 (ブート開始)<br />Other: Other (システム開始)<br />自動: 自動開始<br />手動: 要求の開始<br />Disabled: Disabled<br /><br /> null にすることはできません。|  
|status|**int**|サービスの現在の状態を示します。 有効な値とそれに対応する説明を次に示します。<br /><br /> 1: 停止しました<br />2: その他 (開始待ち)<br />3: その他 (停止保留中)<br />4: 実行中<br />5: その他 (保留の継続)<br />6: その他 (一時停止保留中)<br />7: 一時停止<br /><br /> NULL 値が許可されます。|  
|status_desc|**nvarchar (256)**|サービスの現在の状態を記述します。 有効な値とそれに対応する説明を次に示します。<br /><br /> Stopped: サービスは停止しています。<br />その他 (操作の開始が保留中): サービスは開始処理中です。<br />その他 (保留中の操作の停止): サービスは停止処理中です。<br />Running: サービスは実行中です。<br />その他 (続行操作が保留中): サービスは保留中の状態です。<br />その他 (一時停止待ち): サービスは一時停止処理中です。<br />一時停止: サービスは一時停止されています。<br /><br /> null にすることはできません。|  
|process_id|**int**|サービスのプロセス ID。 null にすることはできません。|  
|last_startup_time|**datetimeoffset(7)**|サービスが最後に開始された日時。 NULL 値が許可されます。|  
|service_account|**nvarchar (256)**|サービスを制御する権限が与えられているアカウント。 このアカウントでは、サービスの開始や停止、またはサービス プロパティの変更が可能です。 null にすることはできません。|  
|filename|**nvarchar (256)**|サービスの実行可能ファイルのパスとファイル名。 null にすることはできません。|  
|is_clustered|**nvarchar (1)**|サービスがクラスターサーバーのリソースとしてインストールされているかどうかを示します。 null にすることはできません。|  
|cluster_nodename|**nvarchar (256)**|サービスがインストールされているクラスター ノードの名前。 NULL 値が許可されます。|
|instant_file_initialization_enabled|**nvarchar (1)**|サービスに対してファイルの瞬時初期化を有効にするかどうかを指定し [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ます。<br /><br />Y = サービスに対してファイルの瞬時初期化が有効になっています。<br /><br />N = サービスに対してファイルの瞬時初期化が無効になっています。<br /><br /> NULL 値が許可されます。<br /><br /> **注:** は、SQL Server エージェントなどの他のサービスには適用されません。<br /><br /> **適用対象:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (以降 [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4、 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以降) をインストールします。|  

## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 サーバーに対する `VIEW SERVER STATE` 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [dm_server_registry &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md)  
  
