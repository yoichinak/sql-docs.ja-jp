---
title: 株価チャート (レポート ビルダー) | Microsoft Docs
description: レポート ビルダーで、線や三角形などのマーカーを使用し、データ ポイント別に最大 4 つの値を使用して財務データや科学データを表示します。
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: f75ca11e-b7f5-4ac0-ba17-fe6f82742dad
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 79db11ee25dd4ca05a5940e511b39d4280a4a5ed
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91933354"
---
# <a name="stock-charts-report-builder-and-ssrs"></a>株価チャート (レポート ビルダーおよび SSRS)

  株価チャートは、各データ ポイントに最大 4 つの値を使用する、財務データや科学的データ向けに特別にデザインされています。 これらの値は、金融株価データをプロットする際に使用される、高値、安値、始値、終値に対応しています。 この種類のグラフでは、マーカーを使用して始値と終値を表示します。マーカーは、通常、線または三角形です。 次の例では、始値が左側のマーカーで示され、終値が右側のマーカーで示されています。  
  
 ![株価チャート](../../reporting-services/report-design/media/rs-stockchart.gif "株価チャート")  
  
 株価チャートについては、レポート ビルダーのサンプル レポートに例が含まれています。 このサンプル レポートおよびその他のサンプル レポートをダウンロードする方法の詳細については、 [レポート ビルダーおよびレポート デザイナーのサンプル レポート](https://go.microsoft.com/fwlink/?LinkId=198283)に関するページを参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>バリエーション  
  
-   **ローソク足**: ローソク足チャートは、特殊な形式の株価チャートです。このチャートでは、四角形を使用して、始値から終値までの範囲が示されます。 株価チャートと同様、ローソク足チャートでは、各データ ポイントに最大 4 つの値を表示することができます。  
  
## <a name="data-considerations-for-stock-charts"></a>株価チャートのデータに関する注意点  
  
-   年間の株価の動向など、多数の株価データ ポイントを表示する場合、各データ ポイントの始値、終値、高値、安値をそれぞれ区別することは困難です。 この場合は、株価チャートの代わりに折れ線グラフの使用を検討してください。  
  
-   軸ラベルが生成されると、通常、ラベル付けは 0 から始まります。  一般に、株価は、他のデータセットと同じようには変動しません。 このため、データを見やすくする目的で、必要に応じて軸ラベルが 0 から始まらないようにします。 これを行うには、 **[軸のプロパティ]** ダイアログ ボックスまたは [プロパティ] ウィンドウで、 **IncludeZero** を **False** に設定します。 グラフの軸ラベルを作成する方法の詳細については、「[グラフの軸ラベルの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)」を参照してください。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、価格指標、相対力指数、MACD など、株価チャートで使用する多くの計算式が用意されています。  

## <a name="next-steps"></a>次のステップ

[範囲グラフ](../../reporting-services/report-design/range-charts-report-builder-and-ssrs.md)   
[グラフ](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
[グラフの書式設定](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
[[軸のプロパティ] ダイアログ ボックス、[軸のオプション]](/previous-versions/sql/)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)