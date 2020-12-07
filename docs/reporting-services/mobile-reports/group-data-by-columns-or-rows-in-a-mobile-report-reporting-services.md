---
title: モバイル レポートのデータを行または列によってグループ化する | Reporting Services | Microsoft Docs
description: Mobile Report Publisher では、多数の種類のグラフのデータを列または行によって整理できます。 この記事では、列または行ごとに構造化されたデータを示します。
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: b9ebd36c-a337-47ae-83e5-6c2f2144eb52
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d775b0346ce2838abeec4bebce55762afd3b0adc
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907330"
---
# <a name="group-data-by-columns-or-rows-in-a-mobile-report--reporting-services"></a>モバイル レポートのデータを行または列によってグループ化する |Reporting Services
[!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)]は、多数の種類のグラフのデータを列または行によって整理できます。 次の手順に従ってください。

時間グラフ、合計グラフ、円グラフ、およびじょうごグラフでは、行または列によってデータを整理できます。 
* テーブルに比較対象となるデータ列が複数ある場合は、列による整理が便利です。 
* テーブルの 1 つの列に複数のカテゴリの名前が含まれている場合は、行による整理のほうが便利です。 

次の手順では、 [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] でシミュレート されたデータを含む比較合計テーブルを使用して、データの行または列によるグラフの構成の違いを示します。  

1. **比較合計グラフ** を **[レイアウト]** タブからデザイン画面にドラッグして少し大きくします。

2. **[データ]** タブを選択します。SimulatedTable テーブルには、一連の列 ( **Metric1** から **Metric5** と **Comparison1** から **Comparison5** ) があります。 

   ![モバイル レポートのデータ グループ列のスクリーンショット。](../../reporting-services/mobile-reports/media/mobile-report-data-group-column.png)

3. **[データ プロパティ]** ペインに表示される **[主要な系列]** は **[SimulatedTable]** です。 **[主要な系列]** の横にあるボックスの矢印を選択すると、 **Metric1** ～ **Metric5** が選択されます。

   ![[主要な系列] の横にあるオプションのスクリーンショット。](../../reporting-services/mobile-reports/media/mobile-report-properties-columns.png)

   同様に、 **[比較対象系列]**  -- **Comparison1** ～ **Comparison5** が選択されます。
   
4. **[Preview]\(プレビュー\)** を選択します。

   ![[Comparisons Totals Chart]\(比較合計グラフ\) のプレビューのスクリーンショット。](../../reporting-services/mobile-reports/media/mobile-report-chart-by-columns.png)

   グラフの各バーは、テーブル内の 1 つの列を表します。 太いバーは Metrics 列を、細いバーは Comparison 列を表します。

5. プレビュー モードを終了するには、左上隅にある戻る矢印を選択します。

6. **[レイアウト]** タブの **[ビジュアルのプロパティ]** ペインで、 **[データ構造]** を **[By columns (列による)]** から **[By rows (行による)]** に変更します。  

7. **[データ]** タブを選択します。SimulatedTable テーブルに **Category** 列が追加され、 **Metric** 列と **Comparison** 列が Category A ～ E 別に表示されます。 

   ![モバイル レポートのデータ グループ行のスクリーンショット。](../../reporting-services/mobile-reports/media/mobile-report-data-group-rows.png)

8.  **[データ プロパティ]** ペインには、SimulatedTable の Category 列を示す [カテゴリ列] ボックスが表示されます。 [主要な系列] で、値を使用する列を選択できます。 既定により、 [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] は、主要な系列として Metric1 ～ Metric5 を、比較対象系列として Comparison1 ～ Comparison5 を選択しています。 

    ![[比較対象系列] の横にあるオプションのスクリーンショット。](../../reporting-services/mobile-reports/media/mobile-report-properties-rows.png)

9. **[Preview]\(プレビュー\)** を選択します。

   ![更新された [Comparisons Totals Chart]\(比較合計グラフ\) のプレビューのスクリーンショット。](../../reporting-services/mobile-reports/media/mobile-report-chart-by-rows.png)

   今回のグラフの各バーは、Category 列の各カテゴリの値を表しています。

### <a name="see-also"></a>関連項目
* [Reporting Services モバイル レポートの視覚エフェクト](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
