---
description: スクリプト タスクによるパッケージの拡張
title: スクリプト タスクによるパッケージの拡張 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- scripts [Integration Services]
- SSIS Script task
- tasks [Integration Services], scripts
- Script task [Integration Services], about Script task
- scripts [Integration Services], about Script task with packages
- SSIS Script task, about Script task
ms.assetid: 911e6d26-a6fd-4fc3-a111-bf5f048e9bff
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c70136ad09aaa3cb24c04c2828e8335f96aef467
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96122848"
---
# <a name="extending-the-package-with-the-script-task"></a>スクリプト タスクによるパッケージの拡張

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  スクリプト タスクを使用すると、カスタム コードを [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic または [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# で記述し、パッケージの実行時にコンパイル、実行することにより、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] パッケージのランタイム機能を拡張できます。 スクリプト タスクは、[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] に含まれているタスクが十分に要件を満たしていない場合に、カスタム ランタイム タスクの開発を単純化します。 必要なすべてのインフラストラクチャ コードがスクリプト タスクによって自動生成されるため、カスタム処理を実行するために必要なコードの記述に集中できます。  
  
 スクリプト タスクは、スクリプト環境で公開される <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel> クラスのインスタンスであるグローバル オブジェクト **Dts** を介して、内部のパッケージとやり取りします。 スクリプト タスク内でコードを記述して、[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 変数に格納された値を変更できます。その後、更新した変数の値をパッケージで使用して、ワークフローのパスを決定できます。 また、カスタム アセンブリだけでなく、[!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 名前空間および [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] クラス ライブラリを使用して、スクリプト タスクに独自の機能を実装することもできます。  
  
 スクリプト タスクおよびそれによって生成されるインフラストラクチャ コードを活用すれば、カスタム タスクを開発するための手順を大幅に簡略化できます。 スクリプト タスクの動作のしくみを理解するため、「[カスタム タスクの開発](../../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)」のセクションを参照して、カスタム タスクの開発手順を理解しておくと役立つ場合があります。  
  
 作成したタスクを複数のパッケージで再利用する予定がある場合は、スクリプト タスクではなく、カスタム タスクを開発することを検討してください。 詳細については、「[スクリプティング ソリューションとカスタム オブジェクトとの比較](../../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 次のトピックでは、スクリプト タスクの詳細について説明します。  
  
 [スクリプト タスク エディターでのスクリプト タスクの構成](../../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)  
 **[スクリプト タスク エディター]** で構成したプロパティがスクリプト タスク コードの機能やパフォーマンスに及ぼす影響について説明します。  
  
 [スクリプト タスクのコーディングおよびデバッグ](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)  
 スクリプト タスクに含まれるスクリプトを [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) を使用して開発する方法について説明します。  
  
 [スクリプト タスクでの変数の使用](../../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md)  
 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> プロパティを介して変数を使用する方法について説明します。  
  
 [スクリプト タスクでのデータ ソースへの接続](../../../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)  
 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> プロパティを介して接続を使用する方法について説明します。  
  
 [スクリプト タスクでのイベントの発生](../../../integration-services/extending-packages-scripting/task/raising-events-in-the-script-task.md)  
 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> プロパティを介してイベントを発生させる方法について説明します。  
  
 [スクリプト タスクでのログ記録](../../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md)  
 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> メソッドを介して情報をログに記録する方法について説明します。  
  
 [スクリプト タスクから結果を返す](../../../integration-services/extending-packages-scripting/task/returning-results-from-the-script-task.md)  
 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> および <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> プロパティを介して結果を返す方法について説明します。  
  
 [スクリプト タスクの例](../../../integration-services/extending-packages-scripting-task-examples/script-task-examples.md)  
 スクリプト タスクの使用方法を示す簡単な例をいくつか提供します。  
  
## <a name="see-also"></a>参照  
 [スクリプト タスク](../../../integration-services/control-flow/script-task.md)   
 [スクリプト タスクとスクリプト コンポーネントの比較](../../../integration-services/extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
  
  
