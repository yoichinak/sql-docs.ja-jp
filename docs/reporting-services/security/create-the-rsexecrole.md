---
description: RSExecRole を作成する
title: RSExecRole を作成する | Microsoft Docs
ms.date: 06/12/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- RSExecRole
ms.assetid: 7ac17341-df7e-4401-870e-652caa2859c0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3735f53eac6101d2cc02568d1ea6fa789df50512
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91935394"
---
# <a name="create-the-rsexecrole"></a>RSExecRole を作成する

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、 **RSExecRole** と呼ばれる定義済みのデータベース ロールを使用して、レポート サーバー データベースに対するレポート サーバーの権限が付与されます。 **RSExecRole** ロールは、レポート サーバー データベースで自動的に作成されます。 原則として、このロールを変更したり、他のユーザーをこのロールに割り当てたりすることはできません。 ただし、レポート サーバー データベースを新規または別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] に移動した場合は、master および MSDB システム データベースでロールを再作成する必要があります。  
  
 ここで説明する手順に従って、次の操作を実行します。  
  
-   master システム データベースでの **RSExecRole** の作成と準備  
  
-   MSDB システム データベースでの **RSExecRole** の作成と準備  
  
> [!NOTE]  
> ここで説明する手順は、レポート サーバー データベースを準備する方法としてスクリプトの実行や WMI コードの作成を考えていないユーザーを対象としています。 大規模な配置を管理していて、データベースを定期的に移動する予定がある場合は、上記の操作を自動的に実行するスクリプトを作成する必要があります。 詳細については、「 [Reporting Service WMI プロバイダーへのアクセス](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md)」を参照してください。  
  
## <a name="before-you-start"></a>開始する前に  
  
-   データベースを移動した後に復元できるように、暗号化キーをバックアップします。 この手順は **RSExecRole**の作成と準備には直接影響しませんが、作業を確認するためにはキーのバックアップが必要です。 詳細については、「 [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)」を参照してください。  
  
-   **インスタンスでの** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 権限を持つユーザー アカウントでログオンしていることを確認します。  
  
-   使用する予定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに [!INCLUDE[ssDE](../../includes/ssde-md.md)] エージェント サービスがインストールされ、実行されていることを確認します。  
  
-   ReportServerTempDB および ReportServer データベースをアタッチします。 実際のロールを作成するためにデータベースをアタッチする必要はありませんが、作業を確認する場合は事前にデータベースをアタッチする必要があります。  
  
 **RSExecRole** を手動で作成する手順は、レポート サーバー インストールの移行というコンテキストで使用されることを目的としています。 レポート サーバー データベースのバックアップや移動などの重要なタスクは、このトピックでは取り上げませんが、データベース エンジンのドキュメントで説明されています。  
  
## <a name="create-rsexecrole-in-master"></a>master での RSExecRole の作成  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスの拡張ストアド プロシージャを使用して、スケジュールされた操作をサポートします。 次の手順では、プロシージャの実行権限を **RSExecRole** ロールに付与する方法について説明します。  
  
### <a name="to-create-rsexecrole-in-the-master-system-database-using-management-studio"></a>Management Studio を使用して master システム データベースに RSExecRole を作成するには  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を起動し、レポート サーバー データベースをホストする [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスに接続します。  
  
2.  **[データベース]** を開きます。  
  
3.  **[システム データベース]** を開きます。  
  
4.  **[master]** を開きます。  
  
5.  **[セキュリティ]** を開きます。  
  
6.  **[ロール]** を開きます。  
  
7.  **[データベース ロール]** を右クリックして **[新しいデータベース ロール]** をクリックします。 **[データベース ロール - 新規]** ページが表示されます。  
  
8.  **[ロール名]** に「 **RSExecRole**」と入力します。  
  
9. **[所有者]** に「**dbo**」と入力します。  
  
10. **[セキュリティ保護可能なリソース]** ページを選択します。  
  
11. **[検索]** をクリックします。 **[オブジェクトの追加]** ダイアログ ボックスが表示されます。 既定では、 **[特定のオブジェクト]** オプションが選択されています。  
  
12. **[OK]** をクリックします。 **[オブジェクトの選択]** ダイアログ ボックスが表示されます。  
  
13. **[オブジェクトの種類]** をクリックします。  
  
14. **[拡張ストアド プロシージャ]** をクリックします。  
  
15. **[OK]** をクリックします。  
  
16. **[参照]** をクリックします。  
  
17. 拡張ストアド プロシージャの一覧を下にスクロールし、以下を選択します。  
  
    1.  xp_sqlagent_enum_jobs  
  
    2.  xp_sqlagent_is_starting  
  
    3.  xp_sqlagent_notify  
  
18. **[OK]** をクリックし、もう一度 **[OK]** をクリックします。  
  
19. **[実行]** 行の **[許可]** 列で、チェック ボックスを選択します。  
  
20. 残りの各ストアド プロシージャに同じ操作を繰り返します。 **RSExecRole** には、3 個のストアド プロシージャすべてに対する実行権限を付与する必要があります。  

21. **[OK]** を選択して作業を終了します。  
  
 ![データベース ロールのプロパティ ページ](../../reporting-services/security/media/rsexecroledbproperties.gif "データベース ロールのプロパティ ページ")  
  
## <a name="create-rsexecrole-in-msdb"></a>MSDB での RSExecRole の作成  
 Reporting Services は、スケジュールされた操作をサポートするために、SQL Server エージェント サービスのストアド プロシージャを使用し、システム テーブルからジョブ情報を取得します。 次の手順では、プロシージャに対する実行権限およびテーブルでの選択権限を RSExecRole に付与する方法を説明します。  
  
### <a name="to-create-rsexecrole-in-the-msdb-system-database"></a>MSDB システム データベースで RSExecRole を作成するには  
  
1.  MSDB のストアド プロシージャとテーブルに対する権限を付与する場合は、同様の手順を繰り返します。 手順を簡素化するために、ストアド プロシージャとテーブルを別々に準備します。  
  
2.  **[MSDB]** を開きます。  
  
3.  **[セキュリティ]** を開きます。  
  
4.  **[ロール]** を開きます。  
  
5.  **[データベース ロール]** を右クリックして **[新しいデータベース ロール]** をクリックします。 [全般] ページが表示されます。  
  
6.  [ロール名] に「 **RSExecRole**」と入力します。  
  
7.  [所有者] に「**dbo**」と入力します。  
  
8.  **[セキュリティ保護可能なリソース]** ページを選択します。  
  
9.  **[検索]** をクリックします。 **[オブジェクトの追加]** ダイアログ ボックスが表示されます。 **[オブジェクトの指定]** オプションが既定で選択されます。  
  
10. **[OK]** をクリックします。  
  
11. **[オブジェクトの種類]** をクリックします。  
  
12. **[ストアド プロシージャ]** をクリックします。  
  
13. **[OK]** をクリックします。  
  
14. **[参照]** をクリックします。  
  
15. 項目の一覧を下にスクロールし、以下を選択します。  
  
    1.  sp_add_category  
  
    2.  sp_add_job  
  
    3.  sp_add_jobschedule  
  
    4.  sp_add_jobserver  
  
    5.  sp_add_jobstep  
  
    6.  sp_delete_job  
  
    7.  sp_help_category  
  
    8.  sp_help_job  
  
    9. sp_help_jobschedule  
  
    10. sp_verify_job_identifiers  
  
16. **[OK]** をクリックしてから、もう一度 **[OK]** をクリックします。  
  
17. 最初のストアド プロシージャ sp_add_category を選択します。  
  
18. **[実行]** 行の **[許可]** 列で、チェック ボックスをオンにします。  
  
19. 残りの各ストアド プロシージャに同じ操作を繰り返します。 RSExecRole には、10 個のストアド プロシージャすべてに対する実行権限を付与する必要があります。  
  
20. 引き続き **[セキュリティ保護可能なリソース]** ページでもう一度 **[検索]** をクリックします。 **[オブジェクトの追加]** ダイアログ ボックスが表示されます。 **[オブジェクトの指定]** オプションが既定で選択されます。  
  
21. **[OK]** をクリックします。  
  
22. **[オブジェクトの種類]** をクリックします。  
  
23. **[テーブル]** をクリックします。  
  
24. **[OK]** をクリックします。  
  
25. **[参照]** をクリックします。  
  
26. 項目の一覧を下にスクロールし、以下を選択します。  
  
    1.  syscategories  
  
    2.  sysjobs  
  
27. **[OK]** をクリックし、もう一度 **[OK]** をクリックします。  
  
28. 最初のテーブル syscategories を選択します。  
  
29. **[選択]** 行の **[許可]** 列で、チェック ボックスをオンにします。  
  
30. sysjobs テーブルに同じ操作を繰り返します。 RSExecRole には、両方のテーブルに対する選択権限を付与する必要があります。  
  
31. **[OK]** を選択して作業を終了します。  
  
## <a name="move-the-report-server-database"></a>レポート サーバー データベースの移動  
 ロールを作成したら、レポート サーバー データベースを新しい SQL Server インスタンスに移動できます。 詳細については、「[別のコンピューターへのレポート サーバー データベースの移動](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)」を参照してください。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] を SQL Server 2016 以降にアップグレードする場合、そのアップグレードはデータベースを移動する前と後のどちらでも実行できます。  
  
 レポート サーバー データベースは、レポート サーバーがそのデータベースに接続するときに、自動的にアップグレードされます。 データベースをアップグレードするために特定の手順を実行する必要はありません。  
  
## <a name="restore-encryption-keys-and-verify-your-work"></a>暗号化キーの復元と作業の確認  
 レポート サーバー データベースをアタッチしたら、次の手順を実行して作業を確認します。  
  
### <a name="to-verify-report-server-operability-after-a-database-move"></a>データベース移動後にレポート サーバーの運用性を確認するには  
  
1.  Reporting Services 構成ツールを起動して、レポート サーバーに接続します。  
  
2.  **[データベース]** をクリックします。  
  
3.  **[データベースの変更]** をクリックします。  
  
4.  **[既存のレポート サーバー データベースを選択する]** をクリックします。  
  
5.  データベース エンジンのサーバー名を入力します。 レポート サーバー データベースを名前付きインスタンスにアタッチした場合は、\<servername>\\<instancename\> の形式でインスタンス名を入力する必要があります。  
  
6.  **[接続テスト]** をクリックします。 "接続テストに成功しました" というダイアログ ボックスが表示されるはずです。
  
7.  **[OK]** を選択してダイアログ ボックスを閉じ、**[次へ]** を選択します。  
  
8.  [データベース] で、レポート サーバー データベースを選択します。  
  
9.  **[次へ]** をクリックして、ウィザードを完了します。  
  
10. **[暗号化キー]** をクリックします。  
  
11. **[復元]** をクリックします。  
  
12. レポート サーバー データベースに格納されている資格情報および接続情報の暗号化を解除するために使用される対称キーのバックアップ コピーが含まれている厳密な名前のキー ファイル (.snk) を選択します。  
  
13. パスワードを入力し、 **[OK]** をクリックします。  
  
14. **[Web ポータルの URL]** をクリックします。  
  
15. リンクをクリックすると、Web ポータルが開きます。 レポート サーバー データベースのレポート サーバー アイテムが表示されます。  

## <a name="creating-the-rsexecrole-role-and-permissions-using-t-sql"></a>T-SQL を使用した RSExecRole ロールおよびアクセス許可の作成
次の T-SQL スクリプトを使用すると、システム データベースにロールも作成し、該当する権限を付与することができます。
```sql
USE master;
GO
IF NOT EXISTS (SELECT 1 FROM sys.database_principals WHERE [type] = 'R' AND [name] = 'RSExecRole') BEGIN
    CREATE ROLE [RSExecRole];
END
GRANT EXECUTE ON dbo.xp_sqlagent_enum_jobs TO [RSExecRole];
GRANT EXECUTE ON dbo.xp_sqlagent_is_starting TO [RSExecRole];
GRANT EXECUTE ON dbo.xp_sqlagent_notify TO [RSExecRole];
GO
USE msdb;
GO
IF NOT EXISTS (SELECT 1 FROM sys.database_principals WHERE [type] = 'R' AND [name] = 'RSExecRole') BEGIN
    CREATE ROLE [RSExecRole];
END
GRANT EXECUTE ON dbo.sp_add_category TO [RSExecRole];
GRANT EXECUTE ON dbo.sp_add_job TO [RSExecRole];
GRANT EXECUTE ON dbo.sp_add_jobschedule TO [RSExecRole];
GRANT EXECUTE ON dbo.sp_add_jobserver TO [RSExecRole];
GRANT EXECUTE ON dbo.sp_add_jobstep TO [RSExecRole];
GRANT EXECUTE ON dbo.sp_delete_job TO [RSExecRole];
GRANT EXECUTE ON dbo.sp_help_category TO [RSExecRole];
GRANT EXECUTE ON dbo.sp_help_job TO [RSExecRole];
GRANT EXECUTE ON dbo.sp_help_jobschedule TO [RSExecRole];
GRANT EXECUTE ON dbo.sp_verify_job_identifiers TO [RSExecRole];
GRANT SELECT ON dbo.syscategories TO [RSExecRole];
GRANT SELECT ON dbo.sysjobs TO [RSExecRole];
GO
```

## <a name="next-steps"></a>次のステップ

[別のコンピューターへのレポート サーバー データベースの移動 (SSRS ネイティブ モード)](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)   
[ネイティブ モードのレポート サーバー データベースを作成する &#40;レポート サーバーの構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
[レポート サーバーの構成マネージャー &#40;ネイティブ モード&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
[Reporting Services の暗号化キーのバックアップと復元](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
