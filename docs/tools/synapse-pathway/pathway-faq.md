---
title: Azure Synapse Pathway プレビューに関する FAQ
description: Azure Synapse Pathway についてよく寄せられる質問
author: anshul82-ms
ms.author: anrampal
ms.topic: overview
ms.date: 03/02/2021
ms.prod: sql
ms.technology: Azure Synapse Pathway
monikerRange: =azure-sqldw-latest
ms.custom: template-overview
ms.openlocfilehash: 345346d2161800810ba3d07667b831107f70b215
ms.sourcegitcommit: 9413ddd8071da8861715c721b923e52669a921d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "101873075"
---
# <a name="azure-synapse-pathway-preview"></a>Azure Synapse Pathway プレビュー
[!INCLUDE [Azure Synapse Analytics](../../includes/applies-to-version/asa.md)]

このガイドでは、Azure Synapse Pathway Preview についてよく寄せられる質問を紹介します。

## <a name="general"></a>全般

### <a name="q-what-is-azure-synapse-pathway"></a>Q. Azure Synapse Pathway とは何ですか?

A. Azure Synapse Pathway はコード翻訳ツールです。これは、T-SQL ベースの Azure Synapse SQL に準拠するために既存のデータ ウェアハウスのコード変換を自動化することで、最新のデータ ウェアハウス プラットフォームにアップグレードする際に役立ちます。

### <a name="q-how-can-i-download-azure-synapse-pathway"></a>Q. Azure Synapse Pathway をダウンロードするにはどうすればよいですか?

A. Synapse Pathway は [Microsoft ダウンロード センター](https://aka.ms/synapse-pathway-download)からダウンロードできます。

### <a name="q-how-much-does-azure-synapse-pathway-cost"></a>Q. Azure Synapse Pathway のコストはどれくらいですか?

A. Synapse Pathway のダウンロードとこれを使用するコード翻訳の実行に関するコストはありません。

### <a name="q-what-sourcetarget-pairs-does-azure-synapse-pathway-currently-support"></a>Q. Azure Synapse Pathway では現在、どのようなソースとターゲットのペアがサポートされていますか?

A. このプレビュー バージョンの Synapse Pathway には、次のデータ ウェアハウスがソースとして含まれています。
- Microsoft SQL Server
- Snowflake
- Netezza

### <a name="q-what-is-included-as-part-of-the-code-conversion"></a>Q. コード変換には何が含まれていますか?

A. Synapse Pathway では、テーブル、スキーマ、ビュー、およびストアド プロシージャのコード翻訳がサポートされています。

### <a name="q-can-it-also-scan-my-environment-and-provide-an-assessment-report-of-all-the-objects-that-need-to-be-convertedtranslated"></a>Q. 環境をスキャンし、変換または翻訳する必要があるすべてのオブジェクトの評価レポートを提供することもできますか?

A. このプレビュー バージョンの Synapse Pathway では、変換する必要がある DDL または DML スクリプトへのリンクはユーザーが提供する必要があります。 翻訳する必要があるオブジェクトを特定するために、Synapse Pathway によって現在の環境がスキャンされることはありません。

### <a name="q-what-information-does-azure-synapse-pathway-capture-about-my-current-data-warehouse-instance"></a>Q. 現在のデータ ウェアハウス インスタンスについて、Azure Synapse Pathway によってどのような情報が取り込まれますか?

A. ローカル環境で Synapse Pathway を実行できるため、Microsoft ダウンロード センターから MSI をダウンロードするときに必要な名前と組織以外に取り込まれるデータはありません。

### <a name="q-where-can-i-raise-issues-encountered-in-azure-synapse-pathway"></a>Q. Azure Synapse Pathway で発生した問題はどこで報告すればよいですか?

A. 現在、Azure Synapse Pathway は **プレビュー** 段階にあります。   Synapse Pathway のサポートは、Microsoft サポート チャネルを通じてご利用いただけます。 チケットは、Azure portal または Standard (通常はオンプレミスのサポート) ポータルで提出することができます。

> [!NOTE] 他の Azure サービスと同様に、すべてのプレビュー サービスは、SLA が適用されないだけで、サポートの対象にはなります。

<!-- ### Troubleshooting and optimization

#### Q. Why do I see slow performance while running the code conversion?

#### Q. Translation of errors or unexpected results? -->

## <a name="next-steps"></a>次のステップ

[Azure Synapse Pathway をダウンロードする](synapse-pathway-download.md)