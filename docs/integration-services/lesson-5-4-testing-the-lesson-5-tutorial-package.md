---
description: レッスン 5-4:レッスン 5 のパッケージをテストする
title: 手順 4:レッスン 5 のパッケージをテストする | Microsoft Docs
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5215b77d-c2ec-4b25-a3de-ca49ea197d74
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 57bad9d0d13f85ae52858005e3fb6acc6f9532f0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500820"
---
# <a name="lesson-5-4-test-the-lesson-5-package"></a>レッスン 5-4:レッスン 5 のパッケージをテストする

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



実行時、パッケージは、パッケージの作成時に指定したディレクトリ名からではなく、構成変数から **Directory** プロパティの値を取得します。 変数の値は、**SSISTutorial.dtsConfig** XML ファイルから取得されます。  
  
パッケージの実行時に、**Directory** プロパティが新しい値に更新されているかどうかを確認するには、パッケージを実行します。 新しいディレクトリにはサンプル データ ファイルが 3 つだけ入っているため、データ フローは 3 回だけ実行されます。  
  
## <a name="checking-the-package-layout"></a>パッケージ レイアウトの確認  
パッケージをテストする前に、レッスン 5 の制御フローとデータ フローが次の図にあるオブジェクトと同様であることを確認します。  
  
**制御フロー**  
  
![パッケージ内の制御フロー](../integration-services/media/task4lesson2control.gif "パッケージ内の制御フロー")  
  
**データ フロー**  
  
![パッケージ内のデータ フロー](../integration-services/media/task9lesson1data.gif "パッケージ内のデータ フロー")  
  
## <a name="test-the-lesson-5-package"></a>レッスン 5 のパッケージをテストする  
  
1.  **[デバッグ]** メニューの **[デバッグの開始]** をクリックします。  
  
2.  パッケージの実行が完了したら、**[デバッグ]** メニューの **[デバッグの停止]** を選択します。  
  
## <a name="next-lesson"></a>次のレッスン  
[レッスン 6:SSIS でプロジェクト配置モデルを持つパラメーターを使用する](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
  
  
  
