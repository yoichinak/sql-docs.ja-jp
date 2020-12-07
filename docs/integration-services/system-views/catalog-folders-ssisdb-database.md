---
description: catalog.folders (SSISDB データベース)
title: catalog.folders (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 21a37c16-60aa-4b3f-8bca-ac90ad1697ac
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8ec7f8fad821c5c62d7b7ec58290050a52b0bf17
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422066"
---
# <a name="catalogfolders-ssisdb-database"></a>catalog.folders (SSISDB データベース)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのフォルダーを表示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|id|**bigint**|フォルダーの一意識別子。|  
|name|**sysname(nvarchar(128)**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログ内で一意のフォルダーの名前。|  
|description|**nvarchar(1024)**|フォルダーの説明。|  
|created_by_sid|**varbinary(85)**|フォルダーを作成したユーザーの一意なセキュリティ識別子 (SID)。|  
|created_by_name|**nvarchar(128)**|フォルダーを作成したユーザーの名前。|  
|created_time|**datetimeoffset(7)**|フォルダーが作成された日時。|  
  
## <a name="remarks"></a>解説  
 このビューは、カタログの各フォルダーの行を表示します。  
  
## <a name="permissions"></a>アクセス許可  
 このビューには、次の権限のいずれかが必要です。  
  
-   フォルダーの READ 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
> [!NOTE]  
>  サーバー上で操作を実行する権限がある場合は、操作に関する情報を表示する権限もあります。 行レベルのセキュリティが適用されるため、表示する権限がある行のみが表示されます。  
  
  
