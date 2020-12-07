---
title: 多次元データのパラメーター値の非表示データセットの表示 | Microsoft Docs
description: レポート内のすべてのデータセットを表示できるように、パラメーター値の非表示データセットを表示する方法について説明します。
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: eb01c4ca-4fd6-4629-b595-f0d2565915df
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4118c7ad1cccb46a08ec200eef223f62010cf45e
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91890821"
---
# <a name="show-hidden-datasets-for-parameter-values---multidimensional-data"></a>多次元データのパラメーター値の非表示データセットの表示
  既定ではレポート データ ペインに表示されない、自動的に生成されたデータセット (非表示のデータセット) がレポートに含まれる場合があります。 これらのデータセットは次のような場合に作成されます。  
  
-   多次元データベース用のクエリ デザイナーの中には、フィルターを適用するフィールドをクエリ ペインのフィルター領域で指定して、そのフィルターのクエリ パラメーターを作成するかどうかを選択できるものがあります。 そのような場合にパラメーターを作成するように選択すると、そのレポート パラメーターの有効な値を提供するレポート データセットが自動的に作成されます。  
  
-   多次元データベースに基づくクエリをインポートすると、非表示のデータセットもレポートに含まれる場合があります。  
  
 非表示のデータセットはウィザードからは使用できません。  
  
 レポート データ ペインで、レポートのすべてのデータセットを表示するビューを変更することができます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-hidden-datasets"></a>非表示のデータセットを表示するには  
  
-   レポート データ ペインで、[データセット] フォルダーを右クリックし、 **[非表示データセットの表示]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [クエリ デザイン ツール (SSRS)](query-design-tools-ssrs.md)   
 [Reporting Services クエリ デザイナー](/previous-versions/sql/)   
 [レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [レポート データセット (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)  
  
