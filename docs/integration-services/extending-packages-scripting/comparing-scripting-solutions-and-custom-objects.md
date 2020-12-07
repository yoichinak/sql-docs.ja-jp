---
description: スクリプティング ソリューションとカスタム オブジェクトとの比較
title: スクリプティング ソリューションとカスタム オブジェクトとの比較 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- managed tasks [Integration Services]
- Script task [Integration Services], vs. custom managed tasks
- SSIS Script task, vs. custom managed tasks
- custom tasks [Integration Services], scripts
ms.assetid: c0aea822-a21e-44e1-a3d3-8777bd0a1c34
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d0e862da85c7c3c2e2255bbd522045b507b5d471
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88430314"
---
# <a name="comparing-scripting-solutions-and-custom-objects"></a>スクリプティング ソリューションとカスタム オブジェクトとの比較

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] スクリプト タスクまたはスクリプト コンポーネントは、カスタム マネージド タスクまたはデータ フロー コンポーネントで使用できる機能とほぼ同じ機能を実装できます。 ここでは、適切な種類のタスクを必要に応じて選択するときに役立つ注意事項について説明します。  
  
-   構成または機能が個々のパッケージに固有である場合は、カスタム オブジェクトを開発する代わりに、スクリプト タスクまたはスクリプト コンポーネントを使用します。  
  
-   機能が汎用で、将来は他のパッケージ用に使用されたり、他の開発者が使用する可能性がある場合は、スクリプト ソリューションを使用する代わりに、カスタム オブジェクトを作成します。 カスタム オブジェクトは任意のパッケージで使用できますが、スクリプトは、そのスクリプトが作成されたパッケージでのみ使用できます。  
  
-   同じパッケージ内でコードを再使用する場合、カスタム オブジェクトを作成することを検討します。 あるスクリプト タスクまたはコンポーネントから別のスクリプト タスクまたはコンポーネントにコードをコピーすると、コードの複数コピーの維持および更新が煩雑になるため、管理が難しくなります。  
  
-   将来的に実装方法を変更する場合は、カスタム オブジェクトの使用を検討します。 カスタム オブジェクトは、親パッケージとは別に開発および配置できますが、スクリプト ソリューションを更新する場合は、パッケージ全体を再配置する必要があります。  
  
## <a name="see-also"></a>関連項目  
 [カスタム オブジェクトを使用したパッケージの拡張](../../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
  
  
