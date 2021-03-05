---
title: Azure Synapse Pathway プレビューのレポート生成
description: Azure Synapse Pathway を使用すると、翻訳されたスクリプトに関する包括的なレポートが得られます。
author: anshul82-ms
ms.author: anrampal
ms.topic: tutorial
ms.prod: sql
ms.technology: tools-other
ms.date: 03/02/2021
monikerRange: =azure-sqldw-latest
ms.custom: template-tutorial
ms.openlocfilehash: 26701c33f713a1b82e3bab604a03e7dca054a36b
ms.sourcegitcommit: ca81fc9e45fccb26934580f6d299feb0b8ec44b7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102186362"
---
# <a name="report-generation-for-azure-synapse-pathway-preview"></a>Azure Synapse Pathway プレビューのレポート生成
[!INCLUDE [Azure Synapse Analytics](../../includes/applies-to-version/asa.md)]

Azure Synapse Pathway を使用すると、正常に翻訳されたスクリプトの数について包括的なレポートが得られます。 また、このレポートには、変換されなかったステートメントに関するエラーおよび警告の数も表示されます。

## <a name="generate-report"></a>レポートの生成

**[翻訳]** を選択すると、次のようなレポートが表示されます。

![Azure Synapse Pathway のレポート。](./media/report-generaration/report-overview.png)

## <a name="report-summary"></a>レポートの概要

[変換完了] に、正常に翻訳されたスクリプトの割合が表示されます。

![Azure Synapse Pathway。](./media/report-generaration/conversion-success.png)

[ステートメントの分布] セクションには、作成されたスキーマ、テーブル、データベースの数など、翻訳された DDL および DML ステートメントの数について詳細が表示されます。

![Azure Synapse のレポート 1。](./media/report-generaration/statement-distribution.png)

移行のコスト削減は、翻訳されたオブジェクトの数と複雑さ (シンプル、高、または中程度) に基づいて計算されます。 Synapse Pathway では、オブジェクトの翻訳ごとに 30 分の手動作業が発生することを前提としています。

![Azure Synapse のレポート 2。](./media/report-generaration/migration-savings.png)

## <a name="next-steps"></a>次のステップ

[Azure Synapse Pathway をダウンロードする](synapse-pathway-download.md)