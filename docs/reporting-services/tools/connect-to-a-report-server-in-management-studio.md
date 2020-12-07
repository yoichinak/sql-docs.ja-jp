---
title: Management Studio でレポート サーバーに接続する | Microsoft Docs
description: SQL Server Management Studio のオブジェクト エクスプローラーを使用して、SQL Server ファミリの任意のサーバーに接続し、その内容をグラフィカルに表示する方法について学習します。
ms.date: 05/07/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.connecttors.connectionproperties.f1
- sql13.swb.connecttors.login.f1
- sql13.swb.connection.login.reportserver.f1
helpviewer_keywords:
- report servers [Reporting Services], connections
- connections [Reporting Services], report server
- registering report servers
- report servers [Reporting Services], registering
- Connect to Server dialog box, Reporting Services
ms.assetid: c875ff87-ee7d-443a-a702-bdb4b6c27c6e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 027d3bb67c087f119c3848a2d81ac0875b138db3
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91934852"
---
# <a name="connect-to-a-report-server-in-management-studio"></a>Management Studio でレポート サーバーに接続する

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] のオブジェクト エクスプローラーでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ファミリのあらゆるサーバーに接続して、その内容をグラフィカルに表示できます。 Reporting Services については、オブジェクト エクスプローラーを使用して、次のタスクを実行できます。

- レポート サーバーの機能を有効にする。

- サーバーの既定値を設定し、ロールの定義を構成する。

- 実行中のジョブを管理する。

- ジョブ スケジュールを管理する。

 ネイティブ モードのレポート サーバーまたは SharePoint 統合モードで実行されているレポート サーバーに接続できます。 接続構文および実行できる操作の種類は、レポート サーバーのサーバー モードとユーザーの権限によって異なります。 レポート サーバーに接続できない場合または特定のタスクの実行で問題が発生した場合は、権限が不足しているか、レポート サーバー名を正しく指定していない可能性があります。 権限および接続構文の詳細については、この記事の最後に掲載された表を参照してください。

 オブジェクト エクスプローラーを使用してレポート サーバーのコンテンツを表示したり管理したりすることはできません。 コンテンツ管理は、レポート サーバーがネイティブ モードで動作している場合は Web ポータルを使用し、レポート サーバーが SharePoint 統合モードで動作している場合は SharePoint サイトを使用して実行します。

 オブジェクト エクスプローラーでは、同じサーバー グループに登録された複数のサーバー インスタンスへの接続を同じワークスペースで開くことができます。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でレポート サーバー インスタンスに接続するには、そのサーバーが登録されている必要があります。 既にレポート サーバーが登録されている場合は、この手順をスキップできます。 レポート サーバーを登録する手順については、この記事の最後に説明します。

### <a name="to-connect-to-a-native-mode-report-server"></a>ネイティブ モードのレポート サーバーに接続するには

1. まだオブジェクト エクスプローラーを開いていない場合は、 **[表示]** メニューから選択します。

2. **[接続]** を選択してサーバーの種類を一覧表示し、 **[Reporting Services]** を選択します。

3. **[サーバーへの接続]** ダイアログ ボックスに、レポート サーバー インスタンスの名前を入力します。 レポート サーバー インスタンスの名前は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前に基づいています。 既定では、ローカル レポート サーバー インスタンスのインスタンス名はコンピューター名です。 レポート サーバーを名前付きインスタンスとしてインストールした場合は、次の構文を使用してサーバーを指定します: *\<servername>[\\<instancename\>]* 。

4. **[認証の種類]** を選択します。 Windows 認証を使用している場合は、資格情報を使用して接続します。 基本認証またはフォーム認証を選択した場合は、アカウントおよびパスワードを入力します。  
  
5. **[接続]** を選択します。 レポート サーバーがオブジェクト エクスプローラーに表示されます。  

6. サーバー ノードを右クリックし、システムのプロパティおよびサーバーの既定値を設定します。 詳細については、「[レポート サーバーのプロパティを設定する &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)」を参照してください。

### <a name="to-connect-to-a-sharepoint-integrated-mode-report-server"></a>SharePoint 統合モードのレポート サーバーに接続するには  

1. まだオブジェクト エクスプローラーを開いていない場合は、 **[表示]** メニューから選択します。

2. **[接続]** を選択してサーバーの種類を一覧表示し、 **[Reporting Services]** を選択します。

3. **[サーバーへの接続]** ダイアログ ボックスに、SharePoint サイトへの URL を入力します。 構文例を次に示します。`https://<web server>/sites/<site>`

4. **[認証の種類]** を選択します。 Windows 認証を使用している場合は、資格情報を使用して接続する必要があります。 基本認証またはフォーム認証を選択した場合は、アカウントおよびパスワードを入力します。

5. **[接続]** を選択します。 レポート サーバーがオブジェクト エクスプローラーに表示されます。

6. サーバー ノードを右クリックし、システムのプロパティおよびサーバーの既定値を設定します。 詳細については、「[レポート サーバーのプロパティを設定する &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)」を参照してください。

### <a name="to-register-a-report-server"></a>レポート サーバーを登録するには

1. レポート サーバーに接続できない場合は、それへのアクセス権がないか、サーバーが登録されていません。 サーバーを登録するには、 **[表示]** メニュー、 **[登録済みサーバー]** の順に選択します。

2. **Reporting Services** アイコンを選択します。

3. **[Reporting Services]** を右クリックし、 **[新規作成]**  >  **[サーバーの登録]** をクリックします。 **[新規サーバーの登録]** ダイアログ ボックスが表示されます。

4. **[サーバー名]** に値を入力します。 サーバーのモードに応じて値を指定します。

    - ネイティブ モードのレポート サーバーでは、レポート サーバー インスタンスの名前を入力します。 レポート サーバー インスタンスの名前は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前に基づいています。 既定では、ローカル レポート サーバー インスタンスのインスタンス名はコンピューター名です。 レポート サーバーを名前付きインスタンスとしてインストールした場合は、次の構文を使用してサーバーを指定します: *\<servername>[\\<instancename\>]* 。

    - SharePoint 統合モードで動作するレポート サーバーの場合、接続先のサーバーは、レポート サーバーが接続されている SharePoint サイトです。 権限レベルを表示できるように、SharePoint サイトに接続します。 権限によって、レポート サーバーのコンテンツに対するアクセスと操作を制御します。 サイト コレクション内の任意のサイトを指定できます。 構文例を次に示します。`https://mysharepointsite`

5. **[認証]** では、レポート サーバーで既に使用している認証モードを選択します。

   - 既定のセキュリティを使用している場合は、 **[Windows 認証]** を選択します。
   - カスタム セキュリティ拡張機能をインストールして配置した場合は、 **[フォーム認証]** を選択します。
   - 基本認証を使用するようにレポート サーバーを構成した場合は、 **[基本認証]** を選択します。
   - レポート サーバーが SharePoint 統合モード用に構成されている場合は、 **[Windows 認証]** を選択します。

6. **[テスト]** を選択すると、接続が検証されます。

7. メッセージが表示されたら、 **[OK]** 、 **[保存]** の順に選択します。

## <a name="connection-syntax-and-permissions"></a>接続構文と権限

 次の表は、特定のタスクを実行するために必要な接続構文、手順、および権限をまとめたものです。

 [サーバーの種類] として [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を指定した場合、 **[サーバーへの接続]** ダイアログ ボックスには、レポート サーバーの名前または Web サービスのエンドポイントを指定できます。

|接続先|   タスク   |   アクセス許可   |
|----------|-----------|-----------------|  
|ネイティブ モードのレポート サーバー (既定のインスタンスまたは名前付きインスタンスとして接続)<br /><br /> \<server name>\<_instance><br /><br /> レポート サーバーへの接続は、レポート サーバー WMI プロバイダーを介して行われます。|サーバーのプロパティと既定値を表示および設定する。<br /><br /> ジョブを表示および取り消す。<br /><br /> 共有スケジュールを作成および管理する。<br /><br /> ロール定義を作成、変更、または削除する。|システム管理者ロールへの割り当て。|  
|ネイティブ モードのレポート サーバー (レポート サーバー Web サービスへのエンドポイントを介し、既定のインスタンスまたは名前付きインスタンスとして接続)<br /><br /> `https://<servername>/reportserver`<br /><br /> レポート サーバーの URL を指定することによって、レポート サーバーに接続することもできます。|サーバーのプロパティと既定値を表示および設定する。<br /><br /> ジョブを表示および取り消す。<br /><br /> 共有スケジュールを作成および管理する。<br /><br /> ロール定義を作成、変更、または削除する。|システム管理者ロールへの割り当て。|  
|SharePoint 統合モードのレポート サーバー (SharePoint サイトを介して接続)<br /><br /> `https://<webserver>/<SharePointSite>`|サーバーのプロパティと既定値を表示および設定する。<br /><br /> ジョブを表示および取り消す。<br /><br /> 接続先のサイトに定義される共有スケジュールを作成および管理する。<br /><br /> 接続先のサイトに定義された権限レベルを表示する。|接続先の SharePoint サイトに対するフル コントロール レベルの権限。|
|SharePoint 統合モードのレポート サーバー (レポート サーバー インスタンスの名前を介して接続)<br /><br /> \<server name>\<_instance>|サーバーのプロパティと既定値を表示および設定する。<br /><br /> ジョブを表示および取り消す。|レポート サーバーと統合された SharePoint サイトに対するフル コントロール レベルの権限。<br /><br /> SharePoint サイトに接続せずに、レポート サーバーに接続した場合は、実行できるタスクの数が減っている点に注意してください。 この理由は、レポート サーバーが、レポート サーバー データベースで保存または管理されたアプリケーション データのみ返すことができ、SharePoint の構成データベースとコンテンツ データベースに格納されたデータを返すことはできないためです。|

## <a name="see-also"></a>関連項目

 [レポート サーバー データベース接続の構成 (レポート サーバー構成マネージャー)](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
 [SQL Server Management Studio の Reporting Services &#40;SSRS&#41;](../../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)
