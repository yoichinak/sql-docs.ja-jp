---
description: catalog.projects (SSISDB データベース)
title: catalog.projects (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: a6b595e1-5227-47ce-8ee2-a28c1e1d5645
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 874d4a89af11ab022ce2714334b9aefb506de1a6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421996"
---
# <a name="catalogprojects-ssisdb-database"></a>catalog.projects (SSISDB データベース)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **SSISDB** カタログに表示されるすべてのプロジェクトの詳細を表示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|project_id|**bigint**|プロジェクトの一意識別子 (ID)。|  
|folder_id|**bigint**|プロジェクトがあるフォルダーの一意の ID。|  
|name|**sysname**|プロジェクトの名前です。|  
|description|**nvarchar(1024)**|プロジェクトの説明 (省略可)。|  
|project_format_version|**int**|プロジェクトの開発に使用された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョン。|  
|deployed_by_sid|**varbinary(85)**|プロジェクトをインストールしたユーザーのセキュリティ識別子 (SID)。|  
|deployed_by_name|**nvarchar(128)**|プロジェクトをインストールしたユーザーの名前。|  
|last_deployed_time|**datetimeoffset(7)**|パッケージを配置または再配置した日付と時刻。|  
|created_time|**datetimeoffset(7)**|プロジェクトが作成された日時。|  
|object_version_lsn|**bigint**|プロジェクトのバージョン。 この番号は、シーケンシャルを保証するものではありません。|  
|validation_status|**char(1)**|検証状態。|  
|last_validation_time|**datetimeoffset(7)**|前回の検証操作の時刻。|  
  
## <a name="remarks"></a>解説  
 このビューは、カタログの各プロジェクトの行を表示します。  
  
## <a name="permissions"></a>アクセス許可  
 このビューには、次の権限のいずれかが必要です。  
  
-   プロジェクトに対する READ 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ。  
  
> [!NOTE]  
>  プロジェクトの READ 権限がある場合は、そのプロジェクトに関連付けられたすべてのパッケージおよび環境の READ 権限もあります。 行レベルのセキュリティが適用されるため、表示する権限がある行のみが表示されます。  
  
  
