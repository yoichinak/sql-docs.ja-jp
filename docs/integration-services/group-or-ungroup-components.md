---
description: コンポーネントのグループ化とグループの解除
title: コンポーネントのグループ化とグループの解除 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- grouping containers
- tasks [Integration Services], grouping
- containers [Integration Services], grouping
- grouping tasks
ms.assetid: 34320838-c271-4f8c-90b3-1254690890bb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7cd88383577694d5bef248baea5004056d239136
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "92195210"
---
# <a name="group-or-ungroup-components"></a>コンポーネントのグループ化とグループの解除

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  **デザイナーの**[制御フロー] **、**[データ フロー] **、および** [イベント ハンドラー] [!INCLUDE[ssIS](../includes/ssis-md.md)] タブでは、折りたたみ可能なグループ化がサポートされています。 パッケージに多数のコンポーネントがある場合、タブは過密状態になることがあります。このような状態になると、すべてのコンポーネントを一度に表示するのが難しくなり、操作する項目を探すのも困難になります。 折りたたみ可能なグループ化機能を使用すると、作業画面上の領域を節約でき、大きなパッケージの処理が容易になります。  
  
 グループ化機能では、グループ化するコンポーネントを選択し、それらをグループ化します。次に、作業に合わせてグループを展開するか、折りたたみます。 グループを展開すると、グループ内のコンポーネントのプロパティにアクセスできます。 タスクとコンテナーを連結する優先順位制約は、自動的にグループ内に含まれます。  
  
 コンポーネントのグループ化に関する注意事項は次のとおりです。  
  
-   コンポーネントをグループ化するには、コントロール フロー、データ フロー、またはイベント ハンドラーに複数のコンポーネントが含まれている必要があります。  
  
-   グループは入れ子にすることもできます。これにより、グループ内にグループを作成できます。 デザイン画面は、入れ子になっていないグループを複数実装できます。ただし、グループが入れ子になっていない場合、コンポーネントが所属できるのは 1 グループのみです。  
  
-   [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーは、パッケージの保存時にグループ化を保存します。ただし、グループ化はパッケージの実行には影響しません。 コンポーネントのグループ化機能は、デザイン時の機能であり、パッケージの実行時の動作には影響しません。  
  
### <a name="to-group-components"></a>コンポーネントをグループ化するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]**、 **[データ フロー]**、または **[イベント ハンドラー]** タブをクリックします。  
  
4.  タブのデザイン画面で、グループ化するコンポーネントを選択します。選択したコンポーネントを右クリックし、 **[グループ]** をクリックします。  
  
5.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
### <a name="to-ungroup-components"></a>コンポーネントのグループを解除するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]**、 **[データ フロー]**、または **[イベント ハンドラー]** タブをクリックします。  
  
4.  タブのデザイン画面で、グループを解除するコンポーネントが含まれているグループを選択します。そのグループを右クリックし、 **[グループ解除]** をクリックします。  
  
5.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [制御フローのタスクまたはコンテナーを追加または削除する](../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [既定の優先順位制約を使用してタスクとコンテナーを連結する](./control-flow/precedence-constraints.md)  
  
