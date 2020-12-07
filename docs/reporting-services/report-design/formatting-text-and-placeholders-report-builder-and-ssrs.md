---
title: テキストとプレースホルダーの書式設定 (レポート ビルダー) | Microsoft Docs
description: レポートビルダーで、フォント、スタイル、色、テキスト内の配置、またはデータ領域を選択し、レポートを読みやすくします。
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- sql11.rtp.rptdesigner.placeholderproperties.font.f1
- "10118"
- "10135"
- sql11.rtp.rptdesigner.textboxproperties.font.f1
- "10132"
- sql11.rtp.rptdesigner.textproperties.font.f1
ms.assetid: 26a4baf2-7bc5-4634-b136-552687ffa477
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e50c5c3f239900ab1c477f1c9d49507b3b4a43e8
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91935342"
---
# <a name="formatting-text-and-placeholders-report-builder-and-ssrs"></a>テキストとプレースホルダーの書式設定 (レポート ビルダーおよび SSRS)
  テキスト ボックスは、データ領域内のレポート アイテムまたは個々のセルであり、テキスト、計算フィールド、データベース内のフィールドへのポインター、またはこの 3 つのアイテムの組み合わせが格納されます。 フォントと色の組み合わせ、太字や斜体のスタイルの追加、整列配置やぶら下げインデントなどの段落スタイルの使用が可能です。 また、テキスト ボックス全体の書式を設定することも、テキスト ボックス内の特定のテキスト、数値、式、またはフィールドの書式を設定することも可能です。  
  
 フォント、サイズ、色、効果などはすべてレポートの読みやすさを左右します。 テキスト ボックスやデータ領域内のテキストに、フォント、フォント スタイル、フォント サイズ、下線などの効果を適用できます。 既定では、使用されるレポート フォントは、Arial (10 ポイント、黒) です。 **[テキスト ボックス]** ダイアログ ボックスと **[テキスト プロパティ]** ダイアログ ボックスでは、レポートが表示されるときのテキストの外観を指定できます。  
  
 ![rs_MixedFormatText](../../reporting-services/report-design/media/rs-mixedformattext.gif "rs_MixedFormatText")  
  
 この図では、テキスト ボックス自体に罫線があり、すべてのテキストが同じテキスト ボックス内にありますが、テキストにはさまざまな書式が設定されています。  
  
 すぐに使用するには、「[チュートリアル:テキストの書式設定 &#40;レポート ビルダー&#41;](../../reporting-services/tutorial-format-text-report-builder.md)」をご覧ください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="creating-placeholder-text-in-a-text-box"></a>テキスト ボックス内のプレースホルダー テキストの作成  
 テキスト ボックス内に単純型または複合型の式が定義されている場合、この式の結果表示される UI を *プレースホルダー*と呼んでいます。 1 つのテキスト ボックス内の任意の数のプレースホルダーまたはテキスト セクションに、色、フォント、アクション、その他の動作を定義できます。  
  
 プレースホルダーの値は常に、単純型または複合型の式です。 式を作成してテキスト ボックスにプレースホルダーを追加するには、次のいずれかの方法に従います。  
  
-   **レポート データ** ペインからテキスト ボックスにフィールドをドラッグしてドロップします。 レポート本文のその他の場所に式をドラッグした場合は、プレースホルダーを含んだ新しいテキスト ボックスが作成されます。 このプレースホルダーの値は、ドロップされたフィールドに対応するフィールド式になります。  
  
-   テキスト ボックス内で右クリックし、 **[プレースホルダーの挿入]** を選択します。 **[プレースホルダーのプロパティ]** ダイアログ ボックスで、プレースホルダーの値として式を指定できます。 詳細については、「 [[全般] ([プレースホルダーのプロパティ] ダイアログ ボックス) (レポート ビルダーおよび SSRS)](./text-boxes-report-builder-and-ssrs.md)」をご覧ください。  
  
-   任意の単純型または複合型の式をテキスト ボックスに入力します。 たとえば、テキスト ボックスに「 **Name: [Name]** 」と入力すると、式 **を表すプレースホルダーとして** [Name] `=Fields!Name.Value`というテキストが表示されます。  
  
-   空のテキスト ボックスに、等号 (=) で始まる式を入力します。 テキスト ボックスからフォーカスを切り替えると、結果の式が編集可能なプレースホルダーに変換されます。 テキスト ボックスが空でない場合や、テキスト ボックス内のテキストが等号 (=) で始まっていない場合は、等号が文字列リテラルとして解釈され、プレースホルダーが作成されません。 単純型または複合型の式の定義方法については、「[レポートでの式の使用 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="formatting-placeholders-and-static-text-in-a-text-box"></a>テキスト ボックス内のプレースホルダーと静的テキストの書式設定  
 **[プレースホルダーのプロパティ]** ダイアログ ボックスを使用してプレースホルダーの書式を設定できます。 書式設定できるのは、プレースホルダーの一部ではなく、プレースホルダー全体です。 基になる式を確認する場合は、プレースホルダーにポインターを合わせます。 基になる式を変更するには、プレースホルダーをダブルクリックするか、プレースホルダーを右クリックして **[プレースホルダーのプロパティ]** を選択します。 **[プレースホルダーのプロパティ]** ダイアログ ボックスの **[全般]** にある **[ラベル]** プロパティを使用すると、UI ラベルも指定できます。 これは、デザイン時に表示されるプレースホルダーのテキストになります。  
  
 ![rs_MixedTextnPlaceholder](../../reporting-services/report-design/media/rs-mixedtextnplaceholder.gif "rs_MixedTextnPlaceholder")  
  
 この図では、リストのテキスト ボックスには、太字の書式が設定されたラベルと書式が設定されていないプレースホルダーがあります。  
  
 プレースホルダー テキストとは異なり、テキスト ボックス内のテキストを個別に配置したり、1 つのテキスト ボックス内に複数の段落を使用したり、テキストのサブセットに他の動作を定義したりできます。  
  
 1 つのテキスト ボックス内のテキストのサブセットに色、フォント、アクション、その他の動作を定義して、レポートのテキストに文書の差し込みやテンプレートを作成できます。 また、1 つのテキスト ボックス内で複数の段落を使用できます。 たとえば、テキストに 2 つの段落がある場合、テキスト ボックス内で ENTER を押すと段落を分けることができます。 個々のテキスト文字列に配置の値を設定することもできます。 また、テキスト ボックス内の個々のテキストにアクションを定義することもできます。 これは、テキスト ボックス内に含まれているテキスト文字列にハイパーリンクを追加する場合に便利です。  
  
> [!NOTE]  
>  テキスト ボックスに定義されたアクションは、テキスト ボックス内の個々のテキストに定義されたアクションよりも優先度が高くなります。  
  
 混合書式設定の詳細については、「[テキスト ボックス内のテキストの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="aligning-horizontal-text-using-general"></a>全般を使用した横方向のテキストの配置  
 **[テキスト ボックスのプロパティ]** ダイアログ ボックスの **[配置]** では、テキストを横方向に配置する方法を指定できます。 配置の値を指定しなければ、配置の既定値は **[既定]** になります。 つまり、テキストはプレースホルダーの値のフィールド タイプに基づいて配置されます。 非数など、文字列以外に評価される式を指定すると、テキストが右揃えになります。 数値など、式が文字列に評価される場合は、テキストが左揃えになります。  
  
## <a name="see-also"></a>参照  
 [式 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [グラフの軸ラベルの書式設定 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [ゲージのスケールの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [[プレースホルダーのプロパティ] ダイアログ ボックス、[全般] &#40;レポート ビルダーおよび SSRS&#41;](./text-boxes-report-builder-and-ssrs.md)   
 [Microsoft Excel へのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)   
 [テキスト ボックス (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)  
  
