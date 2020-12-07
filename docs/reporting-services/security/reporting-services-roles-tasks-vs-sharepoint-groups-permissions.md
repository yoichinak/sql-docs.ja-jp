---
description: SQL Server Reporting Services と SharePoint グループのアクセス許可
title: SQL Server Reporting Services と SharePoint グループのアクセス許可 | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- security [Reporting Services], tasks
- roles [Reporting Services], predefined
- SharePoint integration [Reporting Services], permissions
- permissions [Reporting Services], native mode
- security [Reporting Services], predefined roles
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 429f1dbb-183a-4097-bd1b-693da9fe7a36
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2abd5aa8f15a0213a8eccee0965688cf626abc02
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988148"
---
# <a name="reporting-services-roles-tasks-vs-sharepoint-groups-permissions"></a>SQL Server Reporting Services と SharePoint グループのアクセス許可
  このトピックでは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モードのロール ベースおよびタスク ベースの承認機能を、SharePoint 製品のセキュリティ機能と比較します。 このトピックでは、ロール、タスク、SharePoint グループ、権限レベル、および権限の用語と特徴を比較します。  
  
[!INCLUDE[applies](../../includes/applies-md.md)]

:::row:::
    :::column:::
        [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モード  
          SharePoint 2010 および SharePoint 2013  
    :::column-end:::
    :::column:::
        [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード  
    :::column-end:::
:::row-end:::



  
 **このトピックの内容:**  
  
-   [権限ツールと用語の比較](#bkmk_compare_tools_terms)  
  
-   [ネイティブ モードと SharePoint グループの比較](#bkmk_compare_roles_groups)  
  
-   [ネイティブ モード タスクと SharePoint の権限の比較](#bkmk_compare_tasks_permissions)  
  
##  <a name="compare-permission-tools-and-terminology"></a><a name="bkmk_compare_tools_terms"></a> 権限ツールと用語の比較  
 **ネイティブ モード:**[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モードの権限オブジェクト (ロールおよびタスク) は、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 内で作成し、レポート マネージャー内で個々のユーザーに対して構成します。  
  
 **SharePoint モード:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モードでは、SharePoint の権限の機能を活用します。 SharePoint のグループと権限は、次の **[サイトの設定]** ページで管理します。  
  
 次の表では、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モードと SharePoint の間で、権限に関連するオブジェクトと概念を比較します。  
  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード|SharePoint|  
|---------------------------------------------|----------------|  
|**役割:** たとえば、"コンテンツ マネージャー"。|**グループ:** たとえば、既定の "閲覧者" グループ。|  
|---|**権限レベルのグループ:** たとえば、"閲覧者" グループに対応する "表示のみ"。|  
|**タスク:** たとえば、"レポートの管理"。|**権限:** たとえば、"表示のみ" グループ内には、アイテムの表示、バージョンの表示、アプリケーション ページの表示の一覧に関連する権限があります。|  
  
 SharePoint の権限の詳細については、「 [アクセス許可レベルと権限](https://support.office.com/article/Understand-groups-and-permissions-on-a-SharePoint-site-258E5F33-1B5A-4766-A503-D86655CF950D) 」、および「 [アクセス許可レベルおよびグループを決定する (SharePoint 2013)](/SharePoint/sites/determine-permission-levels-and-groups-in-sharepoint-server)」を参照してください。  
  
##  <a name="compare-native-mode-roles-and-sharepoint-groups"></a><a name="bkmk_compare_roles_groups"></a> ネイティブ モードと SharePoint グループの比較  
 次の表では、ネイティブ モードの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] で事前定義されているロールの定義と、標準の SharePoint グループとを比較しています。 SharePoint のグループが目的のロールと一致しない場合は、SharePoint でカスタム グループを作成し、権限レベルを割り当てることができます。  
  
 **注**: 使用できる既定の SharePoint グループは、SharePoint サイトの作成に使用されたサイト テンプレートによって異なります。  
  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ロール|SharePoint グループ|  
|--------------------------------------|-----------------------|  
|**ブラウザー**<br /><br /> View|レポートを表示する権限を許可するには、 **閲覧者** グループを使用します。 **閲覧者** グループには読み取りレベルの権限が与えられます。グループ メンバーは、ページ、リスト アイテム、およびドキュメントを表示できます。|  
|**コンテンツ マネージャー**<br /><br /> セキュリティを設定する権限を含めて、あらゆるアイテムおよびアイテムレベルの操作に対する完全な権限。|SharePoint サイト上のレポート サーバー アイテムに対するフル コントロールを許可するには、 **所有者** グループを使用します。 **所有者** グループにはフル コントロール権限が与えられるので、グループ メンバーは、サイトのコンテンツ、ページ、または機能に変更を加えることができます。 フル コントロールのアクセスは、サイト管理者のみに制限する必要があります。|  
|**個人用レポート**|これに相当するグループはありません。 **個人用レポート** は、SharePoint モードで動作するレポート サーバーではサポートされません。 同等の機能が必要な場合は、 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] で個人用サイト機能を使用できます。|  
|**発行元**<br /><br /> レポート、レポート モデル、共有データ ソース、およびリソースの追加、更新、表示、および削除を行います。|アイテムの追加と編集、および SharePoint サイト上の依存アイテムへの参照の更新を行う権限を許可するには、 **メンバー** グループを使用します。 **メンバー** グループには投稿レベルの権限が与えられます。グループ メンバーは、ページを表示してアイテムの追加または更新を行った後に、変更内容を送信して承認を求めることができます。|  
|**レポート ビルダー**<br /><br /> レポートを表示し、個々のサブスクリプションを自己管理し、レポート ビルダーでレポートを開きます。|レポート ビルダーのレポート定義に相当するような定義済みの権限レベルまたは SharePoint グループはありません。 既定では、 **メンバー** グループまたは **所有者** グループに属するユーザーには、レポート ビルダーを使用する権限があります。 もっと多くのユーザーがレポート ビルダーを使用できるようにするには、レポート ビルダー ロールと同等の権限レベルが提供されるカスタム セキュリティ設定を作成する必要があります。 詳細については、「 [SharePoint サイト上のレポート サーバー アイテムに対する権限の設定 (Reporting Services の SharePoint 統合モード)](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)」を参照してください。|  
|-|表示されたレポートを閲覧する権限を許可するには、 **閲覧者** グループを使用します。 **閲覧者** グループは、レポート アイテムのコンテンツをダウンロードすることも表示することもできません。<br /><br /> **注:** SQL Server 2012 以降の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]では、 **閲覧者** グループには、サブスクリプションを作成する権限がなくなりました。|  
|**システム ユーザー** および **システム管理者**|これらのロールは、SharePoint モードで動作するレポート サーバーでは必要ありません。 **システム ユーザー** と **システム管理者** は、SharePoint ファーム レベルまたは Web アプリケーション レベルの権限に対応します。 レポート サーバーでは、これらのレベルでの承認が必要となる機能が提供されません。|  
  
##  <a name="comparing-native-mode-tasks-and-sharepoint-permissions"></a><a name="bkmk_compare_tasks_permissions"></a> ネイティブ モード タスクと SharePoint の権限の比較  
 次の表は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モードのタスクと SharePoint の権限との対応関係を示しています。 **[種類]** 列では、ネイティブ モードのタスクが、システム ロールと、標準的なロールおよびアイテムのどちらに関連しているかを示します。 システム ロールは、システム レベルの権限、たとえば共有スケジュールを管理します。  
  
|ネイティブ モードのタスク|ロールの種類|同等の SharePoint の権限|  
|----------------------|---------------|--------------------------------------|  
|レポートの使用|項目|アイテムの編集、アイテムの表示。|  
|リンク レポートの作成|項目|サポートされていません。|  
|すべてのサブスクリプションを管理|項目|アラートの管理。|  
|データ ソースを管理する|項目|アイテムの追加、アイテムの編集、アイテムの削除、アイテムの表示。|  
|フォルダーの管理|項目|アイテムの追加、アイテムの編集、アイテムの削除、アイテムの表示。|  
|個別のサブスクリプションを管理|項目|アイテムの編集<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]より前のバージョンでは、必要な権限レベルは "通知の作成" でした。|  
|モデルを管理する|項目|アイテムの追加、アイテムの編集、アイテムの削除、アイテムの表示。|  
|レポート履歴の管理|項目|アイテムの編集、バージョンの表示、バージョンの削除。|  
|レポートの管理|項目|アイテムの追加、アイテムの編集、アイテムの削除、アイテムの表示。|  
|リソースの管理|項目|アイテムの追加、アイテムの編集、アイテムの削除、アイテムの表示。|  
|アイテムごとにセキュリティを設定|項目|アクセス許可の管理|  
|データ ソースの表示|項目|アイテムの表示。|  
|フォルダーの表示|項目|アイテムの表示。|  
|モデルの表示|項目|アイテムの表示。|  
|レポートの表示|項目|アイテムの表示。|  
|リソースの表示|項目|アイテムの表示。|  
||||  
|レポート定義の実行|システム|アイテムの表示。|  
|イベントの生成|システム|Web サイトの管理。|  
|ジョブの管理|システム|なし (サポートされていません)。|  
|レポート サーバーのプロパティを管理|システム|なし (該当しません)。 レポート サーバーでは、サーバーの全体管理で統合設定を表示する権限をユーザーに与えるかどうかは制御されません。|  
|ロールの管理|システム|権限の管理。|  
|共有スケジュールの管理|システム|Web サイトの管理、開く。|  
|レポート サーバーのセキュリティを管理|システム|なし (該当しません)。 レポート サーバーでは、SharePoint 統合モードで動作するサーバー上ではシステムレベルのロール割り当てが使用されません。|  
|レポート サーバーのプロパティを表示|システム|なし (該当しません)。 レポート サーバーでは、サーバーの全体管理で統合設定を表示する権限をユーザーに与えるかどうかは制御されません。|  
|共有スケジュールの表示|システム|アイテムを開きます。|  
  
## <a name="see-also"></a>参照  
 [SharePoint サイト上のレポート サーバー アイテムに対する権限の設定 (Reporting Services の SharePoint 統合モード)](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [SharePoint Web アプリケーションのレポート サーバー操作に対するアクセス許可を設定する](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [SharePoint サイトのレポート サーバー アイテムに対する権限の付与](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [ロールの定義](../../reporting-services/security/role-definitions.md)   
 [定義済みロール](../../reporting-services/security/role-definitions-predefined-roles.md)  
  
