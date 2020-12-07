---
title: ログ配布のセカンダリへのフェールオーバー
description: SQL Server Management Studio または Transact-SQL を使用して、SQL Server ログ配布のセカンダリにフェールオーバーする方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- primary databases [SQL Server]
- secondary data files [SQL Server], manual fail over
- log shipping [SQL Server], failover
- failover [SQL Server], log shipping
ms.assetid: edfe5d59-4287-49c1-96c9-dd56212027bc
author: cawrites
ms.author: chadam
ms.openlocfilehash: d4e6ec31a1f1082ae13142fe521858122f079939
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96130753"
---
# <a name="fail-over-to-a-log-shipping-secondary-sql-server"></a>ログ配布のセカンダリへのフェールオーバー (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  ログ配布のセカンダリへのフェールオーバーは、プライマリ サーバー インスタンスが失敗した場合、またはプライマリ サーバー インスタンスにメンテナンスが必要な場合に役立ちます。  
  
## <a name="preparing-for-a-controlled-failover"></a>制御されたフェールオーバーの準備  
 プライマリ データベースは最新のバックアップ ジョブの後も更新され続けるため、通常、プライマリ データベースとセカンダリ データベースは同期されていません。 また、場合によっては、最新のトランザクション ログのバックアップは、セカンダリ サーバー インスタンスにコピーされていなかったり、コピーされたログのバックアップの一部がセカンダリ データベースにまだ適用されていない可能性があります。 可能な場合は、すべてのセカンダリ データベースをプライマリ データベースに同期することから開始することをお勧めします。  
  
 ログ配布ジョブの詳細については、「 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)」を参照してください。  
  
## <a name="failing-over"></a>フェールオーバー  
 セカンダリ データベースにフェールオーバーするには、次の操作を行います。  
  
1.  バックアップ共有からコピーされていないバックアップ ファイルを、各セカンダリ サーバーのコピー先フォルダーにコピーします。  
  
2.  適用されていないトランザクション ログのバックアップを、各セカンダリ データベースに順に適用します。 詳細については、「[トランザクション ログ バックアップの適用 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)」を参照してください。  
  
3.  プライマリ データベースにアクセスできる場合は、アクティブなトランザクション ログをバックアップし、そのログのバックアップをセカンダリ データベースに適用します。 復元コマンドを発行する前に排他アクセスを取得し、復元の完了後にマルチユーザーに切り替えるには、データベースを[シングル ユーザー モード](../../relational-databases/databases/set-a-database-to-single-user-mode.md)に設定しなければならない場合があります。  
  
     元のプライマリ サーバー インスタンスが破損していない場合は、WITH NORECOVERY を使用してプライマリ データベースのトランザクション ログの末尾をバックアップします。 これにより、データベースは復旧状態で維持されるので、ユーザーは使用できなくなります。 最終的には、置換プライマリ データベースからトランザクション ログのバックアップを適用することにより、このデータベースをロールフォワードできるようになります。  
  
     詳細については、「[トランザクション ログ バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)」を参照してください。   
  
4.  セカンダリ サーバーが同期された後は、任意のサーバーのセカンダリ データベースを復旧し、そのサーバー インスタンスにクライアントをリダイレクトすることによって、そのサーバーにフェールオーバーできます。 復旧によって、データベースは一貫性のある状態になり、オンラインになります。  
  
    > [!NOTE]  
    >  セカンダリ データベースを使用可能にするときは、そのデータベースのメタデータと元のプライマリ データベースのメタデータに一貫性があることを確認します。 詳細については、「 [データベースを別のサーバー インスタンスで使用できるようにするときのメタデータの管理 &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)」を参照してください。  
  
5.  セカンダリ データベースを復旧した後は、そのデータベースが他のセカンダリ データベースのプライマリ データベースとして機能するように再構成できます。  
  
     他に使用できるセカンダリ データベースがない場合の詳細については、「[ログ配布の構成 &#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md)」を参照してください。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 関連タスク  
  
-   [プライマリ ログ配布サーバーとセカンダリ ログ配布サーバー間でのロールの変更 &#40;SQL Server&#41;](../../database-engine/log-shipping/change-roles-between-primary-and-secondary-log-shipping-servers-sql-server.md)  
  
-   [役割の交代後のログインとジョブの管理 &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [ログ配布テーブルとストアド プロシージャ](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)   
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [ログ末尾のバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)  
  
  
