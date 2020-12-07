---
description: ビュー (Integration Services カタログ)
title: ビュー (Integration Services カタログ) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- views [Integration Services]
ms.assetid: d0294d43-4852-46dc-9afa-d0c19ea9aa03
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d4dfe305d34435dd1b09dc825021995e1a9cb75d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421956"
---
# <a name="views-integration-services-catalog"></a>ビュー (Integration Services カタログ)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  このセクションでは、[!INCLUDE[tsql](../../includes/tsql-md.md)] のインスタンスに配置されている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを管理できる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ビューについて説明します。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ビューに対してクエリを実行すると、**SSISDB** カタログに格納されているオブジェクト、設定、および業務データを検査できます。  
  
 カタログの既定の名前は、SSISDB です。 カタログに格納されているオブジェクトには、プロジェクト、パッケージ、パラメーター、環境、操作履歴があります。  
  
 データベース ビューとストアド プロシージャを直接使用することも、マネージド API を呼び出すカスタム コードを記述することもできます。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] およびマネージド API では、ビューに対してクエリを実行し、多くのタスクを実行するストアド プロシージャ (このセクションで説明) を呼び出します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [catalog.catalog_properties &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのプロパティを表示します。  
  
 [catalog.effective_object_permissions &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-effective-object-permissions-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのすべてのオブジェクトの現在のプリンシパルに対する有効な権限を表示します。  
  
 [catalog.environment_variables &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-environment-variables-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのすべての環境に対する環境変数の詳細を表示します。  
  
 [catalog.environments &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-environments-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのすべての環境に対する環境の詳細を表示します。 環境には、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトが参照できる変数が含まれています。  
  
 [catalog.execution_parameter_values &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)  
 インスタンスの実行中に [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージによって使用される実際のパラメーター値を表示します。  
  
 [catalog.executions &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのパッケージ実行のインスタンスを表示します。 パッケージ実行タスクで実行されるパッケージは、親パッケージと同じ実行のインスタンスで実行されます。  
  
 [catalog.explicit_object_permissions &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-explicit-object-permissions-ssisdb-database.md)  
 ユーザーに明示的に割り当てられた権限のみを表示します。  
  
 [catalog.extended_operation_info &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのすべての操作に対する拡張された情報を表示します。  
  
 [catalog.folders &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-folders-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのフォルダーを表示します。  
  
 [catalog.object_parameters &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのすべてのパッケージおよびプロジェクトのパラメーターを表示します。  
  
 [catalog.object_versions &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-object-versions-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのオブジェクトのバージョンを示します。 このリリースでは、プロジェクトのバージョンのみがこのビューでサポートされます。  
  
 [catalog.operation_messages &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログでの操作中に記録されるメッセージを表示します。  
  
 [catalog.operations &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのすべての操作の詳細を表示します。  
  
 [catalog.packages &#40;SSISDB データ&#41;](../../integration-services/system-views/catalog-packages-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログに表示されるすべてのパッケージの詳細を表示します。  
  
 [catalog.environment_references &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-environment-references-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのすべてのプロジェクトに対する環境参照を表示します。  
  
 [catalog.projects &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-projects-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログに表示されるすべてのプロジェクトの詳細を表示します。  
  
 [catalog.validations &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-validations-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのすべてのプロジェクトおよびパッケージ検証の詳細を表示します。  
  
[catalog.master_properties &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-master-properties-ssisdb-database.md)  
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Master のプロパティを表示します。

[catalog.worker_agents &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-worker-agents-ssisdb-database.md)  
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker の情報を表示します。  
