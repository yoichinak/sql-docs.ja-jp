---
description: レッスン 3-1:レッスン 2 のパッケージのコピー
title: 手順 1:レッスン 2 のパッケージのコピー | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 4bd91402-4e37-41de-ab78-8ca5a1948a37
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d5916961ea33dd7534d6b98ff2c158f718ea6db7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88390718"
---
# <a name="lesson-3-1-copy-the-lesson-2-package"></a>レッスン 3-1:レッスン 2 のパッケージのコピー

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



ここでは、レッスン 2 の Lesson 2.dtsx パッケージのコピーを作成します。 レッスン 2 を終了していない場合は、このチュートリアルに含まれる、完了しているレッスン 2 のパッケージをプロジェクトに追加した後、コピーすることもできます。 レッスン 3 の残りの実習では、このパッケージの新しいコピーを使用します。

## <a name="create-the-lesson-3-package"></a>レッスン 3 のパッケージの作成

完了したレッスン 2 をコピーする場合、この手順を使用します。  レッスン 2 のサンプルをコピーするには、次のセクションを参照してください。

1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools がまだ開いていない場合は、 **[開始]**  >  **[すべてのプログラム]**  >  **[Microsoft SQL Server 2017]** の順に選択し、次に **[SQL Server Data Tools]** を選択します。

2.  **[ファイル]** メニューで、 **[開く]**  >  **[プロジェクト/ソリューション]** の順に選択し、 **[SSIS Tutorial]** フォルダーを選択し、 **[開く]** を選択してから、 **[SSIS Tutorial.sln]** をダブルクリックします。

3.  **ソリューション エクスプローラー**で、 **[Lesson 2.dtsx]** を右クリックし、 **[コピー]** を選択します。

4.  **ソリューション エクスプローラー**で、 **[SSIS パッケージ]** を右クリックし、 **[貼り付け]** を選択します。

    コピーしたパッケージの既定の名前は、Lesson 3.dtsx です。

5.  **ソリューション エクスプローラー**で **[Lesson 3.dtsx]** をダブルクリックし、パッケージを開きます。

6.  **[制御フロー]** デザイン画面の背景上で任意の場所を右クリックし、 **[プロパティ]** を選択します。

7.  **[プロパティ]** ウィンドウで、 **[Name]** プロパティを「**Lesson 3**」に変更します。

8.  **ID** プロパティのボックスを選択し、ドロップダウン矢印を選択し、 **[\<Generate New ID>]** を選択します。

## <a name="add-the-completed-lesson-2-package"></a>完了したレッスン 2 のパッケージの追加

1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools を開き、SSIS Tutorial プロジェクトを開きます。

2.  **ソリューション エクスプローラー**で **[SSIS パッケージ]** を右クリックし、 **[既存のパッケージを追加]** を選択します。

3.  **[既存のパッケージのコピーを追加]** ダイアログの **[パッケージの場所]** で、 **[ファイル システム]** を選択します。

4.  参照ボタン **[...]** を選択し、コンピューター上の **Lesson 2.dtsx** に移動して、 **[開く]** を選択します。

5.  前のセクションの手順 3 から 8 の説明に従って、レッスン 3 パッケージをコピーして貼り付けます。  
  
## <a name="go-to-next-task"></a>次のタスクに進む
[手順 2:ログ記録の追加および構成](../integration-services/lesson-3-2-adding-and-configuring-logging.md)  
  
