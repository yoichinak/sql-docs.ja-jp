---
title: SharePoint モード レポート サーバーのサブスクリプションの作成と管理 | Microsoft Docs
description: SharePoint モードのレポート サーバーと統合されている SharePoint Web アプリから、レポートを配信する Reporting Services サブスクリプションを作成する方法について説明します。
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], creating
- subscriptions [Reporting Services], deleting
- subscriptions [Reporting Services], managing
ms.assetid: 44be7ee2-33ce-46e4-9d1a-a20aaf43a227
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 289483df5c80b4524a281e62b4d63147b6f61bb0
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91986848"
---
# <a name="create-and-manage-subscriptions-for-sharepoint-mode-report-servers"></a>SharePoint モード レポート サーバーのサブスクリプションの作成と管理
  SharePoint モードのレポート サーバーと統合されている SharePoint Web アプリケーションから、レポートを配信する [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サブスクリプションを作成することができます。 サブスクリプションは、ドキュメント ライブラリやファイル フォルダーに対して、または電子メールとしてレポートを配信できます。 このトピックでは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サブスクリプションを作成するための要件と手順についてまとめます。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モード &#124; SharePoint 2010 と SharePoint 2013|  
  
 サブスクリプションを作成する場合、配信を指定する方法には次の 3 つがあります。  
  
-   **ドキュメント ライブラリ**: 元のレポートと同じ SharePoint サイト内のライブラリに、元のレポートに基づくドキュメントを配信するためのサブスクリプションを作成できます。 同じサイト コレクション内の別のサーバーや別のサイト上のライブラリにドキュメントを配信することはできません。 ドキュメントを配信するには、レポートの配信先のライブラリにアイテムを追加する権限が必要です。  
  
-   **ファイル フォルダー:** 元のレポートに基づくドキュメントを、ファイル システムの共有フォルダーに配信できます。 この場合、ネットワーク接続経由でアクセスできる既存のフォルダーを選択する必要があります。  
  
-   **電子メール:** レポート サーバーのメール配信拡張機能を使用できるようにレポート サーバーが構成されている場合は、レポートまたはエクスポートされたレポート ファイル (出力形式で保存) を受信トレイに送信するサブスクリプションを作成できます。 レポートまたはレポート URL なしで通知だけを受信するには、 **[レポートへのリンクを含める]** チェック ボックスと **[メッセージ内にレポートを表示する]** チェック ボックスをオフにします。  
  
 **このトピックの内容:**  
  
-   [サブスクリプションの一般的な要件](#bkmk_subscription_requirements)  
  
-   [SharePoint ライブラリにレポートを配信するサブスクリプションを作成するには](#bkmk_tosharepoint_library)  
  
-   [SharePoint ライブラリにレポートを配信するサブスクリプションを作成するには](#bkmk_tosharepoint_library)  
  
-   [レポート サーバー電子メール配信のサブスクリプションを作成するには](#bkmk_subscription_for_email)  
  
-   [サブスクリプションを表示または変更するには](#bkmk_to_modify_subscription)  
  
-   [サブスクリプションを削除するには](#bkmk_to_delete_subscription)  
  
##  <a name="general-requirements-for-subscriptions"></a><a name="bkmk_subscription_requirements"></a> サブスクリプションの一般的な要件  
 サブスクリプションを作成するには、レポートの表示と警告の作成の権限が必要です。レポートでは、保存された資格情報が使用されている必要があります。  
  
 サブスクリプションを作成する際には、出力ファイル形式を選択できます。 形式によっては正しく機能しないレポートもあります。 サブスクリプションで形式を選択する前に、レポートを開き、別の形式にエクスポートして、期待どおりに表示されることを確認します。  
  
 ユーザーが **サブスクリプションを作成できるようにする場合は、そのユーザーは SharePoint の** アイテムの編集 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] リスト権限を必要とします。 詳細については、「 [レポート サーバー アイテムの SharePoint サイトおよびリスト権限のリファレンス](../../reporting-services/security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)」をご覧ください。  
  
> [!IMPORTANT]  
>  ライブラリまたは共有フォルダーにレポートを配信するサブスクリプションでは、元のレポートに基づいて新しく静的ファイルが作成されますが、これはレポート ビューアー Web パーツで実行される実際のレポート定義ではありません。 元のレポートに対話機能 (ドリルスルー リンクなど) や動的コンテンツが含まれている場合、対象の場所に配信される静的ファイルでは、これらの機能を使用できません。 "Web ページ" を選択すると、ある程度の対話機能を維持することができます。しかし、このドキュメントはレポート ビューアーで実行される .rdl ファイルではないため、レポートをクリックすると新しいページがブラウザー セッションで作成され、サイトに戻るにはそれらをスクロールする必要があります。  
  
 エクスポートされるレポートのファイル名拡張子を .rdl に変更するだけでは、そのレポートをレポート ビューアー Web パーツで実行することはできません。 実際のレポートを提供するサブスクリプションを作成する場合、レポート サーバーの電子メール配信拡張機能を使用して、そのレポートへのリンクを含めるオプションを設定します。  
  
 配信されたドキュメントを格納するライブラリのバージョン設定により、配信ごとにドキュメントの新しいバージョンを作成するかどうかが決まります。 既定では、バージョン設定はライブラリごとに有効です。 **[バージョンを管理しない]** を明確に選択しない限り、配信ごとにドキュメントの新しいメジャー バージョンが作成されます。 サブスクリプションを配信した結果として、ドキュメントのメジャー バージョンのみが作成されます。マイナー バージョンを許可するバージョン管理オプションを設定した場合でも、マイナー バージョンは作成されません。 保持されるメジャー バージョンの数を制限している場合は、制限値に達すると古い配信が新しい配信に置き換えられます。  
  
 サブスクリプション用に選択する出力形式は、レポート サーバーにインストールされた表示拡張機能に基づきます。 そのため、レポート サーバーの表示拡張機能によってサポートされる出力形式しか選択できません。  
  
###  <a name="to-create-a-subscription-to-deliver-a-report-to-a-sharepoint-library"></a><a name="bkmk_tosharepoint_library"></a> SharePoint ライブラリにレポートを配信するサブスクリプションを作成するには  
  
1.  レポートを含む SharePoint ライブラリを参照します。  
  
2.  レポートの隣にある下矢印をクリックして、 **[サブスクリプションの管理]** をクリックします。  
  
3.  **[サブスクリプションの追加]** をクリックします。  
  
4.  **[配信拡張機能]** で、 **[SharePoint ドキュメント ライブラリ]** をクリックします。  
  
5.  **[ドキュメント ライブラリ]** で、同じサイト内のライブラリを選択します。  
  
6.  **[ファイルのオプション]** で、サブスクリプションで作成するドキュメントのファイル名とタイトルを指定します。  
  
7.  **[出力形式]** で、アプリケーションの形式を選択します。  
  
     自己完結型の HTML ファイルを作成できるため、Web アーカイブ (MHTML) が既定の形式になっていますが、元のレポートに対話機能が含まれている場合、この形式では維持できません。  
  
8.  **[上書きオプション]** では、後続の配信でファイルを上書きするかどうかを決めるオプションを指定します。 以前に配信したファイルを残しておきたい場合は、 **[一意な名前のファイルを作成する]** を選択できます。 一意なファイル名を作成するために、新しいファイルには番号が付加されます。  
  
9. **[配信イベント]** では、サブスクリプションを実行するスケジュールまたはイベントを指定します。 カスタム スケジュールを作成するか、使用可能であれば共有スケジュールを選択できます。または、スナップショット データを使って実行されるレポートのデータが更新された場合に、その都度サブスクリプションを実行することもできます。 スケジュールとデータ処理の詳細については、「[処理オプションの設定 (Reporting Services の SharePoint 統合モード)](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)」を参照してください。  
  
10. **[パラメーター]** では、パラメーター化されたレポートに対するサブスクリプションを作成している場合に、サブスクリプション処理時にレポートと共に使用する値を指定します。 選択したレポートにパラメーターが含まれていない場合、パラメーター セクションはこのページに表示されません。 パラメーターの詳細については、「[パブリッシュ済みレポートのパラメーターを設定する方法 (Reporting Services の SharePoint 統合モード)](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md)」を参照してください。  
  
###  <a name="to-create-a-subscription-for-shared-folder-delivery"></a><a name="bkmk_subscription_for_sharedfolder"></a> 共有フォルダーへの配信のサブスクリプションを作成するには  
  
1.  レポートを含む SharePoint ライブラリを参照します。  
  
2.  レポートの隣にある下矢印をクリックして、 **[サブスクリプションの管理]** をクリックします。  
  
3.  **[サブスクリプションの追加]** をクリックします。  
  
4.  **[配信拡張機能]** で、 **[Windows ファイル共有]** をクリックします。  
  
5.  **[ファイル名]** に、共有フォルダー内に作成するファイルの名前を入力します。  
  
6.  **[パス]** に、コンピューターのネットワーク名を含むフォルダー パスを汎用名前付け規則 (UNC) 形式で入力します。 フォルダー パスの末尾には円記号 (バックスラッシュ) を含めないでください。 たとえば、 `\\ComputerName01\Public\MyReports`のようにパスを入力できます。Public と MyReports は共有フォルダーです。  
  
7.  **[表示形式]** では、レポートのアプリケーション形式を選択します。  
  
8.  **[書き込みモード]** では、 **[なし]** 、 **[自動増分]** 、 **[上書き]** の中から選択します。 これらのオプションは、後続の配信でファイルを上書きするかどうかを決定します。 以前に配信したファイルを保持する場合、 **[自動増分]** を選択できます。 一意なファイル名を作成するために、新しいファイルには番号が付加されます。 **[なし]** を選択した場合は、配信先の場所に同じ名前のファイルが既に存在すると配信が行われません。  
  
9. **[ファイル拡張子]** で、アプリケーションのファイル形式に対応するファイル名拡張子を追加する場合は **[True]** 、拡張子を付けずにファイルを作成する場合は [False] を選択します。  
  
10. **[ユーザー名]** および **[パスワード]** には、共有フォルダーに対する書き込み権限のある資格情報を入力します。  
  
11. **[配信イベント]** では、サブスクリプションを実行するスケジュールまたはイベントを指定します。 カスタム スケジュールを作成するか、使用可能であれば共有スケジュールを選択できます。または、スナップショット データを使って実行されるレポートのデータが更新された場合に、その都度サブスクリプションを実行することもできます。 スケジュールとデータ処理の詳細については、「[処理オプションの設定 (Reporting Services の SharePoint 統合モード)](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)」を参照してください。  
  
12. **[パラメーター]** では、パラメーター化されたレポートに対するサブスクリプションを作成している場合に、サブスクリプション処理時にレポートと共に使用する値を指定します。 パラメーターの詳細については、「[パブリッシュ済みレポートのパラメーターを設定する方法 (Reporting Services の SharePoint 統合モード)](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md)」を参照してください。  
  
###  <a name="to-create-a-subscription-for-report-server-e-mail-delivery"></a><a name="bkmk_subscription_for_email"></a> レポート サーバー電子メール配信のサブスクリプションを作成するには  
  
1.  レポートを含む SharePoint ライブラリを参照します。  
  
2.  レポートの隣にある下矢印をクリックして、 **[サブスクリプションの管理]** をクリックします。  
  
3.  **[サブスクリプションの追加]** をクリックします。  
  
4.  **[配信拡張機能]** で、 **[電子メール]** をクリックします。  
  
5.  **[配信オプション]** で、レポートの送信先電子メール アドレスを指定します。  
  
6.  必要に応じて、件名行を変更できます。 件名行では、レポート名とレポートの処理時刻を取得するための組み込みのパラメーターが使用されています。 使用できる組み込みパラメーターはこれらのみです。 これらのパラメーターは、件名行に表示されるテキストをカスタマイズするためのプレースホルダーですが、静的テキストで置き換えることもできます。  
  
7.  メッセージの本文にレポートの URL を埋め込むには、 **[レポートへのリンクを含める]** チェック ボックスをオンにします。  
  
8.  **[レポート コンテンツ]** では、メッセージの本文に実際のレポートを埋め込むかどうかを指定します。  
  
     表示形式およびブラウザーによって、レポートが埋め込まれるか添付されるかが決まります。 ブラウザーが HTML 4.0 および MHTML をサポートする場合、Web アーカイブ表示形式を選択すると、レポートがメッセージの一部として埋め込まれます。 その他すべての表示形式 (CSV、PDF など) では、添付ファイルとしてレポートを配信します。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、レポートを送信する前に、添付ファイルまたはメッセージのサイズを確認しません。 添付ファイルまたはメッセージがメール サーバーで許可された最大サイズを超えると、レポートは配信されません。 レポートのサイズが大きい場合は、他の配信オプション (URL や通知など) のいずれかを選択します。  
  
9. **[配信イベント]** では、サブスクリプションを実行するスケジュールまたはイベントを指定します。 カスタム スケジュールを作成するか、使用可能であれば共有スケジュールを選択できます。または、スナップショット データを使って実行されるレポートのデータが更新された場合に、その都度サブスクリプションを実行することもできます。 スケジュールとデータ処理の詳細については、「[処理オプションの設定 (Reporting Services の SharePoint 統合モード)](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)」を参照してください。  
  
10. **[パラメーター]** では、パラメーター化されたレポートに対するサブスクリプションを作成している場合に、サブスクリプション処理時にレポートと共に使用する値を指定します。 パラメーターの詳細については、「[パブリッシュ済みレポートのパラメーターを設定する方法 (Reporting Services の SharePoint 統合モード)](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md)」を参照してください。  
  
###  <a name="to-view-or-modify-a-subscription"></a><a name="bkmk_to_modify_subscription"></a> サブスクリプションを表示または変更するには  
  
1.  レポートを含む SharePoint ライブラリを参照します。  
  
2.  レポートの隣にある下矢印をクリックして、 **[サブスクリプションの管理]** をクリックします。  
  
3.  各サブスクリプションは、配信の種類で識別されます。 サブスクリプションの種類をクリックし、既存のプロパティを表示および変更します。  
  
###  <a name="to-delete-a-subscription"></a><a name="bkmk_to_delete_subscription"></a> サブスクリプションを削除するには  
  
1.  レポートを含む SharePoint ライブラリを参照します。  
  
2.  レポートの隣にある下矢印をクリックして、 **[サブスクリプションの管理]** をクリックします。  
  
3.  削除するサブスクリプションの横にあるチェック ボックスをオンにし、 **[削除]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [サブスクリプションと配信 &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Reporting Services の電子メール配信](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md)   
 [Reporting Services でのファイル共有の配信](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)   
 [Reporting Services での SharePoint ライブラリへの配信](../../reporting-services/subscriptions/sharepoint-library-delivery-in-reporting-services.md)   
 [電子メール配信用のレポート サーバーの構成 (レポート サーバー構成マネージャー)](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
  
  
