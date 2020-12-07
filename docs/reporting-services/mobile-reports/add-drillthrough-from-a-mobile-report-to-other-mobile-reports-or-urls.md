---
title: モバイル レポートから他のモバイル レポートまたは URL にドリルスルーを追加する | Microsoft Docs
description: Reporting Services モバイル レポート内の任意のゲージ、グラフ、またはデータ グリッドから、別のモバイル レポートまたはカスタム URL にドリルスルーを追加することができます。
ms.date: 09/20/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 30d0a3fd-5588-417e-b25d-cc5b7624cdb1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 149c074b0aacc56f192b27cfea0894fe2cd73778
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907300"
---
# <a name="add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls"></a>モバイル レポートから他のモバイル レポートまたは URL にドリルスルーを追加する
[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] モバイル レポート内の任意のゲージ、グラフ、またはデータ グリッドから、別のモバイル レポートまたはカスタム URL にドリルスルーを追加することができます。 

*ドリルスルー*  とは、ソース レポートからのリンクで、別のターゲット レポートまたは URL を開きます。 ターゲットのドリルスルー レポートには、多くの場合、要約レポート内の何らかの項目に関する詳細が含まれています。 ソース モバイル レポートに応じて、1 つまたは複数のパラメーターを、ターゲット モバイル レポートに渡すことも、カスタム URL に統合することもできます。  
  
[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] でソース モバイル レポートを表示し、ドリルスルー ターゲットを持つ要素を選択すると、そのターゲット (別のモバイル レポートまたは URL のいずれか) に移動します。  

URL または別のモバイル レポートへのドリルスルーがあるレポート項目。右上にドリルスルー アイコン :::image type="icon" source="../../reporting-services/mobile-reports/media/mobile-report-drill-through-icon.png"::: があります。

![ドリルスルーがあるモバイル レポート ゲージのスクリーンショット。](../../reporting-services/mobile-reports/media/mobile-report-gauge-drill-through.png)

>**ヒント** : ターゲット レポートを作成し、それを最初に [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] Web ポータルに保存します。 ソース レポートからのパラメーターを渡す場合は、そのパラメーターをターゲット レポートにも追加します。 ソース レポートからターゲット レポートへのドリルスルーをセットアップできます。 [モバイル レポートへのパラメーターの追加](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)を行います。
 
## <a name="set-up-drillthrough-to-a-mobile-report"></a>モバイル レポートへのドリルスルーを設定する  

1. [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]のレイアウトビューで、ドリルスルーをサポートする視覚化を選択します。   

   マップおよびゲージは、ほとんどのグラフと単純なデータ グリッドの場合と同様に、ドリルスルーをサポートします。
   
2. **[ビジュアルのプロパティ]** ウィンドウで、 **[ドリルスルー ターゲット]** > **[モバイル レポート]** の順に選択します。  
3. サーバーとターゲット モバイル レポートを選択します。  

   >注: ターゲット モバイル レポートがソース モバイル レポートと同じサーバー上にない場合は、次のセクションの説明に従って、カスタム URL を使用してそれに接続します。  
 
4. ターゲット モバイル レポートを選択すると、使用可能な入力パラメーターが表示されます。これには、ターゲット モバイル レポートのデータセットに対して構成されたナビゲーター コントロールおよびパラメーターにバインドすることができるプロパティも含まれます。  

   ![使用できるレポート パラメーターを示す [ターゲット レポートの構成] ダイアログ ボックスのスクリーンショット。](../../reporting-services/mobile-reports/media/mobile-report-drillthrough-target.PNG)
   
   *ターゲットのモバイル レポートのドリルスルー プロパティ*  
  
5. 各プロパティの右側にある矢印を選択して、データ型が一致するプロパティを、ソース モバイル レポートに対する使用可能な出力プロパティに接続します。 レポート ユーザーが、ソース モバイル レポートをまだ操作していない状態でターゲット モバイル レポートにドリルスルーする場合、出力ごとに既定値を設定することもできます。  
  
## <a name="set-up-a-drillthrough-to-a-custom-url"></a>カスタム URL へのドリルスルーを設定する  
  
1. [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]のレイアウト ビューで、ドリルスルー ターゲットをサポートする視覚化を選択します。    
2. **[ビジュアルのプロパティ]** ウィンドウで **[ドリルスルー ターゲット]** > **[カスタム URL]** の順に選択します。  これにより、ドリルスルー構成用のダイアログ ボックスが開きます。  
  
3. **[ドリルスルー URL の設定]** で、視覚化がクリックされたときに移動する先の URL を入力し、右側に一覧されている **[使用可能なパラメーター]** の中から必要なものを選択します。 サンプルの解決済みパラメーター (取り込まれている場合) と組み合わせられたカスタム URL のプレビューが下のパネルに表示されます。  
  
   ![[ドリルスルー URL の設定] ダイアログ ボックスのスクリーンショット。](../../reporting-services/mobile-reports/media/mobile-report-drillthrough-url.PNG)
  
   *カスタム URL プロパティへにドリルスルーする*  
  
4. **[適用]** をクリックします。  

  
[!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)]のモバイル レポートをプレビューすると、ドリルスルーで視覚化をクリックした場合には、ドリルスルーが無効になっている旨のメッセージが表示されます。 モバイル レポートを保存または公開してからそれを表示すると、その後は、ターゲットへは実際にドリルスルーするしかなく、 [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] のレイアウト モードまたはプレビュー モードでのドリルスルーはできません。  

## <a name="hide-a-target-mobile-report-on-the-web-portal"></a>Web ポータルでターゲット モバイル レポートを非表示にする
ターゲット レポートの既定値を設定しない場合は、Web ポータルでターゲット レポートを非表示にすることを検討してください。 非表示にしなかった場合、誰かが、ソース レポートを参照することなく、Web ポータルでターゲット レポートを直接表示しようとした場合、その内容は空になります。

1. Web ポータルで、非表示にするターゲット レポートに対して省略記号 (...) を選択し、[管理] を選択します。

2. [ **プロパティ** ] で、[ **タイルビューで非表示にする** ] を選択します。

Web ポータルでは非表示項目を確認することができます。 

* Web ポータルの右上で、 **[ビュー]**  >  **[非表示項目の表示]** の順に選択します。 

非表示の項目が、明るい色で表示されます。
    
### <a name="see-also"></a>関連項目  
 
* [Reporting Services モバイル レポートにパラメーターを追加する](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)
* [SQL Server Mobile Report Publisher を使用してモバイル レポートを作成する](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md) 
* [Web ポータル (SSRS ネイティブ モード)](../../reporting-services/web-portal-ssrs-native-mode.md)

