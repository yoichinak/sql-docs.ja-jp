---
description: データ移行の監視とトラブルシューティング (Stretch Database)
title: データ移行の監視とトラブルシューティング
ms.date: 06/14/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, monitoring
- monitoring Stretch Database
ms.assetid: 06950858-8c02-4ec6-9c59-42b787316a2d
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 7e4ca3f7b7a857e5c8592844c9523753b68a3728
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492672"
---
# <a name="monitor-and-troubleshoot-data-migration-stretch-database"></a>データ移行の監視とトラブルシューティング (Stretch Database)
[!INCLUDE [sqlserver2016-windows-only](../../includes/applies-to-version/sqlserver2016-windows-only.md)]


  Stretch Database モニターでデータ移行を監視するには、SQL Server Management Studio でデータベースについて **[タスク]、[Stretch]\(ストレッチ)、[Monitor]\(監視)** の順に選択します。  
  
## <a name="check-the-status-of-data-migration-in-the-stretch-database-monitor"></a>Stretch Database モニターでのデータ移行の状態の確認  
 SQL Server Management Studio でデータベースについて **[タスク]、[Stretch] \(ストレッチ)、[Monitor] \(監視)** の順に選択して Stretch Database モニターを開き、データ移行を監視します。  
  
-   モニターの上部には、Stretch 対応 SQL Server データベースとリモート Azure データベースの両方についての一般情報が表示されます。  
  
-   モニターの下部には、データベース内の各 Stretch 対応テーブルに関するデータ移行の状態が表示されます。  
  
 ![Stretch Database の監視](../../sql-server/stretch-database/media/stretch-monitor.PNG "Stretch Database の監視")  
  
##  <a name="check-the-status-of-data-migration-in-a-dynamic-management-view"></a><a name="Migration"></a> 動的管理ビューでのデータ移行の状態の確認  
 動的管理ビュー **sys.dm_db_rda_migration_status** を開いて、移行されたバッチ数とデータ行数を確認します。 詳細については、「[sys.dm_db_rda_migration_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/stretch-database-sys-dm-db-rda-migration-status.md)」を参照してください。  
  
##  <a name="troubleshoot-data-migration"></a><a name="Firewall"></a> データ移行のトラブルシューティング  
 **対象の Stretch 対応テーブルの行が Azure に移行されていません。何が問題なのでしょうか。**  
 移行に影響を与え得る問題は複数あります。 次の点を確認してください。  
  
-   SQL Server コンピューターに対するネットワーク接続を確認する。  
  
-   Azure ファイアウォールが、SQL Server からリモート エンドポイントへの接続をブロックしていないことを確認します。  
  
-   動的管理ビュー **sys.dm_db_rda_migration_status** で最新のバッチの状態を確認する。 エラーが発生した場合は、バッチの error_number、error_state、error_severity の値を確認します。  
  
    -   ビューの詳細については、「[sys.dm_db_rda_migration_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/stretch-database-sys-dm-db-rda-migration-status.md)」を参照してください。  
  
    -   SQL Server エラー メッセージの内容の詳細については「[sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)」を参照してください。  
  
 **ローカル サーバーからの接続が Azure ファイアウォールによってブロックされています。**  
 Azure サーバーの Azure ファイアウォール設定にルールを追加して、SQL Server がリモートの Azure サーバーと通信できるようにする必要があります。  
  
## <a name="see-also"></a>参照  
 [Stretch Database の管理とトラブルシューティング](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
  
