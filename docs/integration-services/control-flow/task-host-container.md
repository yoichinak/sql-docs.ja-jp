---
description: タスク ホスト コンテナー
title: タスク ホスト コンテナー | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.taskhostcontainer.f1
helpviewer_keywords:
- containers [Integration Services], Task Host
- Task Host container
ms.assetid: 7394a2c2-1b07-427d-b94a-9792e7783d35
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b1c57dbe96b038857a329b17d7d9e17b31565102
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192815"
---
# <a name="task-host-container"></a>タスク ホスト コンテナー

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  タスク ホスト コンテナーは、1 つのタスクをカプセル化します。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでは、タスク ホストは個別には構成されず、カプセル化するタスクのプロパティを設定する際に構成されます。 タスク ホスト コンテナーがカプセル化するタスクの詳細については、「 [Integration Services タスク](../../integration-services/control-flow/integration-services-tasks.md)」を参照してください。  
  
 タスク ホスト コンテナーは、変数とイベント ハンドラーの使用を、タスク レベルに拡張します。 詳細については、「[Integration Services (SSIS) のイベント ハンドラー](../../integration-services/integration-services-ssis-event-handlers.md)」および「[Integration Services (SSIS) の変数](../../integration-services/integration-services-ssis-variables.md)」を参照してください。  
  
## <a name="configuration-of-the-task-host"></a>タスク ホストの構成  
 プロパティを設定するには、 **の** [プロパティ] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ウィンドウで行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]でのこれらのプロパティの設定については、「 [タスクまたはコンテナーのプロパティを設定する](./add-or-delete-a-task-or-a-container-in-a-control-flow.md)」を参照してください。  
  
 プログラムによってこれらのプロパティを設定する方法については、 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [タスクまたはコンテナーのプロパティを設定する](./add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
## <a name="see-also"></a>参照  
 [Integration Services コンテナー](../../integration-services/control-flow/integration-services-containers.md)  
  
