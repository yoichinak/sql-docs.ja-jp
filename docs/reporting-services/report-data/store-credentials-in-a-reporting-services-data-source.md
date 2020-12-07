---
title: Reporting Services データ ソースに資格情報を保存する | Microsoft Docs
description: ネイティブ モードと SharePoint モードの両方のレポート サーバーに対して、保存された資格情報を構成する方法について説明します。
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.custom: ''
ms.date: 05/24/2018
ms.openlocfilehash: 2b9db41c61a0e50dffd6a31fffa25f02f1e8369e
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91935233"
---
# <a name="store-credentials-in-a-reporting-services-data-source"></a>Store Credentials in a Reporting Services Data Source

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)]

::: moniker-end

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーが、レポートに必要な外部データにアクセスするときに使用する、保存された資格情報を構成できます。 保存された資格情報は、レポートを自動実行する場合に使用されます。たとえば、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サブスクリプションがレポートを電子メールとしてパブリッシュする場合などです。 この資格情報は、レポート処理がスケジュールで設定されている場合、または、レポート処理がトリガーされた場合に、レポート サーバーによって取得されて使用されます。 このトピックでは、ネイティブ モードと SharePoint モードの両方のレポート サーバーに対して、保存された資格情報を構成する方法について説明します。  
  
##  <a name="security-policy-requirements-for-stored-credentials"></a><a name="bkmk_top"></a> 保存された資格情報のセキュリティ ポリシー要件  
 ![as_powerpivot_refresh_sss_set_key](/analysis-services/analysis-services/power-pivot-sharepoint/media/as-powerpivot-refresh-sss-set-key.gif "as_powerpivot_refresh_sss_set_key") 保存された資格情報に使用するアカウントを、レポート サーバー上で、次のいずれかのセキュリティ ポリシー用に構成する必要があります。 環境に必要な最小レベルの権限を持つポリシーを選択することをお勧めします。  
  
1.  **ローカル ログオンを許可する**。 詳細については、「 [ローカル ログオンを許可する](https://technet.microsoft.com/library/cc756809\(v=WS.10\).aspx)」を参照してください。  
  
2.  **バッチ ジョブとしてログオン**。 詳細については、「 [バッチ ジョブとしてログオン](https://technet.microsoft.com/library/cc755659\(v=ws.10\).aspx)」を参照してください。  
  
3.  ポリシーに関する一般的な情報については、「 [グループ ポリシー オブジェクトのセキュリティの設定を編集する](https://technet.microsoft.com/library/cc736516\(v=ws.10\).aspx)」を参照してください。  
  
##  <a name="configure-stored-credentials-for-a-report-specific-data-source-native-mode"></a><a name="bkmk_stored_credentials_data_source_native"></a> レポート固有のデータ ソース用の保存された資格情報を構成する (ネイティブ モード)  
  
1.  Web ポータルで、レポートが含まれているフォルダーを参照します。 レポート タイルの右上隅にある省略記号 (...) をクリックします。  
  
2.  **[管理]** をクリックして、 **[データ ソース]** をクリックします。  
  
3.  **[カスタム データ ソース]** をクリックします。  
  
4.  **[データ ソースの種類]** の一覧で、データ ソースから取得したデータの処理に使用するデータ処理拡張機能を選択します。  
  
5.  **[接続文字列]** でレポート サーバーがデータ ソースへの接続に使用する接続文字列を指定します。 以下に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースへの接続に使用する接続文字列の例を示します。  
  
    ```  
    data source=<servername>;initial catalog=AdventureWorks2012  
    ```  
  
6.  **[接続に使用する認証]** で、 **[レポート サーバーに保存され、セキュリティで保護された資格情報]** をクリックします。  
  
7.  ユーザー名とパスワードを入力します。  
  
    -   このアカウントが Windows ドメイン ユーザー アカウントである場合は、\<domain>\\<account\> という形式で指定し、 **[データ ソースへの接続時に Windows 資格情報として使用する]** チェック ボックスをオンにします。  
  
    -   ユーザー名とパスワードがデータベースの資格情報である場合は、 **[データ ソースへの接続時に Windows 資格情報として使用する]** を選択しないでください。 データベース サーバーが権限の借用または委譲をサポートしている場合は、 **[データ ソースへの接続が確立した後に、認証されているユーザーの権限を借用する]** を選択できます。  
  
8.  **[Apply]** をクリックします。  
  
     ![[トップに戻る] リンクで使用される矢印アイコン](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン") [保存された資格情報のセキュリティ ポリシーの要件](#bkmk_top)  
  
##  <a name="configure-stored-credentials-for-a-report-specific-data-source-sharepoint-mode"></a><a name="bkmk_stored_credentials_data_source_sharepoint"></a> レポート固有のデータ ソース用の保存された資格情報を構成する (SharePoint モード)  
  
1.  レポートを含むドキュメント ライブラリを参照し、開くメニューをクリックします![ssrs 項目のドキュメント ライブラリのコンテキスト メニュー](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "ssrs 項目のドキュメント ライブラリのコンテキスト メニュー")。  
  
2.  2 番目の開くメニューをクリックし![ssrs 項目のドキュメント ライブラリのコンテキスト メニュー](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "ssrs 項目のドキュメント ライブラリのコンテキスト メニュー")、 **[データ ソースの管理]** をクリックします。  
  
3.  資格情報を使用して構成する **[カスタム]** データ ソースの名前をクリックします。  
  
4.  **[データ ソースの種類]** の一覧で、データ ソースから取得したデータの処理に使用するデータ処理拡張機能を選択します。  
  
5.  **[接続文字列]** でレポート サーバーがデータ ソースへの接続に使用する接続文字列を指定します。 以下に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースへの接続に使用する接続文字列の例を示します。  
  
    ```  
    data source=<servername>;initial catalog=AdventureWorks2012  
    ```  
  
6.  **[資格情報]** で、 **[格納された資格情報]** を選択します。  
  
7.  **[ユーザー名]** と **[パスワード]** を入力します。  
  
    -   このアカウントが Windows ドメイン ユーザー アカウントである場合は、\<domain>\\<account\> という形式で指定し、 **[データ ソースへの接続時に Windows 資格情報として使用する]** チェック ボックスをオンにします。  
  
    -   ユーザー名とパスワードがデータベースの資格情報である場合は、 **[Windows 資格情報として使用する]** を選択しないでください。 データベース サーバーが権限の借用または委譲をサポートしている場合は、 **[実行コンテキストをこのアカウントに設定する]** を選択できます。  
  
8.  **[OK]** をクリックします。  
  
     ![[トップに戻る] リンクで使用される矢印アイコン](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン") [保存された資格情報のセキュリティ ポリシーの要件](#bkmk_top)  
  
##  <a name="configure-stored-credentials-for-a-shared-data-source-native-mode"></a><a name="bkmk_stored_credentials_shared_data_source_native"></a> 共有データ ソース用の保存された資格情報を構成する (ネイティブ モード)  
  
1.  Web ポータルで、共有データ ソース アイテムを参照します。 
  
2.  レポート タイルの右上隅にある省略記号 (...)、 **[管理]** の順にクリックします。 
  
3.  **[種類]** リストで、データ ソースから取得したデータの処理に使用するデータ処理拡張機能を指定します。  
  
4.  **[接続文字列]** でレポート サーバーがデータ ソースへの接続に使用する接続文字列を指定します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、接続文字列に資格情報を指定しないことをお勧めします。  
  
     以下に、ローカルの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースへの接続に使用する接続文字列の例を示します。  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
5.  ユーザー名とパスワードを入力します。  
  
    -   このアカウントが Windows ドメイン ユーザー アカウントである場合は、\<domain>\\<account\> という形式で指定し、 **[データ ソースへの接続時に Windows 資格情報として使用する]** チェック ボックスをオンにします。  
  
    -   ユーザー名とパスワードがデータベースの資格情報である場合は、 **[データ ソースへの接続時に Windows 資格情報として使用する]** を選択しないでください。 データベース サーバーが権限の借用または委譲をサポートしている場合は、 **[データ ソースへの接続が確立した後に、認証されているユーザーの権限を借用する]** を選択できます。  
  
6.  **[Apply]** をクリックします。  
  
     ![[トップに戻る] リンクで使用される矢印アイコン](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン") [保存された資格情報のセキュリティ ポリシーの要件](#bkmk_top)  
  
##  <a name="configure-stored-credentials-for-a-shared-data-source-sharepoint-mode"></a><a name="bkmk_stored_credentials_shared_data_source_sharepoint"></a> 共有データ ソース用の保存された資格情報を構成する (SharePoint モード)  
  
1.  ドキュメント ライブラリで、共有データ ソース項目を参照します。![共有データ ソースのアイコン](../../reporting-services/report-data/media/hlp-16datasource.png "共有データ ソースのアイコン")  
  
2.  コンテキスト メニューをクリックし![ssrs 項目のドキュメント ライブラリのコンテキスト メニュー](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "ssrs 項目のドキュメント ライブラリのコンテキスト メニュー")、2 番目のコンテキスト メニューをクリックします![ssrs 項目のドキュメント ライブラリのコンテキスト メニュー](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "ssrs 項目のドキュメント ライブラリのコンテキスト メニュー")。  
  
3.  **[データ ソース定義の編集]** をクリックします。  
  
4.  **[データ ソースの種類]** の一覧で、データ ソースから取得したデータの処理に使用するデータ処理拡張機能を指定します。  
  
5.  **[接続文字列]** でレポート サーバーがデータ ソースへの接続に使用する接続文字列を指定します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、接続文字列に資格情報を指定しないことをお勧めします。  
  
     以下に、ローカルの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースへの接続に使用する接続文字列の例を示します。  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
6.  ユーザー名とパスワードを入力します。  
  
    -   このアカウントが Windows ドメイン ユーザー アカウントである場合は、\<domain>\\<account\> という形式で指定し、 **[Windows 資格情報として使用する]** を選択します。  
  
    -   ユーザー名とパスワードがデータベースの資格情報である場合は、 **[Windows 資格情報として使用する]** を選択しないでください。 データベース サーバーが権限の借用または委譲をサポートしている場合は、 **[実行コンテキストをこのアカウントに設定する]** を選択できます。  
  
7.  **[OK]** をクリックします。  
  
     ![[トップに戻る] リンクで使用される矢印アイコン](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン") [保存された資格情報のセキュリティ ポリシーの要件](#bkmk_top)  
  
## <a name="see-also"></a>参照  
 [レポート データ ソースに関する資格情報と接続情報を指定する](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
