---
title: エラーとイベントのリファレンス (Reporting Services)
description: さまざまなレポート サーバー イベントの ID、種類、カテゴリ、ソース、説明を確認できます。 これらのイベントの種類には、エラー、警告、情報があります。
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.custom: ''
ms.date: 06/12/2019
ms.openlocfilehash: 2631af98c007914e59994d05b83b59186f320ecd
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91935174"
---
# <a name="errors-and-events-reference-reporting-services"></a>エラーとイベントのリファレンス (Reporting Services)

この記事では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のエラーとイベントについて説明します。 エラー情報は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のログ ファイルにも記録されます。 使用可能なログ ファイルの種類とログの表示方法の詳細については、「 [Reporting Services のログ ファイルとソース](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)」を参照してください。  

## <a name="cause-and-resolution-for-reporting-services-error-messages"></a>Reporting Services のエラー メッセージの原因と解決方法  

[!INCLUDE[msCoName](../../includes/msconame-md.md)] Web サイトでは、最も頻繁に検索されているエラーの原因と解決方法についての情報を入手できます。 詳細については、「 [Reporting Services エラーの原因と解決方法](../../reporting-services/troubleshooting/cause-and-resolution-of-reporting-services-errors.md)」を参照してください。  
  
## <a name="report-server-events"></a>レポート サーバーのイベント

次のレポート サーバーのイベントは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アプリケーション ログに記録されます。  
  
|イベント ID|Type|カテゴリ|source|説明|  
|--------------|----------|--------------|------------|-----------------|  
|106|エラー|スケジュール設定|レポート サーバー|スケジュールされた操作 (たとえば、レポートのサブスクリプションおよび配信) を定義する場合は、SQL Server エージェントを実行する必要があります。|  
|[107](../../reporting-services/troubleshooting/report-server-windows-service-mssqlserver-107.md)|エラー|起動/シャットダウン|レポート サーバー<br /><br /> スケジュールおよび配信のプロセッサ|*\<Source>* からレポート サーバー データベースに接続できません。 詳細については、「[レポート サーバー Windows サービス &#40;MSSQLServer&#41; 107](../../reporting-services/troubleshooting/report-server-windows-service-mssqlserver-107.md)」を参照してください。|  
|108|エラー|拡張機能|レポート サーバー<br /><br /> Web ポータル|*\<Source>* から、配信、データ処理、または表示拡張機能を読み込めません。<br /><br /> 最も可能性が高い原因として、配置が完全でないか、拡張機能が削除された可能性があります。 詳細については、SQL Server オンライン ブックの「 [データ処理拡張機能の配置](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md) 」および「 [配信拡張機能の配置](../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)」を参照してください。|  
|109|Information|管理|レポート サーバー<br /><br /> Web ポータル|構成ファイルが変更されています。 詳細については、「 [Reporting Services 構成ファイル](../../reporting-services/report-server/reporting-services-configuration-files.md)」を参照してください。|  
|110|警告|管理|レポート サーバー<br /><br /> Web ポータル|1 つの構成ファイルの設定が変更され、設定が無効になっています。 代わりに既定値が使用されます。 詳細については、「 [Reporting Services 構成ファイル](../../reporting-services/report-server/reporting-services-configuration-files.md)」を参照してください。|  
|111|エラー|ログ記録|レポート サーバー<br /><br /> Web ポータル|*\<Source>* からトレース ログを作成できません。 詳細については、「 [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)」を参照してください。|  
|112|警告|Security|レポート サーバー|レポート サーバーは、サービス拒否攻撃 (DoS) の可能性を検出しました。 詳細については、「 [Reporting Services のセキュリティと保護](../../reporting-services/security/reporting-services-security-and-protection.md)」を参照してください。|  
|113|エラー|ログ記録|レポート サーバー|レポート サーバーでは、パフォーマンス カウンターを作成できません。|  
|114|エラー|起動/シャットダウン|Web ポータル|Web ポータルは ReportServer サービスに接続できません。|  
|115|警告|スケジュール設定|スケジュールおよび配信のプロセッサ|SQL Server エージェント キューの定期タスクは、変更または削除されました。|  
|116|エラー|内部|レポート サーバー<br /><br /> Web ポータル<br /><br /> スケジュールおよび配信のプロセッサ|An internal error occurred.|  
|117|エラー|起動/シャットダウン|レポート サーバー|レポート サーバー データベースのバージョンが無効です。|  
|118|警告|ログ記録|レポート サーバー<br /><br /> Web ポータル|予期されたディレクトリの場所にトレース ログがありません。既定のディレクトリに新しいトレース ログが作成されます。 詳細については、「 [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)」を参照してください。|  
|119|エラー|アクティブ化|レポート サーバー<br /><br /> スケジュールおよび配信のプロセッサ|*\<Source>* には、レポート サーバー データベースのコンテンツへのアクセス権がありません。|  
|120|エラー|アクティブ化|レポート サーバー|対称キーの暗号化を解除できません。 最も可能性が高い原因として、サービスの実行に使用されるアカウントが変更されたことが考えられます。 詳細については、「[暗号化キーの構成と管理 &#40;レポート サーバーの構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)」を参照してください。|  
|121|エラー|起動/シャットダウン|レポート サーバー|リモート プロシージャ コール (RPC) サービスを開始できませんでした。|  
|122|警告|配送|スケジュールおよび配信のプロセッサ|スケジュールおよび配信のプロセッサは、電子メールの配信に使用している SMTP サーバーに接続できません。 SMTP サーバー接続の詳細については、「[電子メールの設定 - Reporting Services のネイティブ モード (Configuration Manager)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)」を参照してください。|  
|123|警告|ログ記録|レポート サーバー<br /><br /> Web ポータル|レポート サーバーでは、トレース ログへの書き込みに失敗しました。 トレース ログの詳細については、「 [レポート サーバー サービスのトレース ログ](../../reporting-services/report-server/report-server-service-trace-log.md)」を参照してください。|  
|124|Information|アクティブ化|レポート サーバー|レポート サーバー サービスが初期化されました。 詳細については、[レポート サーバーの初期化 &#40;レポート サーバーの構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md) に関するページを参照してください。|  
|125|Information|アクティブ化|レポート サーバー|データの暗号化に使用したキーは、正常に展開されました。 キーの詳細については、「[暗号化キーの構成と管理 &#40;レポート サーバーの構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)」を参照してください。|  
|126|Information|アクティブ化|レポート サーバー|データの暗号化に使用したキーは、正常に適用されました。 キーの詳細については、「[暗号化キーの構成と管理 &#40;レポート サーバーの構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)」を参照してください。|  
|127|Information|アクティブ化|レポート サーバー|暗号化されたコンテンツは、正常にレポート サーバー データベースから削除されました。 回復不可能な暗号化されたデータの削除に関する詳細については、「[暗号化キーの構成と管理 &#40;レポート サーバーの構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)」を参照してください。|  
|128|エラー|アクティブ化|レポート サーバー|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コンポーネントのエディションが異なる場合は一緒に使用することはできません。|  
|129|エラー|管理|レポート サーバー<br /><br /> スケジュールおよび配信のプロセッサ|暗号化された構成ファイルの設定の暗号化を解除できません。|  
|130|エラー|管理|レポート サーバー<br /><br /> スケジュールおよび配信のプロセッサ|*\<Source>* から構成ファイルを見つけられません。 レポート サーバーでは、構成ファイルが必要です。|  
|131|エラー|Security|レポート サーバー<br /><br /> スケジュールおよび配信のプロセッサ|暗号化されたユーザー データ値の暗号化を解除できませんでした。|  
|132|エラー|Security|レポート サーバー|ユーザー データの暗号化中にエラーが発生しました。 値は保存されません。|  
|133|エラー|管理|レポート サーバー<br /><br /> Web ポータル<br /><br /> スケジュールおよび配信のプロセッサ|構成ファイルを読み込めませんでした。 このエラーは、XML が無効な場合に発生することがあります。|  
|134|エラー|管理|レポート サーバー|レポート サーバーでは、構成ファイルの設定の値を暗号化できませんでした。|  
  
## <a name="see-also"></a>関連項目

 [Reporting Services のサブスクリプションを監視する](../../reporting-services/subscriptions/monitor-reporting-services-subscriptions.md)  
 [Reporting Services のログ ファイルとソース](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)
