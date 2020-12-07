---
description: ネイティブ モードのレポート サーバーに対するアクセス許可の付与
title: ネイティブ モードのレポート サーバーに対するアクセス許可の付与 | Microsoft Docs
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- roles [Reporting Services], creating
- authorization [Reporting Services]
- server security [Reporting Services]
- role-based security [Reporting Services]
- items [Reporting Services], security
- permissions [Reporting Services], native mode
- published reports [Reporting Services], security
- reports [Reporting Services], security
- report items [Reporting Services], security
- role-based security [Reporting Services], about role-based security
- security [Reporting Services], role-based
ms.assetid: 260dc2e9-546c-4f04-9fa1-977e23c9d68c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 82fba1144cdb970d97b8aac4938fd7c3e8fe0980
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88373298"
---
# <a name="grant-permissions-on-a-native-mode-report-server"></a>ネイティブ モードのレポート サーバーに対するアクセス許可の付与
  SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、ロールベースの承認および認証サブシステムを使用して、操作の実行およびレポート サーバーのアイテムへのアクセスを行えるユーザーを決定します。 ロールベースの承認では、ユーザーまたはグループが実行できる一連のアクションがロールに分類されます。 認証は、組み込みの Windows 認証、または指定したカスタム認証モジュールに基づいて行われます。 どちらの種類の認証でも、定義済みロールまたはカスタム ロールを使用できます。
  
## <a name="use-roles-to-grant-report-server-access"></a>ロールを使用したレポート サーバーへのアクセス許可
 すべてのユーザーは、特定のレベルのアクセスを定義するロールのコンテキスト内でレポート サーバーと対話します。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、レポート サーバーにすぐにアクセスできるように、ユーザーおよびグループに割り当てることのできる定義済みロールが含まれています。 **コンテンツ マネージャー**、**パブリッシャー**、および**閲覧者**は、定義済みロールの例です。 各ロールでは、関連するタスクのコレクションを定義します。 たとえば、 **パブリッシャー** には、レポートを追加して、そのレポートを格納するフォルダーを作成する権限があります。
  
 通常、ロールの割り当ては親ノードから継承されますが、特定のアイテムに対する新しいロールの割り当てを作成することで権限の継承を無効にすることができます。 あるレポートの**コンテンツ マネージャー** ロールのメンバーであるユーザーは、別のレポートの**閲覧者**ロールのメンバーである可能性があります。
  
 レポート サーバーのアイテムと操作へのアクセスを許可するには:
  
1. 定義済みロールを確認して、これらのロールをそのまま使用できるかどうかを判断します。 タスクを調整したり追加のロールを定義したりする必要がある場合は、ユーザーを特定のロールに割り当てる前に、これらの処理を行います。 各ロールの詳細については、[定義済みロール](../../reporting-services/security/role-definitions-predefined-roles.md)に関するページを参照してください。
  
1. レポート サーバーへのアクセス権を必要とするユーザーやグループ、およびそのレベルを特定します。 多くのユーザーを**閲覧者**ロールまたは**レポート ビルダー** ロールに割り当てます。 **パブリッシャー** ロールには、少数のユーザーを割り当てます。 **コンテンツ マネージャー** ロールには、数人のユーザーのみを割り当てます。
  
1. Web ポータルを使用して、アクセスを必要とする各ユーザーまたはグループのホーム フォルダーにロールを割り当てます。 ホーム フォルダーは、レポート サーバーのフォルダー階層で最上位レベルのフォルダーです。
  
1. サイト レベルでは、Web ポータルの **[サイトの設定]** ページで、 **[システム ユーザー]** および **[システム管理者]** という定義済みロールを使用して、各ユーザーまたはグループにシステムレベルのロールの割り当てを作成します。
  
1. 特定のフォルダー、レポートなどのアイテムに対し、必要に応じて、追加のロールの割り当てを作成します。 ロールの割り当てを作成しすぎないようにします。 多く作成しすぎると、各ユーザーの権限レベルが多岐にわたり、追跡が困難になります。
  
> [!NOTE]  
>  SharePoint 統合モードで実行するようにレポート サーバーを構成した場合、SharePoint サイトに対する権限を、レポート サーバー アイテムへのアクセスを許可するように設定する必要があります。 詳細については、「[SharePoint サイトのレポート サーバー アイテムに対する権限の付与](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)」を参照してください。
> 
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。
  
## <a name="who-sets-permissions"></a>権限の設定者
 初期状態では、レポート サーバーにアクセスできるのは、ローカルの Administrators グループのメンバーであるユーザーだけです。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] は、ローカルの Administrators グループのメンバーにアイテムレベルおよびシステムレベルのアクセスを許可する 2 つの既定のロールの割り当てと共にインストールされます。 ローカルの Administrators は、このような組み込みのロールの割り当てを使用して、他のユーザーにレポート サーバーへのアクセスを許可したり、レポート サーバー アイテムを管理したりできます。 組み込みのロールの割り当ては削除できません。 ローカル管理者は、常に、レポート サーバー インスタンスを完全に管理する権限が与えられています。
 
 Windows Vista または Windows Server 2008 を実行しているローカル コンピューター上のレポート サーバー インスタンスを管理するには、追加の構成が必要となります。 詳細については、「[ローカル管理用のネイティブ モードのレポート サーバー &#40;SSRS&#41; の構成](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)」を参照してください。
  
## <a name="how-permissions-are-stored"></a>権限が格納されるしくみ
 ロールの割り当てと定義はレポート サーバー データベースに格納されます。 さまざまなクライアント ツールやプログラム インターフェイスを使用している場合、すべてのアクセスは、レポート サーバー インスタンス全体を対象として定義されている権限に従います。 スケールアウト配置で複数のレポート サーバーを構成する場合、あるインスタンスで定義したロールの割り当ては共有データベースに格納され、同じスケールアウト配置内のその他すべてのインスタンスで使用されます。 ロールの割り当てはセキュリティで保護されているアイテムと共に格納されるので、定義した権限を維持したまま、データベースを別のレポート サーバーに移動することができます。
  
## <a name="tasks-and-tools-for-managing-permissions"></a>権限を管理するためのタスクとツール
 ロールの定義と割り当てを管理するには、次のツールを使用します。
  
|ツール|タスク|  
|----------|-----------|  
|Management Studio: ロールの定義を表示、変更、作成、および削除する場合に使用します|[ロールを作成、削除、または変更する &#40;Management Studio&#41;](../../reporting-services/security/role-definitions-create-delete-or-modify.md)|  
|Web ポータル: ロールにユーザーとグループを割り当てる場合に使用します|[レポート サーバーへのユーザー アクセスを許可する](../../reporting-services/security/grant-user-access-to-a-report-server.md)<br /><br /> [ロールの割り当てを変更または削除する](../../reporting-services/security/role-assignments-modify-or-delete.md)|  
  
## <a name="see-also"></a>関連項目
 - [定義済みロール](../../reporting-services/security/role-definitions-predefined-roles.md)  
 - [SharePoint サイトのレポート サーバー アイテムに対する権限の付与](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
 - [レポート サーバーでの認証](../../reporting-services/security/authentication-with-the-report-server.md)  
 - [ロールの割り当ての作成と管理](../../reporting-services/security/create-and-manage-role-assignments.md)  
 - [Reporting Services のセキュリティと保護](../../reporting-services/security/reporting-services-security-and-protection.md)  
 - [レポート サーバー コンテンツの管理 &#40;SSRS ネイティブ モード&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)  
  
  
