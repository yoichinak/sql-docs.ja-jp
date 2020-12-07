---
description: catalog.extended_operation_info (SSISDB データベース)
title: catalog.extended_operation_info (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: db299b45-557d-4c62-8e14-355cdb051f63
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c4082c0bbf428a96776ae18fece7333f0401a2b6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422076"
---
# <a name="catalogextended_operation_info-ssisdb-database"></a>catalog.extended_operation_info (SSISDB データベース)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのすべての操作に対する拡張された情報を表示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|info_id|**bigint**|拡張された情報の一意識別子 (ID)。|  
|operation_id|**bigint**|拡張された情報に対応する操作の一意の ID。|  
|object_name|**nvarchar(260)**|オブジェクトの名前。|  
|object_type|**smallint**|操作の影響を受けるオブジェクトの種類。 オブジェクトは、フォルダー (`10`)、プロジェクト (`20`)、パッケージ (`30`)、環境 (`40`)、または実行のインスタンス (`50`) です。|  
|reference_id|**bigint**|操作で使用される参照の一意の ID。|  
|status|**int**|操作のステータス。 使用される可能性がある値は、作成済み (`1`)、実行中 (`2`)、取り消し済み (`3`)、失敗 (`4`)、保留中 (`5`)、予期しない終了 (`6`)、成功 (`7`)、停止 (`8`)、および完了 (`9`) です。|  
|start_time|**datetimeoffset(7)**|操作が開始された日時。|  
|end_time|**datetimeoffset(7)**|操作が終了した日時。|  
  
## <a name="remarks"></a>解説  
 1 回の操作で、複数の拡張された情報行を指定できます。  
  
## <a name="permissions"></a>アクセス許可  
 このビューには、次の権限のいずれかが必要です。  
  
-   この操作の READ 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
> [!NOTE]  
>  サーバー上で操作を実行する権限がある場合は、操作に関する情報を表示する権限もあります。 行レベルのセキュリティが適用されるため、表示する権限がある行のみが表示されます。  
  
  
