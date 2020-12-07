---
title: レポートの印刷 (レポート ビルダー) | Microsoft Docs
description: ブラウザー、Reporting Services Web ポータル、またはエクスポートされたレポートの表示に使用する任意のアプリケーションで、レポートを表示および印刷できます。
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: b96936c9-c387-41a9-8c19-6eb325769ffd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 68566f7fb3f29f94d2b27bed472c113981afc7cb
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891802"
---
# <a name="print-a-report-report-builder-and-ssrs"></a>レポートの印刷 (レポート ビルダーおよび SSRS)
  レポートをレポート サーバーに保存した後は、ブラウザー、Reporting Services Web ポータル、またはエクスポートされたレポートの表示に使用する任意のアプリケーションで、レポートを表示および印刷できます。 レポートを保存する前にプレビューする場合は、印刷することができます。  
  
 レポートを印刷するときには、使用する用紙のサイズを指定できます。 用紙のサイズによって、レポート内のページ数や各ページに収まるレポート データが決定されます。 用紙のサイズが影響するのは、ハード改ページ レンダラーを使用してレンダリングされるレポートのみです(PDF、画像、または印刷のハード改ページレンダラー)。 用紙サイズの設定はその他のレンダラーには影響しません。 詳しくは、「[レンダリングの動作 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)」をご覧ください。  
  
 Reporting Services Web ポータルのレポート ビューアー ツール バー、またはレポート ビルダーのプレビューでは、レポートを強制改ページ レンダラーにエクスポートしたり、[印刷] ボタンをクリックしてレポートのコピーを印刷したりすることができます。 用紙のサイズやその他のページ設定プロパティの設定が必要になる場合もあります。 **[レポートのプロパティ]** ダイアログ ボックスを使用すると、用紙のサイズを含むページ設定プロパティを変更できます。  
  
 印刷ページの余白は、デザイン モードと実行モードの 2 か所で指定できます。  
  
-   **デザイン モード。** デザイン モードでページの余白を設定した場合は、レポートの保存時に、その設定がレポート定義に保存されます。  
  
-   **実行モード。** 実行モードでページの余白を設定した場合、この情報はレポート定義に保存されません。 次回レポートを印刷するときは、余白を再指定しない限り、レポート定義から設定が取得されます。  
  
    > [!NOTE]  
    >  印刷の余白は、デザイン モードでも実行モードでも表示されません。 デザイン画面領域とレポートの印刷領域の間に関連はありません。 印刷の余白を確認するには、実行モード時に、リボンの **[実行]** タブにある [印刷レイアウト] をクリックします。  
  
 レポートの改ページの詳細については、「[Reporting Services の改ページ (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-print-a-report-in-report-builder"></a>レポート ビルダーでレポートを印刷するには  
  
1.  レポートを開きます。  
  
2.  [ホーム] タブで **[実行]** をクリックします。  
  
3.  (省略可) 印刷するレポートの外観を確認するには、 **[印刷レイアウト]** をクリックします。  
  
4.  (省略可) 用紙、用紙の向き、および余白を設定するには、 **[ページ設定]** をクリックします。  
  
    > [!NOTE]  
    >  これらの既定値は、[デザイン] ビューで設定されているレポート プロパティから取得されます。 ここで設定した **[ページ設定]** ダイアログ ボックスの値は、このセッションでのみ有効です。 このレポートを閉じてから再度開くと、既定値に戻ります。  
  
5.  **[印刷]** をクリックします。  
  
6.  **[印刷]** ダイアログ ボックスで、プリンターを選択し、その他の印刷オプションを指定します。  
  
### <a name="to-print-a-report-from-a-web-browser-application"></a>Web ブラウザー アプリケーションからレポートを印刷するには  
  
1.  Reporting Services Web ポータルで、印刷するレポートに移動します。 レポートを開きます。  
  
3.  レポート上部のツール バーで **[印刷]** をクリックします。  
  
    > [!NOTE]  
    >  HTML レポートを初めて印刷する場合、印刷に必要な ActiveX コントロールのインストールを促すメッセージが表示されます。 印刷するためには、このコントロールをインストールして構成する必要があります。  
  
4.  **[印刷]** ダイアログ ボックスでプリンターを選択し、 **[印刷]** をクリックします。  
  
### <a name="to-print-a-report-from-other-applications"></a>他のアプリケーションからレポートを印刷するには  
  
1.  Reporting Services Web ポータルで、印刷するレポートに移動します。 レポートを開きます。  
  
2.  レポート上部のツール バーから表示形式を選択して、 **[エクスポート]** をクリックします。 選択した表示形式に対応するビューアー アプリケーションでレポートが表示されます。  
  
     たとえば、PDF を選択した場合、Adobe Acrobat Reader でレポートが表示されます。  
  
3.  このプログラムで **[ファイル]** メニューの **[印刷]** をクリックします。  
  
### <a name="to-change-paper-size"></a>ページ サイズを変更するには  
  
1.  レポート本文の外側を右クリックし、 **[レポートのプロパティ]** をクリックします。  
  
2.  **[ページ設定]** で **[用紙サイズ]** ボックスの一覧から値を選択します。 各オプションによって、 **[幅]** プロパティと **[高さ]** プロパティの値が設定されます。 **[幅]** ボックスと **[高さ]** ボックスに数値を入力することにより、カスタム サイズを指定することもできます。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  サイズの値には、ユーザーのロケール設定に基づいた既定の単位が使用されます。 別の単位を指定するには、数値の後に cm、mm、pt、pc などの物理的な単位指定子を入力します。  
  
### <a name="to-set-page-margins-in-design-mode"></a>デザイン モードでページの余白を設定するには  
  
-   デザイン画面の周りの青い領域を右クリックし、 **[レポートのプロパティ]** をクリックしてから **[ページ設定]** ページをクリックします。  
  
### <a name="to-set-page-margins-in-run-mode"></a>実行モードでページの余白を設定するには  
  
-   **[実行]** タブの **[ページ設定]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [レポートの印刷 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
 [レポートのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [[ページ設定] ([レポートのプロパティ] ダイアログ ボックス) (レポート ビルダー)](/previous-versions/sql/sql-server-2016/dd220640(v=sql.130))   
 [レポート デザイン ビュー &#40;レポート ビルダー&#41;](../../reporting-services/report-builder/report-design-view-report-builder.md)  
  
