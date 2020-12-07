---
title: レポートの実行プロパティを構成する - Reporting Services | Microsoft Docs
description: レポートが要求されるたびに同じデータを取得するオーバーヘッドを回避するために、レポート処理オプションを設定してレポート データを取得するタイミングを指定する方法について説明します。
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- report execution properties [Reporting Services]
- reports [Reporting Services], properties
- reports [Reporting Services], execution options
ms.assetid: 73cc8dcc-ef80-40d7-9739-d33bba0eb28a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 13b74b5437eb9df1cd51425929ffb70770595a69
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988390"
---
# <a name="configure-execution-properties-for-a-report"></a>レポートの実行プロパティを構成する
  レポートの処理オプションでは、レポート データが取得されるタイミングを指定できます。 レポート データ処理のスケジュールを設定することは、外部データ ソースが特定の時刻に更新される場合 (日次または週次で更新されるデータ ウェアハウスなど) や、レポート要求のたびに同じデータが取得されるオーバーヘッドを回避したい場合などに効果的です。 また、外部のデータベース サーバーにかかる処理負荷を制御する場合や、まったく同じ一連のデータを扱う複数のユーザーに一貫性した結果を提供する場合に役立てることもできます。 変化しやすいデータを使用した場合、レポートを要求するたびに異なる結果が生成される可能性があります。 一方、レポート スナップショットでは、同時点のデータを含む他のレポートや分析ツールとの有効な比較が可能になります。  
  
 レポート スナップショットは、特定の時点で取得されたレイアウト指定およびクエリ結果を含むレポートです。 レポートを選択したときに最新のクエリ結果を取得する要求時レポートとは異なり、レポート スナップショットはスケジュールに従って処理され、その後、レポート サーバーに保存されます。 表示するレポート スナップショットを選択すると、レポート サーバーによってレポート サーバー データベースに格納されたレポートが取得され、スナップショット作成時点のレポートで最新だったデータとレイアウトを表示します。  
  
 レポート スナップショットは、特定の表示形式では保存されません。 その代わりに、レポート スナップショットは、ユーザーまたはアプリケーションが要求したときのみ、最終的な表示形式 (HTML など) で表示されます。 遅延表示により、スナップショットの移植性が実現します。 レポートは、要求元のデバイスまたは Web ブラウザーの適切な形式で表示できます。  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
## <a name="to-configure-report-processing-options"></a>レポート処理オプションを構成するには  
  
1.  [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](../web-portal-ssrs-native-mode.md) を開始します。  
  
2.  処理オプションを設定するレポートに移動し、そのレポートを開きます。  
  
 レポートの上にマウス ポインターを移動し、下矢印をクリックします。  
  
1.  ドロップダウン メニューで、 **[管理]** をクリックし、 **[処理オプション]** タブを選択します。  
  
2.  **[このレポートを実行スナップショットから表示する]** をクリックしてから、次のオプションのいずれかを選択します。  
  
    -   スナップショットを作成する場合は、 **[次のスケジュールを使用して、レポート実行スナップショットを作成する]** を選択し、レポート固有のスケジュールを定義するか、または **[共有スケジュール]** 一覧からスケジュールを選択します。  
  
    -   スナップショットをすぐに作成する場合は、 **[このページの [適用] ボタンをクリックしたときに、レポート スナップショットを作成します]** を選択します。  
  
3.  **[Apply]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [レポート処理プロパティの設定](../../reporting-services/report-server/set-report-processing-properties.md)   
 [[コンテンツ] ページ (レポート マネージャー)](/previous-versions/sql/sql-server-2016/ms186470(v=sql.130))   
 [レポート サーバー コンテンツの管理 &#40;SSRS ネイティブ モード&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [[処理オプション] プロパティ ページ &#40;レポート マネージャー&#41;](/previous-versions/sql/sql-server-2016/ms178821(v=sql.130))  
  
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
  
## <a name="to-configure-report-execution-properties"></a>レポート実行プロパティを構成するには  
  
「[レポート サーバーの Web ポータル (SSRS ネイティブ モード)](../../reporting-services/web-portal-ssrs-native-mode.md)」から:  
  
1. 実行プロパティを構成するレポートに移動します。  
  
2. レポートを右クリックし、ドロップダウン メニューから **[管理]** を選択します。

3. **[履歴スナップショット]** タブを選択すると、 **[履歴スナップショット]** ページが表示されます。  
  
4. **[Schedules and settings]\(スケジュールと設定\)** ボタンを選択し、 **[スケジュールに従って履歴スナップショットを作成する]** がオンになっていない場合はオンにします。
  
5. 必要に応じて **[共有スケジュール]** または **[レポート固有スケジュール]** を選択します。  
  
6. **[詳細]** セクションで、履歴スナップショットに望ましい**アイテム保持**ポリシーを選択します。  
  
7. **[適用]** を選択します。  
  
   >[!NOTE]
   >スナップショットをすぐに作成する場合、 **[Schedules and settings]\(スケジュールと設定\)** ボタンではなく **[新しい履歴スナップショット]** ボタンを選択します。レポート スナップショットが直後に作成されます。  
  
## <a name="see-also"></a>関連項目  
 [レポート処理プロパティの設定](../../reporting-services/report-server/set-report-processing-properties.md)   
 [レポート サーバー コンテンツの管理 (SSRS ネイティブ モード)](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [レポート処理プロパティの設定](../../reporting-services/report-server/set-report-processing-properties.md)   

::: moniker-end