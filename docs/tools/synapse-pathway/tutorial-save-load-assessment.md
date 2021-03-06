---
title: Azure Synapse Pathway プレビューを使用した保存および読み込み
description: Azure Synapse Pathway プレビューを使用してデータ ウェアハウスの評価を保存して読み込む
author: anshul82-ms
ms.author: anrampal
ms.prod: sql
ms.technology: tools-other
ms.topic: tutorial
ms.date: 03/02/2021
monikerRange: =azure-sqldw-latest
ms.openlocfilehash: fbaa518e2f2a5485f85fc7812291beb88896ac6e
ms.sourcegitcommit: ca81fc9e45fccb26934580f6d299feb0b8ec44b7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102186267"
---
# <a name="save-and-load-assessments-with-azure-synapse-pathway-preview"></a>Azure Synapse Pathway プレビューを使用した保存および読み込み
[!INCLUDE [Azure Synapse Analytics](../../includes/applies-to-version/asa.md)]

次の詳細な手順では、Azure Synapse Pathway を使用してデータ ウェアハウスの評価をファイルに保存し、そこからアップロードする方法について説明します。

このチュートリアルでは、以下の内容を学習します。

> [!div class="checklist"]
> * 評価をファイルに保存する
> * ファイルから評価を読み込む

## <a name="prerequisites"></a>前提条件

このチュートリアルを完了するには、[Azure Synapse Pathway](synapse-pathway-download.md) がインストールされていることを確認してください。このツールの詳細については、[Azure Synapse Pathway の概要](azure-synapse-pathway-overview.md)に関するページを参照してください。

## <a name="saving-an-assessment-to-a-file"></a>ファイルに評価を保存する

1. 翻訳を実行すると、コードの翻訳を要約したレポートが表示されます。![Azure Synapse Pathway の評価レポートの概要。](./media/tutorial-save-load-assessment/report-overview.png)
1. **[評価の保存]** ボタンを選択し、ファイルの名前を指定して、 **[保存]** を選択します。
![Azure Synapse Pathway の評価。](./media/tutorial-save-load-assessment/save-assessment.png)

1. 指定した宛先に .asmprj ファイルが作成されます。

## <a name="loading-an-assessment-from-a-file"></a>ファイルから評価を読み込む

1. 同じ評価を開くには、 **[評価の読み込み]** を選択し、.asmprj ファイルの名前を指定します。![Azure Synapse Pathway の評価の場所への移動。](./media/tutorial-save-load-assessment/browse-location.png)

1. 選択した評価に基づいて、[ソース]、[入力]、[出力] の各フォルダーが設定されます。
![翻訳の種類、入力ディレクトリ、出力ディレクトリを示す Azure Synapse Pathway の評価構成。](./media/tutorial-save-load-assessment/load-assessment.png)
1. **[翻訳]** を選択して、コードの翻訳を再実行します

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [レポートの生成](report-generation.md)
