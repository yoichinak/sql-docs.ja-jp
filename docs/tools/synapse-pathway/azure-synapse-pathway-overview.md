---
title: Azure Synapse Pathway プレビューの概要
description: Azure Synapse Pathway は、データ ウェアハウスを Azure Synapse Analytics に移行するためのツールです。
author: anshul82-ms
ms.author: anrampal
ms.topic: overview
ms.date: 03/02/2021
ms.prod: sql
ms.technology: tools-other
monikerRange: =azure-sqldw-latest
ms.custom: template-overview
ms.openlocfilehash: 5e3844f6e63fafca5137a646ff4c02edbc7105b8
ms.sourcegitcommit: ca81fc9e45fccb26934580f6d299feb0b8ec44b7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102185925"
---
# <a name="azure-synapse-pathway-preview-overview"></a>Azure Synapse Pathway プレビューの概要
[!INCLUDE [Azure Synapse Analytics](../../includes/applies-to-version/asa.md)]

お客様がデータ ウェアハウス システムの最新化を検討している間、直面する重要なブロックのいずれかで SQL コードが翻訳されます。 既存のコードは現在のシステム用に記述および最適化されていますが、移行先の新しいシステム用に最適化する必要があります。

世界中の組織は、総保有コスト (TCO) とイノベーションの利点の両方を享受するために、分析プラットフォームを最新化する必要があります。 しかし、お客様はそれぞれのデータ ウェアハウスのために数千の作業時間を費やし、数百万ドルを投じ、数万行のコードを作成しました。
 
この重要な SQL コードを翻訳するには、お客様は既存の SQL コードを手動で書き直すか、またはコードを書き直したり変換したりするために外部の業務に大量の予算を投ずる必要があります。

> [!IMPORTANT]
> 現在、Azure Synapse Pathway はパブリック プレビュー段階にあります。
> このプレビュー バージョンはサービス レベル アグリーメントなしで提供されています。運用環境のワークロードに使用することはお勧めできません。 特定の機能はサポート対象ではなく、機能が制限されることがあります。
 
> 詳しくは、[Microsoft Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)に関するページをご覧ください。 

**Azure Synapse Pathway** は、既存のデータ ウェアハウスのコード翻訳を自動化することで、最新のデータ ウェアハウス プラットフォームにアップグレードするのに役立ちます。 これは無料の直感的で使いやすいツールであり、Azure Synapse Analytics へのより迅速な移行を可能にするコード翻訳を自動化するものです。

 ![Azure Synapse Pathway の概要。](./media/azure-synapse-pathway-overview/pathway-overview.png) 

Synapse Pathway により、データ定義言語 (DDL) およびデータ操作言語 (DML) ステートメントが、Azure Synapse SQL と互換性のある T-SQL 準拠言語に翻訳されます。

## <a name="behind-the-scenes"></a>バックグラウンド処理

Azure Synapse Pathway についてさらに学習する場合は、Azure Synapse Pathway のしくみについて、段階的なプロセスを示す[バックグラウンド](synapse-pathway-behind-the-scenes.md)に関するページを参照してください。

## <a name="get-azure-synapse-pathway"></a>Azure Synapse Pathway を取得する

Synapse Pathway をインストールする場合は、[Azure Synapse Pathway のダウンロード](synapse-pathway-download.md)に関するページで、前提条件と最新バージョンをダウンロードするためのリンクを確認してください。

## <a name="supported-sources"></a>サポートされているソース

Azure Synapse Pathway では、次のソースのデータベース、スキーマ、テーブルのコード変換がサポートされています。
- **IBM Netezza**
- **Microsoft SQL Server**
- **Snowflake**

## <a name="frequently-asked-questions"></a>よく寄せられる質問

Azure Synapse Pathway の追加情報については、[FAQ ページ](pathway-faq.md)を参照してください

## <a name="next-steps"></a>次のステップ

- [Azure Synapse Pathway で初めての翻訳を実行する](synapse-pathway-assessment.md)
- お知らせブログ - [Azure Synapse Pathway の発表: データ ウェアハウスの移行を加速させる - Microsoft Tech Community](https://techcommunity.microsoft.com/t5/azure-synapse-analytics/announcing-azure-synapse-pathway-turbocharge-your-data-warehouse/ba-p/2176630)