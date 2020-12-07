---
description: catalog.object_parameters (SSISDB データベース)
title: catalog.object_parameters (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: d7b04903-2d61-4159-9456-475942d1f732
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 856676c6ad5330e6039711d7a391bdd264a2b062
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422046"
---
# <a name="catalogobject_parameters-ssisdb-database"></a>catalog.object_parameters (SSISDB データベース)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのすべてのパッケージおよびプロジェクトのパラメーターを表示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|parameter_id|**bigint**|パラメーターの一意識別子 (ID)。|  
|project_id|**bigint**|プロジェクトの一意な ID。|  
|object_type|**smallint**|パラメーターの型。 プロジェクト パラメーターでは値は `20`、パッケージ パラメーターでは値は `30` です。|  
|object_name|**sysname**|対応するプロジェクトまたはパッケージの名前。|  
|parameter_name|**sysname(nvarchar(128))**|パラメーターの名前。|  
|data_type|**nvarchar(128)**|パラメーターのデータ型です。|  
|必須|**bit**|値が `1` の場合、実行を開始するためパラメーター値が必要です。 値が `0` の場合、実行を開始するためのパラメーター値は不要です。|  
|sensitive|**bit**|値が `1` の場合、パラメーター値はセンシティブです。 値が `0` の場合、パラメーター値はセンシティブではありません。|  
|description|**nvarchar(1024)**|パッケージの説明 (省略可)。|  
|design_default_value|**sql_variant**|プロジェクトまたはパッケージの設計中に割り当てられたパラメーターの既定値。|  
|default_value|**sql_variant**|サーバーで現在使用されている既定値。|  
|value_type|**char(1)**|パラメーター値の型を示します。 このフィールドには、parameter_value がリテラル値の場合は `V`、環境変数を参照することによって値が割り当てられる場合は `R` が表示されます。|  
|value_set|**bit**|値が `1` の場合、パラメーター値は割り当てられています。 値が `0` の場合、パラメーター値は割り当てられていません。|  
|referenced_variable_name|**nvarchar(128)**|パラメーターの値が割り当てられる環境変数の名前。 既定値は **NULL** です。|  
|validation_status|**char(1)**|単に情報を示すためだけに特定されます。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では使用されません。|  
|last_validation_time|**datetimeoffset(7)**|単に情報を示すためだけに特定されます。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では使用されません。|  
  
## <a name="permissions"></a>アクセス許可  
 このビュー内の行を表示するには、次のアクセス権限のいずれかが必要です。  
  
-   プロジェクトに対する READ 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
 行レベルのセキュリティが適用されるため、表示する権限がある行のみが表示されます。  
  
  
