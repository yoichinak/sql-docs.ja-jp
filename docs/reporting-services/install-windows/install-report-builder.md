---
title: レポート ビルダーをインストールする | Microsoft Docs
description: レポート ビルダーは、ユーザーまたは管理者がお使いのコンピューターにインストールする、スタンドアロン アプリです。
ms.date: 01/31/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.assetid: 6b2291bb-1d20-4d08-81cb-a16dd8e01faf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 98134fb195b9184bb10905b4a4f8ddec48f3cb57
ms.sourcegitcommit: d35d0901296580bfceda6e0ab2e14cf2b7e99a0f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2020
ms.locfileid: "92496984"
---
# <a name="install-report-builder"></a>レポート ビルダーをインストールする

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] はスタンドアロン アプリです。ユーザーまたは管理者によってコンピューターにインストールされます。 Microsoft ダウンロード センター、 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] レポート サーバー、または [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]と統合された SharePoint サイトからインストールできます。  

> [!NOTE]
> 代わりに Power BI Report Builder のインストール情報をお探しですか? ダウンロード センターの [Microsoft Power BI Report Builder](https://www.microsoft.com/download/details.aspx?id=58158) ページに移動します。 

 管理者は通常、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインストールと構成、Web ポータルから [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] をダウンロードするための権限の許可、フォルダーの管理とレポート サーバーに保存されたレポート、レポート パーツ、および共有データセットに対する権限の管理を行います。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 管理の詳細については、「[Reporting Services Report Server &#40;Native Mode&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)」 (Reporting Services レポート サーバー &#40;ネイティブ モード&#41;) を参照してください。  
  
## <a name="install-ssrbnoversion-from--a--web-portal-or-sharepoint-library"></a>Web ポータルまたは SharePoint ライブラリから [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] をインストールする 

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web ポータル、または [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] と統合された SharePoint サイトから [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] を起動できます。 詳細については、「 [レポート ビルダーの起動](../../reporting-services/report-builder/start-report-builder.md)」を参照してください。  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
### <a name="sharepoint-site-integrated-with-ssrsnoversion"></a>統合された SharePoint サイト: [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]と統合された SharePoint サイトで、 **[新しいドキュメント]** メニューに **[レポート ビルダー レポート]** 、 **[レポート ビルダーのモデル]** 、および **[レポート データ ソース]** が表示されない場合は、それらのコンテンツの種類を SharePoint ライブラリに追加する必要があります。 詳細については、「 [SharePoint ライブラリへの Reporting Services のコンテンツの種類の追加](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)」をご覧ください。  

::: moniker-end
 
## <a name="install-ssrbnoversion-with-microsoft-endpoint-configuration-manager"></a>Microsoft Endpoint Configuration Manager で [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] をインストールする 
  
 お使いのコンピューターへのプログラムのプッシュに、管理者が Microsoft Endpoint Configuration Manager などのソフトウェアを使用することも可能です。 特定のソフトウェアを使用して [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]をインストールする方法については、そのソフトウェアのマニュアルを参照してください。 詳細については、「[Microsoft Endpoint Configuration Manager のドキュメント](/configmgr/)」を参照してください。  
  
> [!IMPORTANT]  
>  Windows Vista および Windows 7 でコマンド ライン操作を実行するには、セキュリティ機能に基づいて高度な権限が必要となり、コマンド ラインの実行権限が要求されます。 インストールはサイレント モードになりません。 インストールをサイレント モードにするには、管理者としてコマンド ラインを実行する必要があります。  
  
## <a name="system-requirements"></a>システム要件
  
 Microsoft ダウンロード センターの **レポート ビルダーのダウンロード ページ** で、「 [システム要件](https://go.microsoft.com/fwlink/?LinkID=734968) 」セクションを参照してください。
  
##  <a name="to-install-ssrbnoversion-from-the-download-site"></a><a name="download"></a> ダウンロード サイトから [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] をインストールするには  
  
1.  [Microsoft ダウンロード センターのレポート ビルダー ページ](https://go.microsoft.com/fwlink/?LinkID=734968) で、 **[ダウンロード]** をクリックします。  
  
2.  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] のダウンロードが完了したら、 **[実行]** をクリックします。  
  
     これで SQL Server [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] ウィザードが起動します。  
  
3.  使用許諾契約書に同意して、 **[次へ]** をクリックします。  
  
4.  **[既定のターゲット サーバー]** ページで、必要に応じて対象レポート サーバーの URL を指定します (既定の URL と異なる場合)。 **[次へ]** をクリックします。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] をレポート サーバーに接続して使用する場合は、ここでサーバーの URL を指定すると便利です。 また、[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] の **[オプション]** ダイアログ ボックスからも実行できます。  
  
5.  **[インストール]** をクリックして [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] のインストールを完了します。  
  
## <a name="to-install-ssrbnoversion-from-a-share"></a>共有から [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] をインストールするには  
  
1.  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] をお使いのローカル コンピューターにインストールするために実行する ReportBuilder.msi の場所については、管理者にお問い合わせください。  
  
2.  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] の Windows インストーラー パッケージ (MSI) である ReportBuilder.msi の場所を検索してクリックします。  
  
     これで SQL Server [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] ウィザードが起動します。  
  
3.  「 [ダウンロード サイトからレポート ビルダーをインストールするには](#download)」の残りの手順を完了します。  
  
## <a name="to-install-ssrbnoversion-from-the-command-line"></a>コマンド ラインから [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] をインストールするには 

 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] のインストールをコマンド ラインから実行し、引数を指定してインストールをカスタマイズすることもできます。 標準の MSI 固有パラメーターに加えて、[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] に用意されている使用できるカスタム パラメーターはRBINSTALLDIR と RBSERVERURL。 RBINSTALLDIR では、[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 用のルート インストール フォルダーを指定します。 RBSERVERURL では、[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] でサーバーにレポートを保存するときに使用される既定のレポート サーバーを指定します。  
  
 ユーザー インターフェイスをまったく操作しない完全なサイレント インストールを実行する場合は、 **/quiet** オプションを指定します。 quiet オプション フラグを使用するとインストール エラーが抑制されるように設計されています。 そのため、quiet オプションを使用する場合は、ログ記録を指定する **/l** オプションを含めることをお勧めします。   
  
1.  [Microsoft ダウンロード センターのレポート ビルダー ページ](https://go.microsoft.com/fwlink/?LinkID=734968)で、 **[ダウンロード]** をクリックします。  
  
2.  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] のダウンロードが完了したら、 **[保存]** をクリックします。  
  
3.  **[スタート]** メニューの **[ファイル名を指定して実行]** をクリックします。  
  
4.  **[開く]** ボックスに「 **cmd.** 」と入力します。  
  
5.  コマンド プロンプト ウィンドウで、ReportBuilder.msi を保存したフォルダーに移動します。  
  
6.  次の形式のコマンドを入力します。  
  
     `msiexec/i ReportBuilder.msi OPTION=OptionValue [OPTION=OptionValue]`  
  
     [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] のインストールに固有の 2 つのオプションは、RBINSTALLDIR と RBSERVERURL。 コマンド ラインにこれらの引数を含める必要はありません。 標準的なコマンド ラインは次のとおりです。  
  
     `msiexec /i ReportBuilder3_x86.msi /quiet`  
  
7.  Enter キーを押してコマンドを実行します。  
  
## <a name="set-ssrbnoversion-defaults"></a>[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] の既定値を設定する  
  
-   [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] のインストール後に、一部の既定のオプションを設定できます。 **[ファイル]**  >  **[オプション]** をクリックします。  
  
     既定の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web ポータルまたは SharePoint サイトを設定することをお勧めします。 詳細については、「 [Set default options for Report Builder](../../reporting-services/report-builder/set-default-options-for-report-builder.md)」を参照してください。  
  
-   **[レポート ビルダー]** をクリックします。  
  
     既存のサーバーのリストにレポート サーバーが表示されない場合は、 **[レポートを開く]** ダイアログ ボックスを閉じ、[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] の下部の **[接続]** をクリックしてサーバーに接続します。  
  
## <a name="see-also"></a>関連項目  
 [レポート ビルダーの起動](../../reporting-services/report-builder/start-report-builder.md)   
 [レポート ビルダーをアンインストールする](../../reporting-services/install-windows/uninstall-report-builder.md)  
  
