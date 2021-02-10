---
title: Data Migration Assistant を使用した評価の保存と読み込み
description: Data Migration Assistant を使用して評価を保存し、読み込む方法について説明します。
ms.date: 01/10/2020
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: 9f427c7d706e3665cc5cbca092bfbc99a333a1ea
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100030630"
---
# <a name="save-and-load-assessments-with-data-migration-assistant"></a>Data Migration Assistant を使用した評価の保存と読み込み

次の手順では、Data Migration Assistant v1.0 以降を使用してデータベースの評価をファイルに保存し、ファイルから評価を読み込む方法について説明します。

> [!NOTE]
> ユーザーは、最新バージョンの DMA を使用して保存された評価を読み込むだけでなく、この機能を利用して、以前のバージョンの Data Migration Assistant の json ファイルとしてエクスポートされた評価を読み込んで、バージョン5.0 以降で結果を表示することもできます。

## <a name="saving-an-assessment-to-a-file"></a>評価をファイルに保存する

1. Data Migration Assistant を使用して評価を実行した後、[ **評価の保存**] を選択します。

   ![[評価の保存] ダイアログボックスを開く](../dma/media/dma-save-load-assessments/dma-open-save-dialog.png)

   標準の **保存...** ダイアログボックスが表示されます。

   > [!NOTE]
   > Data Migration Assistant で評価を実行する方法の詳細については、 [Data Migration Assistant を使用した SQL Server 移行の評価の実行](../dma/dma-assesssqlonprem.md)に関する記事を参照してください。

2. ファイルの名前を指定し、[ **保存**] を選択します。

   ![評価ファイルに名前を付けて保存する](../dma/media/dma-save-load-assessments/dma-name-save-assessment.png)

## <a name="loading-an-assessment-saved-to-a-file"></a>ファイルに保存された評価を読み込んでいます

1. 以前にファイルに保存した評価を読み込むには Data Migration Assistant を開始し、[ **すべての評価** ] タブで [ **負荷評価**] を選択します。

   ![[負荷評価] ダイアログボックスを開く](../dma/media/dma-save-load-assessments/dma-open-load-dialog.png)

2. 読み込む保存済みの評価ファイルに移動し、ファイルを選択して、[ **開く**] を選択します。

   ![評価ファイルを開く](../dma/media/dma-save-load-assessments/dma-open-assessment.png)

   [ **すべての評価** ] タブに、読み込まれた評価のエントリが表示されます。

   ![評価エントリの表示](../dma/media/dma-save-load-assessments/dma-display-assessment-entry.png)

3. [評価] エントリを選択し、[ **評価を開く**] を選択します。

   ![評価の詳細を開く](../dma/media/dma-save-load-assessments/dma-open-assessment-detail.png)

   Data Migration Assistant に、以前に実行した評価の詳細が表示されるようになりました。

   ![評価の詳細の表示](../dma/media/dma-save-load-assessments/dma-display-assessment-detail.png)
