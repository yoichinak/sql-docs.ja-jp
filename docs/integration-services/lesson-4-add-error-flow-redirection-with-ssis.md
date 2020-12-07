---
description: 'レッスン 4: SSIS でエラー フロー リダイレクションを追加する'
title: 'レッスン 4: SSIS でエラー フロー リダイレクションを追加する | Microsoft Docs'
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 0c8dbda2-75e3-4278-9b4e-dcd220c92522
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d7ef0a6862e334221fd497a5adc44ffd0ab7990d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466586"
---
# <a name="lesson-4-add-error-flow-redirection-with-ssis"></a>レッスン 4:SSIS でエラー フロー リダイレクションを追加する

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、変換プロセスで発生するエラーを処理する目的で、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] で変換できないデータの処理方法をコンポーネントごとに、および列ごとに決定できます。 特定の列の失敗を無視するか、失敗した行全体をリダイレクトするか、コンポーネント単位で失敗を判定するように選択できます。 既定の構成では、エラーの発生時に [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のコンポーネントが変換に失敗したものと見なされます。 コンポーネントが失敗と見なされると、パッケージが失敗と見なされ、処理が停止します。  
  
失敗によりパッケージ実行を停止させるのではなく、潜在的な処理エラーを設定しておき、それが発生したときに処理することができます。 1 つの選択肢は、失敗を全部無視し、パッケージの実行を常に成功させることです。 失敗した行を別の処理パスにリダイレクトすることもできます。そのパスでデータやエラーを保存し、調査し、再処理できます。  
  
このレッスンでは、「[レッスン 3: SSIS でのログ記録の追加](../integration-services/lesson-3-add-logging-with-ssis.md)」で作成したパッケージのコピーを作成します。 この新しいパッケージを使用し、壊れたサンプル データ ファイルを作成します。 この破損ファイルは、パッケージを実行するときに変換エラーを発生させます。  
  
エラー データを処理するには、失敗した行をエラー ファイルに書き込むフラット ファイル変換先を追加し、構成します。 
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] でエラー データをファイルに書き込む前に、エラーの説明を取得するスクリプト コンポーネントを追加します。 その後 Lookup Currency Key 変換を再構成して、処理できなかったデータをスクリプト変換にリダイレクトするようにします。  
  
## <a name="prerequisites"></a>前提条件

> [!NOTE]
> まだ行っていない場合は、[レッスン 1 の前提条件](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)を参照してください。
 
## <a name="lesson-task"></a>レッスンの作業
このレッスンの内容は次のとおりです。  
  
-   [ステップ 1:レッスン 3 のパッケージをコピーする](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
-   [手順 2:破損したファイルを作成する](../integration-services/lesson-4-2-creating-a-corrupted-file.md)  
  
-   [ステップ 3:エラー フロー リダイレクションを追加する](../integration-services/lesson-4-3-adding-error-flow-redirection.md)  
  
-   [手順 4:フラット ファイル変換先を追加する](../integration-services/lesson-4-4-adding-a-flat-file-destination.md)  
  
-   [手順 5:レッスン 4 で作成したチュートリアル パッケージのテスト](../integration-services/lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>レッスンの開始  
[ステップ 1:レッスン 3 のパッケージをコピーする](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
  
  
