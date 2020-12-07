---
description: 個人用レポートをセキュリティで保護する
title: 個人用レポートをセキュリティで保護する | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- denying My Reports folder access
- private folders [Reporting Services]
- user workspace [Reporting Services]
- security [Reporting Services], My Reports folder
- My Reports folder [Reporting Services]
ms.assetid: 3b23a382-13b8-4196-9a93-7fe62d03a63c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: aba081c02ca027a861ab6c7680e038bac7a18304
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498045"
---
# <a name="secure-my-reports"></a>個人用レポートをセキュリティで保護する
  個人用レポート機能により、ユーザーが管理するレポート処理用のワークスペースが提供されます。 [個人用レポート] フォルダーは、その性質上、他の汎用的な用途のフォルダーよりも権限の制限を緩める必要があります。 他のフォルダーのレポートを表示および実行する権限しか持たないユーザーが、[個人用レポート] フォルダーおよび自らが所有するコンテンツを管理するためには、より強い権限が必要となります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、そのための特別なロールの割り当てとロールの定義が用意されています。  
  
> [!NOTE]
>  個人用レポートはレポート マネージャーでのみ使用できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]では使用できません。  
  
## <a name="role-assignment-for-my-reports"></a>個人用レポートのロールの割り当て  
 個人用レポートのロールの割り当てには、あらかじめ要素が定義されています。[個人用レポート] フォルダーがアクティブになっている各ユーザーには、この割り当てが自動的に作成されます。 レポート サーバーから自動的にセキュリティを割り当てられるので、管理者が個人用レポートのユーザー 1 人ずつのアクセス権を有効にする必要がなくなります。したがって、個人用レポートを広く使用する組織にとっては、この手法が非常に有効です。  
  
 **個人用レポート** ロールの割り当ては、次の要素で構成されています。  
  
-   Users フォルダー\\ *\<username>* \個人用レポート フォルダーにある、ユーザーの [個人用レポート] フォルダー。  
  
-   [個人用レポート] フォルダーをアクティブ化するときに判別されたユーザー アカウント。 フォルダーがアクティブ化されるのは、ユーザーがレポート マネージャーの [個人用レポート] フォルダーをクリックするか、レポート デザイナーから [個人用レポート] フォルダーにレポートをパブリッシュしたときです。 ユーザーが [個人用レポート] リンクでプロパティを要求する場合も、このフォルダーはアクティブ化されます。  
  
-   個人用レポートの定義済みロールの定義。  
  
## <a name="role-definition-for-my-reports"></a>個人用レポートのロールの定義  
 個人用レポート ロールの定義には、 **[個人用レポート]** フォルダーのコンテンツ管理をサポートするタスクが含まれています。 **個人用レポート** ロールは、専用の目的を持ったロールとして使用することを想定しています。 個人用レポート ロールはどのアイテムレベルのセキュリティ ポリシーに対しても選択できます。ただし、このロールの多用は避け、できるだけ他のフォルダー要件に合わせてこのロールを変更しないようにしてください。 個人用レポート機能に **個人用レポート** ロールを予約しておくことで、ユーザー間の使用環境を統一することができます。  
  
 既定では、レポート サーバー管理者のみが **個人用レポート** ロールを変更します。 **個人用レポート** ロールに含まれるタスクを変更することで、このロールをカスタマイズできます。 また、別のロールに置き換えることもできます。  
  
## <a name="denying-access-to-my-reports"></a>個人用レポートへのアクセス拒否  
 ユーザーによる個人用レポートへのアクセスを拒否するには、次の方法を使用します。  
  
-   [サイトの設定] ページで個人用レポートを無効にします。 詳細については、 [「個人用レポートの有効化と無効化」](../../reporting-services/report-server/enable-and-disable-my-reports.md)を参照してください。  
  
-   **個人用レポート** ロールからすべてのタスクを削除します。  
  
 個人用レポートを無効にすると、[個人用レポート] フォルダーのリンクがレポート マネージャーから削除されます。 個人用レポートをサポートする基本のフォルダー構造 (つまり Users フォルダーとサブフォルダー) は有効なままなので、ユーザーはフォルダーのパスがわかればアクセスすることができます。 **個人用レポート** ロールからタスクを削除すると、アクセスが拒否されます。  
  
## <a name="see-also"></a>参照  
 [レポートとリソースの保護](../../reporting-services/security/secure-reports-and-resources.md)   
 [フォルダーをセキュリティで保護する](../../reporting-services/security/secure-folders.md)   
 [ネイティブ モードのレポート サーバーに対する権限の許可](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
