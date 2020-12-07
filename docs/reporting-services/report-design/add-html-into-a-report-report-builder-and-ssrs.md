---
title: レポートへの HTML の追加 (レポート ビルダー) | Microsoft Docs
description: レポート ビルダーで、自分のレポートで使用する目的で、自分のデータセットのフィールドにあるプレースホルダーを使用し、HTML をインポートする方法について説明します。
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 30bd631a-f774-48e7-a13a-b6c2eb54d9bb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b2fcdc9d0ff735f069a897626b454bcf4e4cccee
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91933341"
---
# <a name="add-html-into-a-report-report-builder-and-ssrs"></a>レポートへの HTML の追加 (レポート ビルダーおよび SSRS)
  レポートでプレースホルダーを使用すると、データセットのフィールドから HTML をインポートできます。 既定のプレースホルダーはプレーン テキストを表すため、プレースホルダーのマークアップ タイプを HTML に変更する必要があります。 詳細については、[「レポートへの HTML のインポート &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/importing-html-into-a-report-report-builder-and-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-html-from-a-field-in-your-dataset-into-a-text-box"></a>データセットのフィールドからテキスト ボックスに HTML を追加するには  
  
1.  **[挿入]** タブの **[一覧]** をクリックします。 デザイン画面をクリックし、次にマウスをドラッグして、必要なサイズのボックスを作成します。  
  
     **[データセットのプロパティ]** ダイアログ ボックスが表示されます。 共有データセットまたはレポートに埋め込まれたデータセットを使用できます。 詳細については、「[[クエリ] ([データセットのプロパティ] ダイアログ ボックス) &#40;レポート ビルダー&#41;](../../reporting-services/report-data/dataset-properties-dialog-box-query-report-builder.md)」または「[[クエリ] ([データセットのプロパティ] ダイアログ ボックス)](/previous-versions/sql/)」を参照してください。  
  
2.  **[挿入]** タブの **[テキスト ボックス]** をクリックします。 一覧内をクリックし、次にマウスをドラッグして、必要なサイズのボックスを作成します。  
  
3.  データセットからテキスト ボックスに HTML フィールドをドラッグします。 フィールドに対してプレースホルダーが作成されます。  
  
4.  プレースホルダーを右クリックし、 **[プレースホルダーのプロパティ]** をクリックします。  
  
5.  **[全般]** タブの **[値]** ボックスに、手順 3 でドロップしたフィールドを評価する式が入力されていることを確認します。  
  
6.  **[HTML - HTML タグをスタイルとして解釈]** をクリックします。 これで、フィールドが HTML として評価されます。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [数値と日付の書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [線、色、および画像の書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/formatting-lines-colors-and-images-report-builder-and-ssrs.md)   
 [[全般] ([プレースホルダーのプロパティ] ダイアログ ボックス) &#40;レポート ビルダーおよび SSRS&#41;](./text-boxes-report-builder-and-ssrs.md)  
  
