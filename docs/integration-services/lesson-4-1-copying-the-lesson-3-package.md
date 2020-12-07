---
description: 'レッスン 4-1: レッスン 3 のパッケージをコピーする'
title: 手順 1:レッスン 3 のパッケージのコピー | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 0d053786-5203-43f3-a613-27a8dd2bc44a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7476bf5318efcdc7c188dda74a1231d8d4aed094
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449660"
---
# <a name="lesson-4-1-copy-the-lesson-3-package"></a>レッスン 4-1: レッスン 3 のパッケージをコピーする

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



ここでは、レッスン 3 で作成した Lesson 3.dtsx パッケージのコピーを作成します。 レッスン 3 を終了していない場合は、チュートリアルに含まれている、レッスン 3 を完了した状態のパッケージをプロジェクトに追加し、作業用のコピーを作成することもできます。 レッスン 4 の実習では、このパッケージの新しいコピーを使用します。  
  
## <a name="create-the-lesson-4-package"></a>レッスン 4 のパッケージを作成する  
  
完了したレッスン 3 をコピーする場合は、この手順を使用します。  レッスン 3 のサンプルをコピーするには、次のセクションを参照してください。

1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools がまだ開いていない場合は、 **[開始]**  >  **[すべてのプログラム]**  >  **[Microsoft SQL Server 2017]** の順に選択し、次に **[SQL Server Data Tools]** を選択します。

2.  **[ファイル]** メニューで、 **[開く]**  >  **[プロジェクト/ソリューション]** の順に選択し、 **[SSIS Tutorial]** フォルダーを選択し、 **[開く]** を選択してから、 **[SSIS Tutorial.sln]** をダブルクリックします。

3.  **ソリューション エクスプローラー**で、**Lesson 3.dtsx** を右クリックし、 **[コピー]** を選択します。

4.  **ソリューション エクスプローラー**で、 **[SSIS パッケージ]** を右クリックし、 **[貼り付け]** を選択します。

    コピーしたパッケージの既定の名前は、**Lesson 4.dtsx** です。

5.  **ソリューション エクスプローラー**で **Lesson 4.dtsx** をダブルクリックし、パッケージを開きます。

6.  **[制御フロー]** デザイン画面の背景上で任意の場所を右クリックし、 **[プロパティ]** を選択します。

7.  **[プロパティ]** ウィンドウで、 **[Name]** プロパティを「**Lesson 4**」に変更します。

8.  **ID** プロパティのボックスを選択し、ドロップダウン矢印を選択し、 **[\<Generate New ID>]** を選択します。

## <a name="add-the-completed-lesson-3-package"></a>レッスン 3 を完了した状態のパッケージを追加する

1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools を開き、SSIS Tutorial プロジェクトを開きます。

2.  **ソリューション エクスプローラー**で **[SSIS パッケージ]** を右クリックし、 **[既存のパッケージを追加]** を選択します。

3.  **[既存のパッケージのコピーを追加]** ダイアログ ボックスの **[パッケージの場所]** で、 **[ファイル システム]** をクリックします。

4.  参照ボタン **[...]** を選択し、ご利用のコンピューター上の **Lesson 3.dtsx** に移動して、 **[開く]** を選択します。

5.  前のセクションの手順 3 から 8 の説明に従って、レッスン 3 パッケージをコピーして貼り付けます。

  
## <a name="go-to-next-task"></a>次のタスクに進む  
[手順 2:破損したファイルを作成する](../integration-services/lesson-4-2-creating-a-corrupted-file.md)  
  
