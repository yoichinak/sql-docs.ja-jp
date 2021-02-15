---
description: タスクおよびアクセス許可 - アイテム レベルのタスク
title: アイテム レベルのタスク | Microsoft Docs
ms.date: 02/04/2021
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- item-level tasks [Reporting Services]
ms.assetid: fdeb7bc3-167a-4342-84e3-32e3faa1fa39
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 82101577abe86914aff2ac1d5296d7dc176a60b0
ms.sourcegitcommit: 6f4fb9cfd0cad06127a6328adc745e2ba7c191d1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/05/2021
ms.locfileid: "99570436"
---
# <a name="tasks-and-permissions---item-level-tasks"></a>タスクおよびアクセス許可 - アイテム レベルのタスク
  
  [!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]
  
  アイテムレベルのタスクとは、レポート、フォルダー、レポート モデル、リソース、共有データ ソースに関連する権限を集めたものです [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、レポート サーバー サイト全体に適用されるシステムレベル タスクもあります。 詳細については、「 [システムレベルのタスク](../../reporting-services/security/tasks-and-permissions-system-level-tasks.md)」を参照してください。 一般的なタスクおよび権限の詳細については、「 [タスクと権限](../../reporting-services/security/tasks-and-permissions.md)」を参照してください。  
  
> [!NOTE]  
>  プログラムでこれらのタスクを使用して処理を実行している場合、アイテムレベルのタスクをサポートしているメソッドを使用する必要があります。 詳細については、次のトピックを参照してください。 <xref:ReportService2010.ReportingService2010.ListTasks%2A> および <xref:ReportService2010.ReportingService2010.ListRoles%2A>  
  
## <a name="permissions-in-item-level-tasks"></a>アイテムレベルのタスクの権限  
 次の表ではアイテムレベルのタスクを一覧表示し、各タスクに含まれる権限および権限が適用されるアイテムを示します。 権限の一覧は、タスクごとに利用できる機能をより詳細に示すためにのみ記載されています。  
  
 共有データセットは、レポートと同じ一連の権限を使用します。 レポート パーツは、リソースと同じ一連の権限を使用します。  
  
|タスク|適用される項目|アクセス許可|  
|----------|---------------------|-----------------|  
|レポートにコメントを付ける<br />(SSRS 2017 以降、Power BI Report Server)|レポート|プロパティの読み取り<br /><br /> コメントの作成<br /><br /> コメントの削除<br /><br /> コメントの読み取り<br /><br /> コメントの更新|  
|レポートの使用|Reports|コンテンツの読み取り<br /><br /> レポート定義の読み込み<br /><br /> プロパティの読み取り|  
|レポートの使用|共有データセット|コンテンツの読み取り<br /><br /> レポート定義の読み込み<br /><br /> プロパティの読み取り|  
|リンク レポートの作成|レポート|リンクの作成<br /><br /> プロパティの読み取り|  
|すべてのサブスクリプションを管理|レポート|プロパティの読み取り<br /><br /> 任意のサブスクリプションの読み取り<br /><br /> 任意のサブスクリプションの作成<br /><br /> 任意のサブスクリプションの削除<br /><br /> 任意のサブスクリプションの更新|  
|コメントの管理<br />(SSRS 2017 以降、Power BI Report Server)|レポート|プロパティの読み取り<br /><br />コメントの削除|  
|データ ソースを管理する|フォルダー|データ ソースの作成|  
|データ ソースを管理する|Data Sources|プロパティの更新<br /><br /> 更新コンテンツの削除<br /><br /> プロパティの読み取り|  
|フォルダーの管理|フォルダー|フォルダーを作成する<br /><br /> 更新プロパティの削除<br /><br /> プロパティの読み取り|  
|個別のサブスクリプションを管理|レポート|プロパティの読み取り<br /><br /> サブスクリプションの作成<br /><br /> サブスクリプションの削除<br /><br /> サブスクリプションの読み取り<br /><br /> サブスクリプションの更新|  
|モデルを管理する|フォルダー|モデルの作成|  
|モデルを管理する|モデル|プロパティの読み取り<br /><br /> コンテンツの読み取り<br /><br /> 更新コンテンツの削除<br /><br /> データ ソースの読み取り<br /><br /> データ ソースの更新<br /><br /> モデル アイテム承認ポリシーの読み取り<br /><br /> モデル アイテム承認ポリシーの更新<br /><br /> 更新プロパティの削除|  
|レポート履歴の管理|レポート|プロパティの読み取り<br /><br /> レポート履歴の作成<br /><br /> レポート履歴の削除<br /><br /> 読み取りポリシーの実行<br /><br /> ポリシーの更新<br /><br /> レポート履歴の一覧表示|  
|レポートの管理|フォルダー|レポートの作成<br /><br /> 共有データセットの作成にも適用|  
|レポートの管理|レポート|プロパティの読み取り<br /><br /> 更新プロパティの削除<br /><br /> パラメーターの更新<br /><br /> データ ソースの読み取り<br /><br /> データ ソースの更新<br /><br /> レポート定義の読み取り<br /><br /> レポート定義の更新<br /><br /> 読み取りポリシーの実行<br /><br /> ポリシーの更新|  
|レポートの管理|共有データセット|プロパティの読み取り<br /><br /> 更新プロパティの削除<br /><br /> パラメーターの更新<br /><br /> データ ソースの読み取り<br /><br /> データ ソースの更新<br /><br /> レポート定義の読み取り<br /><br /> レポート定義の更新<br /><br /> 読み取りポリシーの実行<br /><br /> ポリシーの更新|  
|リソースの管理|フォルダー|リソースを作成する|  
|リソースの管理|リソース|プロパティの更新<br /><br /> 更新コンテンツの削除<br /><br /> プロパティの読み取り|  
|リソースの管理|レポート パーツ|プロパティの更新<br /><br /> 更新コンテンツの削除<br /><br /> プロパティの読み取り|  
|アイテムごとにセキュリティを設定|レポート、リソース、データ ソース、共有データセット、フォルダー|セキュリティ ポリシーの読み取り、セキュリティ ポリシーの更新|  
|データ ソースの表示|データ ソース|コンテンツの読み取り<br /><br /> プロパティの読み取り|  
|フォルダーの表示|フォルダー|プロパティの読み取り<br /><br /> 実行および表示<br /><br /> レポート履歴の一覧表示|  
|モデルの表示|レポート モデル|プロパティの読み取り<br /><br /> コンテンツの読み取り<br /><br /> データ ソースの読み取り|  
|レポートの表示|レポート|コンテンツの読み取り<br /><br /> プロパティの読み取り|  
|レポートの表示|共有データセット|コンテンツの読み取り<br /><br /> プロパティの読み取り|  
|リソースの表示|リソース|コンテンツの読み取り<br /><br /> プロパティの読み取り|  
|リソースの表示|レポート パーツ|コンテンツの読み取り<br /><br /> プロパティの読み取り|  
  
## <a name="see-also"></a>参照  
 [ネイティブ モードのレポート サーバーに対する権限の許可](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
