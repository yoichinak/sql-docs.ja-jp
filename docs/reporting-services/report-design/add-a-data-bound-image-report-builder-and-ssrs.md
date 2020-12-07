---
title: データ バインド画像の追加 (レポート ビルダー) | Microsoft Docs
description: レポート ビルダーのご自分のレポートに表示する、データベースに格納されている画像を参照する方法について説明します。
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: df4c38d4-bfcc-41c4-aa6d-952ca6fd7a2e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3357ea613a528de5aa216c538d83c1e616b1f470
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91935262"
---
# <a name="add-a-data-bound-image-report-builder-and-ssrs"></a>データバインド画像の追加 (レポート ビルダーおよび SSRS)
  レポートには、データベースに保存されている画像への参照を含めることができます。 このような画像を *データバインド画像*と呼びます。 たとえば、製品一覧で製品名と合わせて表示される画像はデータバインド画像です。  
  
 データバインド画像をページ ヘッダーまたはページ フッターに追加するには、別の手順が必要になります。 詳細については、「[ページ ヘッダーとページ フッター &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-data-bound-image"></a>データバインド画像を追加するには  
  
1.  レポート デザイン ビューで、データ ソース接続のあるテーブル、および画像のバイナリ データを含むフィールドのあるデータセットを作成します。 詳細については、「[テーブル &#40;レポート ビルダーおよび SSRS& #41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)」を参照してください。  
  
2.  テーブルに列を挿入します。 詳細については、「[列の挿入または削除 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md)」を参照してください。  
  
3.  **[挿入]** メニューで **[画像]** をクリックし、新しい列のデータ行をクリックします。  
  
4.  **[画像のプロパティ]** ダイアログ ボックスの [全般] ページにある **[名前]** ボックスに名前を入力するか、既定値を受け入れます。  
  
5.  (省略可) **[ツールヒント]** ボックスに、HTML で表示されたレポートの画像の上にマウスを置いたときに表示されるテキストを入力します。  
  
6.  **[画像ソースの選択]** で、 **[データベース]** を選択します。  
  
7.  **[次のフィールドを使用]** で、レポート内の画像を含むフィールドを選択します。  
  
8.  **[次の MIME の種類を使用]** で、画像の MIME の種類またはファイル形式を選択します (bmp など)。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     画像のプレースホルダーがレポート デザイン画面に表示されます。  
  
## <a name="see-also"></a>参照  
 [画像 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)   
 [レポートへの画像の埋め込み &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [外部の画像の追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-an-external-image-report-builder-and-ssrs.md)   
 [[全般] ([画像のプロパティ] ダイアログ ボックス) (レポート ビルダーおよび SSRS)](./images-report-builder-and-ssrs.md)  
  
