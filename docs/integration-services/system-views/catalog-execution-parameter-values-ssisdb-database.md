---
description: catalog.execution_parameter_values (SSISDB データベース)
title: catalog.execution_parameter_values (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: ec93e67b-04ce-4aae-ab96-3ad20e9793ad
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 022d1d29438da9bebeb7e7544b01445f27803fce
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495227"
---
# <a name="catalogexecution_parameter_values-ssisdb-database"></a>catalog.execution_parameter_values (SSISDB データベース)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  インスタンスの実行中に [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージによって使用される実際のパラメーター値を表示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|execution_parameter_id|**bigint**|実行パラメーターの一意識別子 (ID)。|  
|execution_id|**bigint**|実行のインスタンスの一意の ID。|  
|object_type|**smallint**|値が `20` の場合、パラメーターはプロジェクト パラメーターです。 値が `30` の場合、パラメーターはパッケージ パラメーターです。 値が `50` の場合、パラメーターは次のいずれかです。<br /><br /> **LOGGING_LEVEL**<br /><br /> **DUMP_ON_ERROR**<br /><br /> **DUMP_ON_EVENT**<br /><br /> **DUMP_EVENT_CODE**<br /><br /> **CALLER_INFO**<br /><br /> **SYNCHRONIZED**|  
|parameter_data_type|**nvarchar(128)**|パラメーターのデータ型です。|  
|parameter_name|**sysname**|パラメーターの名前。|  
|parameter_value|**sql_variant**|パラメーターの値。 sensitive が `0` の場合、プレーンテキストの値が表示されます。 sensitive が `1` の場合、**NULL** 値が表示されます。|  
|sensitive|**bit**|値が `1` の場合、パラメーター値はセンシティブです。 値が `0` の場合、パラメーター値はセンシティブではありません。|  
|必須|**bit**|値が `1` の場合、実行を開始するためパラメーター値が必要です。 値が `0` の場合、実行を開始するためのパラメーター値は不要です。|  
|value_set|**bit**|値が `1` の場合、パラメーター値は割り当てられています。 値が `0` の場合、パラメーター値は割り当てられていません。|  
|runtime_override|**bit**|値が `1` の場合、実行が開始される前に、パラメーター値が元の値から変更されました。 値が `0` の場合、パラメーター値は割り設定された元の値です。|  
  
## <a name="remarks"></a>解説  
 このビューは、カタログの実行の各パラメーターの行を表示します。 実行パラメーター値は、1 つのインスタンスの実行中にプロジェクト パラメーターまたはパッケージ パラメーターに割り当てられた値です。  
  
## <a name="permissions"></a>アクセス許可  
 このビューには、次の権限のいずれかが必要です。  
  
-   実行のインスタンスの READ 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
> [!NOTE]  
>  サーバー上で操作を実行する権限がある場合は、操作に関する情報を表示する権限もあります。 行レベルのセキュリティが適用されるため、表示する権限がある行のみが表示されます。  
  
  
