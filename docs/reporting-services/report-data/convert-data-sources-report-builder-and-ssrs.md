---
title: データ ソースの変換 (レポート ビルダー) | Microsoft Docs
description: レポート ビルダーおよびレポート デザイナーでレポート データ ペインのオプションを使用してデータ ソースを変換する方法について説明します。
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], embedded
- data sources [Reporting Services], shared
ms.assetid: 0e099c7e-8c03-43eb-9ea3-76e52d9ebbe3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 58cc14aaa1dace81c3711dfd6bb7d9a24664165d
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891742"
---
# <a name="convert-data-sources-report-builder-and-ssrs"></a>データ ソースの変換 (レポート ビルダーおよび SSRS)
  レポート データ ペインの各データ ソースは、レポートに固有のものとして埋め込まれている場合と、共有されている場合とがあります。 レポート ビルダーにおける共有データ ソースの参照先は、レポート サーバー上または SharePoint サイト上にパブリッシュされた共有データ ソースです。 レポート デザイナーにおける共有データ ソースの参照先は、ソリューション エクスプローラーの **[共有データ ソース]** フォルダーに表示される共有データ ソースです。  
  
 埋め込みデータ ソースと共有データ ソースの相違点の詳細については、「[埋め込みおよび共有のデータ接続またはデータ ソース &#40;レポート ビルダーおよび SSRS&#41;](./data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)」を参照してください。  
  
 共有データ ソースの作成方法の詳細については、「[埋め込みデータ ソースまたは共有データ ソースを作成する &#40;SSRS&#41;](/previous-versions/sql/)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-designer"></a>レポート デザイナー  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>埋め込みデータ ソースから共有データ ソースに変換するには  
  
-   レポート データ ペインでデータ ソースを右クリックし、 **[共有データ ソースに変換]** をクリックします。  
  
    > [!NOTE]  
    >  レポート データ ペインが表示されていない場合は、 **[表示]** メニューの **[レポート データ]** をクリックします。 ペインがフローティング ウィンドウとして開く場合は、ドッキングすることができます。 詳細については、「[レポート デザイナーのレポート データ ペインをドッキングする (SSRS)](../../reporting-services/tools/dock-the-report-data-pane-in-report-designer-ssrs.md)」を参照してください。  
  
     レポート データ ペインでデータ ソース アイコンが共有データ ソースのアイコンに変わります。 ソリューション エクスプローラーでは、同じ名前の共有データ ソースが **[共有データ ソース]** フォルダーに表示されます。  
  
### <a name="to-convert-a-data-source-from-shared-to-embedded"></a>共有データ ソースを埋め込みデータ ソースに変換するには  
  
-   レポート データ ペインでデータ ソースを右クリックし、 **[データ ソースのプロパティ]** ダイアログ ボックスを開いて、 **[埋め込み接続]** をクリックします。 必要な情報を入力します。  
  
     レポート データ ペインでデータ ソース アイコンが共有データ ソースのアイコンに変わります。  
  
## <a name="report-builder"></a>レポート ビルダー  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>埋め込みデータ ソースから共有データ ソースに変換するには  
  
-   レポート データ ペインでデータ ソースを右クリックし、 **[データ ソースのプロパティ]** ダイアログ ボックスを開いて、 **[埋め込み接続]** をクリックします。 必要な情報を入力します。  
  
     レポート データ ペインでデータ ソース アイコンが共有データ ソースのアイコンに変わります。  
  
#### <a name="to-convert-a-data-source-from-shared-to-embedded"></a>共有データ ソースを埋め込みデータ ソースに変換するには  
  
-   レポート データ ペインでデータ ソースを右クリックし、 **[データ ソースのプロパティ]** ダイアログ ボックスを開いて、 **[埋め込み接続]** をクリックします。 必要な情報を入力します。  
  
     レポート データ ペインでデータ ソース アイコンが共有データ ソースのアイコンに変わります。  
  
## <a name="see-also"></a>参照  
 [レポート データ ソースを管理する](../../reporting-services/report-data/manage-report-data-sources.md)   
 [データ接続文字列を作成する - レポート ビルダーおよび SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
