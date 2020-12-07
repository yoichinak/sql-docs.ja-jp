---
title: モバイル レポートで Analysis Services の日付の書式設定を保持する | Reporting Services | Microsoft Docs
description: Mobile Report Publisher では、レポート ビルダー内の共有データセットにメジャーを追加して、Analysis Services データ ソースの日付のデータ型が保持されるようにします。
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: e9a9a199-40e3-4381-b250-1b99fb83aa62
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5fef66452820975107e06e20a4085978163d957d
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907099"
---
# <a name="retain-date-formatting-for-analysis-services-in-mobile-reports"></a>モバイル レポートで Analysis Services の日付の書式設定を保持する
レポート ビルダー内の共有データセットにメジャーを追加して、 [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] データ ソースの日付のデータ型が [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)]で保持されるようにします。

[!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] クエリの既定の戻り値型は文字列です。  [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] レポート ビルダーでデータセットを作成する際には、文字列型が使用され、サーバーに保存されます。 

ただし、JSON テーブル レンダラーはデータセットを処理する際、列の値を文字列として読み取り、文字列を表示します。  また [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)] も、テーブルを取得する際に文字列のみを認識します。

これを回避するには、レポート ビルダーで共有データセットを作成する際に、計算されるメンバーを追加します。 この方法は、 [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] の多次元モデルとテーブル モデルの両方に対して有効です。

## <a name="create-a-measure-to-retain-a-date-field-data-type"></a>日付フィールドのデータ型を保持するためにメジャーを作成する

1. 日付フィールドの値を保持するためのメジャーを作成し、式フィールドで日付の階層/レベルを選択し、 **.CurrentMember.MemberValue** を追加します。 次に例を示します。
 
   [Internet Sales].[Ship Date].CurrentMember.MemberValue
   
   ![[計算されるメンバー ビルダー] ダイアログ ボックスのスクリーンショット。[式] テキスト ボックスにコールアウトが付いています。](../../reporting-services/mobile-reports/media/ssas-calculated-member-report-builder.png)
   
2. 次に、左下の [計算されるメンバー] 一覧から、この計算されるメンバーをドラッグし、右側の列グリッドにドロップすると、その計算されるメンバーが一連の列に追加されます。  

   ![クエリ デザイナーのスクリーンショット。[計算されるメンバー] セクションにコールアウトが付いています。](../../reporting-services/mobile-reports/media/ssas-query-designer-calculated-member-report-builder.png) 
   
### <a name="see-also"></a>関連項目

-  [Reporting Services モバイル レポートのデータ](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)
-  [Reporting Services モバイル レポート用にデータを準備する](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)
