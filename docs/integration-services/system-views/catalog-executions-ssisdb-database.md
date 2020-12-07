---
description: catalog.executions (SSISDB データベース)
title: catalog.executions (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- executions view [Integration Services]
- catalog.executions view [Integration Services]
ms.assetid: 879f13b0-331d-4dee-a079-edfaca11ae5b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 438d551f45447b0b03b075576af9cffb2bde8a36
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425104"
---
# <a name="catalogexecutions-ssisdb-database"></a>catalog.executions (SSISDB データベース)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのパッケージ実行のインスタンスを表示します。 パッケージ実行タスクで実行されるパッケージは、親パッケージと同じ実行のインスタンスで実行されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|execution_id|**bigint**|実行のインスタンスの一意の識別子 (ID)。|  
|folder_name|**sysname(nvarchar(128))**|プロジェクトを含むフォルダーの名前。|  
|project_name|**sysname(nvarchar(128))**|プロジェクトの名前です。|  
|package_name|**nvarchar(260)**|実行中に開始された最初のパッケージの名前。|  
|reference_id|**bigint**|実行のインスタンスによって参照される環境。|  
|reference_type|**char(1)**|環境をプロジェクトと同じフォルダーに配置できるか (相対参照)、または別のフォルダーに配置できるか (絶対参照) を示します。 値が `R` の場合、環境は相対参照を使用して配置されます。 値が `A` の場合、環境は絶対参照を使用して配置されます。|  
|environment_folder_name|**nvarchar(128)**|環境を含むフォルダーの名前です。|  
|environment_name|**nvarchar(128)**|実行中に参照された環境の名前。|  
|project_lsn|**bigint**|実行のインスタンスに対応するプロジェクトのバージョン。 この番号は、シーケンシャルを保証するものではありません。|  
|executed_as_sid|**varbinary(85)**|実行のインスタンスを起動したユーザーの SID。|  
|executed_as_name|**nvarchar(128)**|実行のインスタンスを起動するために使用されたデータベース プリンシパルの名前。|  
|use32bitruntime|**bit**|64 ビット オペレーティング システムで 32 ビットのランタイムを使用してパッケージを実行するかどうかを示します。 値が `1` の場合、実行は 32 ビット ランタイムで実行されます。 値が `0` の場合、実行は 64 ビット ランタイムで実行されます。|  
|object_type|**smallint**|オブジェクトの型。 オブジェクトは、プロジェクト (`20`) またはパッケージ (`30`) です。|  
|object_id|**bigint**|操作の影響を受けるオブジェクトの ID。|  
|status|**int**|操作のステータス。 使用される可能性がある値は、作成済み (`1`)、実行中 (`2`)、取り消し済み (`3`)、失敗 (`4`)、保留中 (`5`)、予期しない終了 (`6`)、成功 (`7`)、停止 (`8`)、および完了 (`9`) です。|  
|start_time|**datetimeoffset**|実行のインスタンスが起動された時間。|  
|end_time|**datetimeoffsset**|実行のインスタンスが終了した時間。|  
|caller_sid|**varbinary(85)**|ログオンに Windows 認証が使用された場合はユーザーのセキュリティ ID (SID)。|  
|caller_name|**nvarchar(128)**|操作を実行したアカウントの名前。|  
|process_id|**int**|外部プロセスのプロセス ID (該当する場合)。|  
|stopped_by_sid|**varbinary(85)**|実行のインスタンスを停止したユーザーのセキュリティ ID (SID)。|  
|stopped_by_name|**nvarchar(128)**|実行のインスタンスを停止したユーザーの名前。|  
|total_physical_memory_kb|**bigint**|実行開始時にサーバーに搭載されている物理メモリの合計 (MB 単位)。|  
|available_physical_memory_kb|**bigint**|実行開始時にサーバーで利用可能な物理メモリの量 (MB 単位)。|  
|total_page_file_kb|**bigint**|実行開始時にサーバーに搭載されているページ メモリの合計 (MB 単位)。|  
|available_page_file_kb|**bigint**|実行開始時にサーバーで利用可能なページ メモリの量 (MB 単位)。|  
|cpu_count|**int**|実行開始時のサーバー上の論理 CPU の数。|  
|server_name|**nvarchar(128)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の指定されたインスタンスに関する Windows サーバーとインスタンスの情報。|  
|machine_name|**nvarchar(128)**|サーバー インスタンスが稼働しているコンピューターの名前。|  
|dump_id|**uniqueidentifier**|実行ダンプの ID。|  
  
## <a name="remarks"></a>注釈  
 このビューは、カタログの実行の各インスタンスの行を表示します。  
  
## <a name="permissions"></a>アクセス許可  
 このビューには、次の権限のいずれかが必要です。  
  
-   実行のインスタンスの READ 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
> [!NOTE]  
>  行レベルのセキュリティが適用されるため、表示する権限がある行のみが表示されます。  
  
  
