---
description: スクリプト タスク エディターでのスクリプト タスクの構成
title: スクリプト タスク エディターでのスクリプト タスクの構成 | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], configuring
- Script Task Editor
- SSIS Script task, configuring
ms.assetid: 232de0c9-b24d-4c38-861d-6c1f4a75bdf3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8b4a052ea59e3c72adda887c3084bca278059f0b
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96122925"
---
# <a name="configuring-the-script-task-in-the-script-task-editor"></a>スクリプト タスク エディターでのスクリプト タスクの構成

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  スクリプト タスクにカスタム コードを記述する前に、**[スクリプト タスク エディター]** の 3 つのページで、主要なプロパティを設定します。 スクリプト タスクに対して一意でない追加のタスク プロパティは、[プロパティ] ウィンドウを使用して設定できます。  
  
> [!NOTE]  
>  スクリプトをプリコンパイルするかどうかを指定できた以前のバージョンとは異なり、[!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] 以降ではすべてのスクリプトがプリコンパイルされます。  
  
## <a name="general-page-of-the-script-task-editor"></a>[スクリプト タスク エディター] の [全般] ページ  
 **[スクリプト タスク エディター]** の **[全般]** ページでは、スクリプト タスクに一意の名前および説明を割り当てます。  
  
## <a name="script-page-of-the-script-task-editor"></a>[スクリプト タスク エディター] の [スクリプト] ページ  
 **[スクリプト タスク エディター]** の **[スクリプト]** ページには、スクリプト タスクのカスタム プロパティが表示されます。  
  
### <a name="scriptlanguage-property"></a>ScriptLanguage プロパティ  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) では、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic または [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# のプログラミング言語がサポートされます。 スクリプト タスクにスクリプトを作成した後で、**[ScriptLanguage]** プロパティの値を変更することはできません。  
  
 スクリプト タスクとスクリプト コンポーネントの既定のスクリプト言語を設定するには、**[オプション]** ダイアログ ボックスの **[全般]** ページにある **[ScriptLanguage]** プロパティを使用します。 詳細については、「 [General Page](../../general-page-of-integration-services-designers-options.md)」を参照してください。  
  
### <a name="entrypoint-property"></a>EntryPoint プロパティ  
 **EntryPoint** プロパティは、スクリプト タスク コードのエントリ ポイントとして [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] ランタイムが呼び出す、VSTA プロジェクトの **ScriptMain** クラスのメソッドを指定します。 **ScriptMain** クラスは、スクリプト テンプレートによって生成される既定のクラスです。  
  
 VSTA プロジェクトでメソッドの名前を変更する場合は、 **EntryPoint** プロパティの値を変更する必要があります。  
  
### <a name="readonlyvariables-and-readwritevariables-properties"></a>ReadOnlyVariables プロパティおよび ReadWriteVariables プロパティ  
 既存の変数をコンマ区切りリストとして、これらのプロパティの値に入力すると、スクリプト タスクのコード内で、その変数に読み取り専用アクセスまたは読み取り/書き込みアクセスできるようになります。 どちらの種類の変数にも、**Dts** オブジェクトの <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> プロパティを介して、コード内でアクセスします。 詳細については、「 [スクリプト タスクでの変数の使用](../../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md)」を参照してください。  
  
> [!NOTE]  
>  変数名の大文字と小文字は区別されます。  
  
 変数を選択するには、プロパティ フィールドの横にある参照ボタン **[...]** をクリックします。 詳細については、「[[変数の選択] ページ](../../../integration-services/control-flow/select-variables-page.md)」を参照してください。  
  
### <a name="edit-script-button"></a>[スクリプトの編集] ボタン  
 **[スクリプトの編集]** ボタンをクリックすると VSTA 開発環境が起動し、カスタム スクリプトを記述できるようになります。 詳細については、「[スクリプト タスクのコーディングおよびデバッグ](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)」を参照してください。  
  
## <a name="expressions-page-of-the-script-task-editor"></a>[スクリプト タスク エディター] の [式] ページ  
 **[スクリプト タスク エディター]** の **[式]** ページでは、式を使用して、上に挙げたスクリプト タスクのプロパティ、およびそれ以外の多くのプロパティに値を指定できます。 詳細については、「 [Integration Services (SSIS) 式](../../../integration-services/expressions/integration-services-ssis-expressions.md)に評価されるまでそのワークフローを繰り返します。  
  
## <a name="see-also"></a>参照  
 [スクリプト タスクのコーディングおよびデバッグ](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)  
  
  
