---
title: サブスクリプションの操作 (Web ポータル) | Microsoft Docs
description: '[サブスクリプション] ページを使用して、Reporting Services の現在のレポートのサブスクリプションをすべて表示する方法について説明します。'
ms.date: 01/31/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 09e8ece5-0200-41f2-87c1-9fab19e261be
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4efd72f1c2d6f9098e2af4840483d38d4749d264
ms.sourcegitcommit: 80701484b8f404316d934ad2a85fd773e26ca30c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93243747"
---
# <a name="working-with-subscriptions-web-portal"></a>サブスクリプションの操作 (Web ポータル)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

[サブスクリプション] ページは、現在のレポートのサブスクリプションをすべて表示するために使用します。 [すべてのサブスクリプションを管理] での指定により十分な権限を持っている場合、すべてのユーザーのサブスクリプションを表示できます。 それ以外の場合、このページには自分のサブスクリプションのみが表示されます。  
  
新しいサブスクリプションを作成するには、保存されている資格情報がレポートのデータ ソースで使用されていることを確認する必要があります。 資格情報を保存するには [データ ソース] プロパティ ページを使用します。  
  
> [!NOTE]
> SQL Server エージェント サービスを開始する必要があります。   
  
![サブスクリプションの管理](../reporting-services/media/working-with-subscriptions-web-portal/ssrs-manage-subscriptions.png)  
レポートの **省略記号 [...]** 、 **[管理]** 、 **[サブスクリプション]** の順に選択して、[サブスクリプション] ページにアクセスします。  
  
[サブスクリプション] ページで、 **[+ 新しいサブスクリプション]** を選択すると、新しいサブスクリプションを作成できます。 既存のサブスクリプションを編集したり、選択したサブスクリプションを削除したりすることもできます。  
  
また、このページでは、実行したサブスクリプションの結果の状態も **[結果]** 列に示されます。 サブスクリプションのエラーが発生した場合、メッセージの内容を表示するには、最初に [結果] 列を確認する必要があります。 

[サブスクリプション] ページで **[今すぐ実行]** を選択して、必要に応じてサブスクリプションを実行することもできます。
  
## <a name="creating-or-editing-a-subscription"></a>サブスクリプションの作成と編集  
[新しいサブスクリプション] ページまたは [サブスクリプションの編集] ページでは、レポートに新しいサブスクリプションを作成したり、既存のサブスクリプションを変更したりできます。 このページに表示されるオプションは、ロールの割り当てによって異なります。 高度な権限を持つユーザーは、追加のオプションを使用して作業できます。  
  
サブスクリプションは、自動的に実行できるレポートでサポートされています。 少なくとも、レポートでは、格納された資格情報を使用するか、資格情報を使用しないようにする必要があります。 レポートでパラメーターを使用する場合、既定値を指定する必要があります。 レポート実行の設定を変更したり、パラメーター プロパティで使用される既定値を削除したりすると、サブスクリプションが非アクティブになることがあります。 詳細については、「[ネイティブ モード レポート サーバーのサブスクリプションの作成と管理](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)」を参照してください。  
  
## <a name="type-of-subscription"></a>サブスクリプションの種類  
**[標準サブスクリプション]** と **[データ ドリブン サブスクリプション]** から選択できます。  
  
![[サブスクリプションの種類] セクションを示すスクリーンショット。](../reporting-services/media/working-with-subscriptions-web-portal/ssrswebportal-subscriptions3.png)  
   
データ ドリブン サブスクリプションは、サブスクリプションを実行するたびに、サブスクライバー データベースにサブスクリプション情報をクエリするサブスクリプションです。 データ ドリブン サブスクリプションはクエリ結果を使用して、サブスクリプションの受信先、配信設定、およびレポート パラメーターの値を決定します。 実行時に、レポート サーバーで、サブスクリプションの設定に使用されている値を取得するクエリが実行されます。   
  
データドリブン サブスクリプションを作成するには、サブスクリプションのデータを取得するクエリまたはコマンドの記述方法についての知識が必要です。 また、サブスクリプションで使用するサブスクライバー データ (サブスクライバーの名前や電子メール アドレスなど) を格納するデータ ストアが必要です。  
  
このオプションを使用できるのは、高度な権限を持つユーザーのみです。 既定のセキュリティを設定している場合、[個人用レポート] フォルダーにあるレポートに対してデータ ドリブン サブスクリプションを使用することはできません。  
  
## <a name="destination"></a>到着地  
レポートの配信に使用する配信拡張機能を選択します。   
  
配信拡張機能を使用できるかどうかは、配信拡張機能がレポート サーバーにインストールおよび構成されているかどうかによって決まります。 レポート サーバーの電子メールは、既定の配信拡張機能ですが、使用する前に構成する必要があります。 ファイル共有配信は構成の必要はありませんが、共有フォルダーは使用前に定義が必要です。  
  
![[宛先] セクションと [配信オプション (Windows ファイル共有)] セクションを示すスクリーンショット。](../reporting-services/media/working-with-subscriptions-web-portal/ssrswebportal-subscriptions2.png)  
  
選択した配信拡張機能に応じて、次の設定が表示されます。  
  
-   電子メール サブスクリプションによって、電子メール ユーザーがよく使用するフィールド ([宛先] フィールド、[件名] フィールド、[優先度] フィールドなど) が表示されます。 レポートを埋め込むか添付するには、 **[レポートを含める]** を指定します。レポートに URL を含めるには、 **[リンクを含める]** を指定します。 添付または埋め込みをするレポートの表示形式を選択するには、 **[表示形式]** を指定します。 詳細については、[電子メール サブスクリプションの作成](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md#bkmk_create_email_subscription)に関するページを参照してください。 
  
-   ファイル共有サブスクリプションには、配信先の場所を指定できるフィールドがあります。 ファイル共有には任意のレポートを配信できます。 ただし、対話機能をサポートするレポート (たとえば、対応する行と列へのドリル ダウンをサポートするマトリックス形式のレポート) は、静的ファイルとして表示されます。 静的ファイルに行と列のドリル ダウンを表示することはできません。 ファイル共有名は、汎用名前付け規則 (UNC) 形式 (たとえば、\mycomputer\public\myreportfiles) で指定する必要があります。 パス名の末尾に円記号を含めないでください。 レポート ファイルは、表示形式に基づくファイル形式で配信されます (たとえば、[Excel] を選択した場合、レポートは .xlsx ファイルとして配信されます)。  詳細については、[ファイル共有サブスクリプションの作成](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md#bkmk_create_fileshare_subscription)に関するページを参照してください。
  
## <a name="data-driven-subscription-dataset"></a>データ ドリブン サブスクリプション データセット  
データ ドリブン サブスクリプションの場合は、サブスクリプションで使用されるデータセットを定義する必要があります。 **[データセットの編集]** を選択して情報を指定します。  
  
![[データセット] セクションを示すスクリーンショット。](../reporting-services/media/working-with-subscriptions-web-portal/ssrswebportal-subscriptions4.png)  
  
クエリに使用するには、最初に **[データ ソース]** を指定する必要があります。 共有データ ソースにするか、カスタム データ ソースを指定することができます。  
  
実行するサブスクリプションに必要なさまざまなオプションを一覧する、 **クエリ** を指定する必要があります。 この画面には、返される必要があるフィールドが示されます。 これらのフィールドは、配信方法とレポートのパラメーターによって異なります。  
  
最適な結果を得るには、クエリを最初に SQL Server Management Studio で実行してから、データ ドリブン サブスクリプションで使用します。 こうすると、結果を調べて必要な情報が含まれているかどうかを確認できます。 クエリ結果に関して重要な点は次のとおりです。  
  
-   結果セット内の列によって、配信オプションおよびレポート パラメーターに指定できる値が決まります。 たとえば、メール配信のデータ ドリブン サブスクリプションを作成する場合は、メール アドレスの列が必要です。  
  
-   結果セット内の行によって、生成されるレポート配信の数が決まります。 行数が 10,000 の場合、レポート サーバーから通知と配信が 10,000 回生成されます。  
  
![[クエリ] セクションを示すスクリーンショット。](../reporting-services/media/working-with-subscriptions-web-portal/ssrswebportal-subscriptions5.png)  
  
クエリを検証できます。 また、 **query timeout** を定義することもできます。  
  
クエリが作成された後、必要なフィールドに値を割り当てることができます。 手動のデータを入力するか、作成したデータセットからフィールドを選択できます。 

## <a name="next-steps"></a>次のステップ

[ネイティブ モード レポート サーバーのサブスクリプションの作成と管理](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)
[Web ポータル](../reporting-services/web-portal-ssrs-native-mode.md)  
[ページ分割されたレポートの使用](working-with-paginated-reports-web-portal.md)  
[共有データセットの操作](../reporting-services/work-with-shared-datasets-web-portal.md)

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
