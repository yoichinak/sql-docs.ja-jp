---
title: SQL Server Integration Services の Azure への移行に関する概要 | Microsoft Docs
description: この記事では、SQL Server Integration Services を Azure に移行するためのプロセスとツールを紹介しています。
ms.date: 04/10/2020
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6fe5435882a55b8e8fcc56dff5d65f957fc6f8c4
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192512"
---
# <a name="migrate-on-premises-ssis-workloads-to-ssis-in-adf"></a>ADF でオンプレミスの SSIS ワークロードを SSIS に移行する

この記事では、SQL Server Integration Services (SSIS) ワークロードを ADF の SSIS に移行するのに役立つプロセスとツールを一覧表示します。

[移行の概要](/azure/data-factory/scenario-ssis-migration-overview)に関するページでは、オンプレミスの SSIS から ADF の SSIS への ETL ワークロードの移行プロセス全体が紹介されています。

移行プロセスは、2 つのフェーズで構成されます。[評価](/azure/data-factory/scenario-ssis-migration-overview#assessment)と[移行](/azure/data-factory/scenario-ssis-migration-overview#migration)です。

## <a name="assessment"></a>評価

Data Migration Assistant (DMA) は、この目的のために自由にダウンロード可能なツールであり、ローカルにインストールして実行できます。 種類が Integration Services の DMA 評価プロジェクトを作成して、SSIS パッケージを一括して評価し、互換性の問題を特定できます。

[Database Migration Assistant](../../dma/dma-overview.md) を取得し、[パッケージの評価を実行します](../../dma/dma-assess-ssis.md)。

## <a name="migration"></a>移行

ソース SSIS パッケージのストレージの種類とデータベース ワークロードの移行先によって、SSIS パッケージと SSIS パッケージ実行をスケジュールする SQL Server エージェント ジョブを移行する手順は異なる場合があります。 詳細については、 [こちらのページ](/azure/data-factory/scenario-ssis-migration-overview#migration)をご覧ください。

## <a name="next-steps"></a>次のステップ

- [SSIS パッケージを Azure SQL Managed Instance に移行する](/azure/dms/how-to-migrate-ssis-packages-managed-instance)
- [SQL Server Management Studio (SSMS) を使用して SSIS ジョブを Azure Data Factory (ADF) に移行する](/azure/data-factory/how-to-migrate-ssis-job-ssms)。