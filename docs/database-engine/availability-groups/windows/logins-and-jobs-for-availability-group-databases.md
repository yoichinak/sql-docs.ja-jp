---
title: 可用性グループ内のデータベースでのジョブのログイン管理
description: Always On 可用性グループに参加しているデータベースを使用するジョブのログインを管理する方法の説明。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: d7da14d3-848c-44d4-8e49-d536a1158a61
author: cawrites
ms.author: chadam
ms.openlocfilehash: 59d07b5a3f469e6c25056b47c5ea859dd6e23afc
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584189"
---
# <a name="manage-logins-for-jobs-using-databases-in-an-always-on-availability-group"></a>Always On 可用性グループのデータベースを使用するジョブのログインを管理する
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Always On 可用性グループのすべてのプライマリ データベースとその対応するセカンダリ データベース上で、ユーザー ログインと [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント ジョブの同じセットを定期的に管理する必要があります。 可用性グループの可用性レプリカをホストする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のすべてのインスタンス上でログインとジョブを再作成する必要があります。  
  
-   **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント ジョブ**  
  
     関連するジョブを、元のプライマリ レプリカをホストするサーバー インスタンスから元のセカンダリ レプリカをホストするサーバー インスタンスに手動でコピーする必要があります。 すべてのデータベースで、関連するジョブの先頭にロジックを追加して、そのジョブがプライマリ データベースでのみ実行されるようにする必要があります。つまり、ローカル レプリカがデータベースのプライマリ レプリカである場合のみ実行されるようにします。  
  
     可用性グループの可用性レプリカをホストするサーバー インスタンスは、構成が異なる場合があります (別のテープ ドライブ文字など)。 各可用性レプリカのジョブは、このような違いを考慮する必要があります。  
  
     バックアップ ジョブは、 [sys.fn_hadr_is_preferred_backup_replica](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md) 関数を使用し、可用性グループのバックアップ設定に従ってローカル レプリカがバックアップ用に推奨されるかどうかを識別できます。 [メンテナンス プラン ウィザード](../../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md) を使用して作成されたバックアップ ジョブは、ネイティブでこの関数を使用します。 他のバックアップ ジョブでは、バックアップ ジョブの中でこの関数を条件として使用して、バックアップ ジョブが優先レプリカでのみ実行されるようにすることをお勧めします。 詳細については、「 [アクティブなセカンダリ: セカンダリ レプリカでのバックアップ &#40;Always On 可用性グループ&#41;](../../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)」を参照してください。  
  
-   **ログイン**  
  
     包含データベースを使用している場合は、データベースの包含ユーザーを構成でき、これらのユーザーにはセカンダリ レプリカをホストするサーバー インスタンス上のログインを作成する必要がありません。 非包含可用性データベースでは、可用性レプリカをホストするサーバー インスタンス上で、ログインするユーザーを作成する必要があります。 詳細については、「[CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md)」を参照してください。  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証またはローカル Windows ログインを使用するアプリケーションがある場合は、このトピックの「[SQL Server 認証またはローカル Windows ログインを使用するアプリケーションのログイン](../../../database-engine/availability-groups/windows/logins-and-jobs-for-availability-group-databases.md#SSauthentication)」を参照してください。  
  
    > [!NOTE]  
    >  SQL Server ログインが未定義のデータベース ユーザー、またはサーバー インスタンスで適切に定義されていないデータベース ユーザーは、インスタンスにログインできません。 このようなユーザーは、そのサーバー インスタンスのデータベースの *孤立ユーザー* と呼ばれます。 ユーザーが特定のサーバー インスタンスで孤立している場合は、いつでもユーザー ログインをセットアップできます。 詳細については、「 [孤立ユーザーのトラブルシューティング &#40;SQL Server&#41;](../../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)を実行します。  
  
-   **追加メタデータ**  
  
     ログインとジョブは、特定の可用性グループのセカンダリ レプリカをホストする各サーバー インスタンスで再作成する必要がある唯一の情報ではありません。 たとえば、サーバー構成設定、資格情報、暗号化されたデータ、権限、サービス ブローカー アプリケーション、トリガー (サーバー レベル) などの再作成が必要な場合があります。 詳細については、「 [データベースを別のサーバー インスタンスで使用できるようにするときのメタデータの管理 &#40;SQL Server&#41;](../../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)」を参照してください。  
  
##  <a name="logins-of-applications-that-use-sql-server-authentication-or-a-local-windows-login"></a><a name="SSauthentication"></a> SQL Server 認証またはローカル Windows ログインを使用するアプリケーションのログイン  
 アプリケーションで SQL Server 認証またはローカル Windows ログインを使用している場合、SID が一致しないと、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のリモート インスタンスでアプリケーションのログインを解決できないことがあります。 SID が一致しないと、ログインはリモート サーバー インスタンスの孤立ユーザーになります。 この問題は、アプリケーションがフェールオーバー後にミラー化されたデータベースまたはログ配布データベース、またはバックアップから初期化されたレプリケーション サブスクライバー データベースに接続すると発生する可能性があります。  
  
 この問題を防ぐために、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のリモート インスタンスによってホストされているデータベースを使用するようにアプリケーションをセットアップする場合、予防策を講じることをお勧めします。 予報策として、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のローカル インスタンスから [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のリモート インスタンスにログインとパスワードを転送する必要があります。 この問題を回避する方法の詳細については、サポート技術情報の記事 918992 「[SQL Server のインスタンス間でログインおよびパスワードを転送する方法](https://support.microsoft.com/kb/918992/)」を参照してください。  
  
> [!NOTE]  
>  この問題は、さまざまなコンピューターの Windows ローカル アカウントに影響します。 ただし、各コンピューターの SID は同じであるため、この問題はドメイン アカウントでは発生しません。  
  
 詳細については、「 [Orphaned Users with Database Mirroring and Log Shipping](/archive/blogs/sqlserverfaq/orphaned-users-with-database-mirroring-and-log-shipping) 」(データベース ミラーリングとログ配布での孤立ユーザー) (データベース エンジンのブログ) を参照してください。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 関連タスク  
  
-   [ログインの作成](../../../relational-databases/security/authentication-access/create-a-login.md)  
  
-   [データベース ユーザーの作成](../../../relational-databases/security/authentication-access/create-a-database-user.md)。  
  
-   [ジョブの作成](../../../ssms/agent/create-a-job.md)  
  
-   [データベースを別のサーバー インスタンスで使用できるようにするときのメタデータの管理 &#40;SQL Server&#41;](../../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [包含データベース](../../../relational-databases/databases/contained-databases.md)   
 [ジョブの作成](../../../ssms/agent/create-jobs.md)  
  
