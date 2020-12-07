---
title: グラフの凡例アイテムを非表示にする (レポート ビルダー) | Microsoft Docs
description: レポート ビルダーで、重要なデータを表示するため、凡例に表示するアイテムを選択する方法について説明します。
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 92256240-0cd5-4be4-8904-d1e3b93cb6b3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cf51a3b08b8296ddfd2e7bf470d36d575485888b
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91935307"
---
# <a name="chart-legend---hide-items-report-builder"></a>グラフの凡例 - 項目の非表示 (レポート ビルダー)
既定では、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のページ分割されたレポートで図形グラフ以外のグラフに追加した系列は、凡例の項目として使用されます。 円グラフ、ドーナツ グラフ、じょうごグラフ、およびピラミッド グラフでは、グラフに系列を追加すると、凡例に個々のデータ ポイントが追加されます。  
  
 凡例の任意の項目を非表示にすることができます。 凡例の項目を非表示にした場合も、グラフには表示されます。 これは、グラフに追加した系列の詳細な情報を表示したくないときに便利です。 たとえば、移動平均のような計算系列をグラフに追加した場合、凡例のこのエントリを非表示にし、元の系列の詳細な情報のみを表示できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-hide-an-item-from-display-in-the-legend"></a>凡例の項目を非表示にするには  
  
1.  非表示にする系列を右クリックし、 **[系列のプロパティ]** をクリックします。  
  
2.  **[凡例]** をクリックします。 **[凡例内の次の系列を非表示にする]** オプションを選択します。  
  
    > [!NOTE]  
    >  あるグループの系列を非表示にし、他のグループの系列を表示することはできません。 **[系列グループ]** 領域にフィールドを追加している場合、このグループに属するすべての系列は非表示になります。  
  
## <a name="see-also"></a>参照  
 [グラフの凡例の書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)   
 [グラフでのデータ ポイントの書式設定 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [凡例アイテムのテキストの変更 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/chart-legend-change-item-text-report-builder.md)   
 [グラフへの移動平均の追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-a-moving-average-to-a-chart-report-builder-and-ssrs.md)   
 [[全般] ([凡例のプロパティ] ダイアログ ボックス) &#40;レポート ビルダーおよび SSRS&#41;](./chart-legend-formatting-report-builder.md)  
  
