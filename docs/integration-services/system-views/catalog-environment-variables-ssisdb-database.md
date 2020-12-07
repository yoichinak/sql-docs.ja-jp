---
description: catalog.environment_variables (SSISDB データベース)
title: catalog.environment_variables (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 45f5aacd-505a-443b-8fc2-c7929e78cff8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b76045d5f901fa1444fd016d1c7673f46170332d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495336"
---
# <a name="catalogenvironment_variables-ssisdb-database"></a>catalog.environment_variables (SSISDB データベース)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのすべての環境に対する環境変数の詳細を表示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|variable_id|**bigint**|環境変数の一意識別子 (ID)。|  
|environment_id|**bigint**|変数が関連付けられている環境の一意の ID。|  
|name|**sysname**|環境変数の名前。|  
|description|**nvarchar(1024)**|環境変数の説明。|  
|type|**nvarchar(128)**|環境変数のデータ型。|  
|sensitive|**bit**|値が `1` のとき、変数はセンシティブで、格納されるときに暗号化されます。 値が `0` のとき、変数はセンシティブではなく、値はプレーンテキストで格納されます。|  
|value|**sql_variant**|環境変数の値。 sensitive が `0` の場合、プレーンテキストの値が表示されます。 sensitive が `1` の場合、**NULL** 値が表示されます。|  
  
## <a name="remarks"></a>解説  
 このビューは、カタログの各環境変数の行を表示します。  
  
## <a name="permissions"></a>アクセス許可  
 このビューには、次の権限のいずれかが必要です。  
  
-   対応する環境に対する READ 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
> [!NOTE]  
>  サーバー上で操作を実行する権限がある場合は、操作に関する情報を表示する権限もあります。 行レベルのセキュリティが適用されるため、表示する権限がある行のみが表示されます。  
  
  
