---
description: catalog.environments (SSISDB データベース)
title: catalog.environments (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 7014c0e3-65dc-4a46-842e-4decf3737748
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 426199180acf6aafc609250638d00d1deb9231ec
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495283"
---
# <a name="catalogenvironments-ssisdb-database"></a>catalog.environments (SSISDB データベース)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのすべての環境に対する環境の詳細を表示します。 環境には、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトが参照できる変数が含まれています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|environment_id|**bigint**|環境の一意識別子 (ID)。|  
|name|**sysname**|環境の名前。|  
|folder_id|**bigint**|環境が存在するフォルダーの一意の ID。|  
|description|**nvarchar(1024)**|環境の説明。 この値は省略可能です。|  
|created_by_sid|**varbinary(85)**|環境を作成したユーザーのセキュリティ識別子 (SID)。|  
|created_by_name|**nvarchar(128)**|環境を作成したユーザーの名前。|  
|created_time|**datetimeoffset**|環境が作成された日時。|  
  
## <a name="remarks"></a>解説  
 このビューは、カタログの各環境の行を表示します。 環境名は、環境が配置されているフォルダーに関してのみ一意です。 たとえば、`E1` という名前の環境をカタログの複数のフォルダーに指定できますが、各フォルダーで使用できる `E1` という名前の環境は 1 つのみです。  
  
## <a name="permissions"></a>アクセス許可  
 このビューには、次の権限のいずれかが必要です。  
  
-   環境に対する READ 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
> [!NOTE]  
>  行レベルのセキュリティが適用されるため、表示する権限がある行のみが表示されます。  
  
  
