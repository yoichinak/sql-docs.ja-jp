---
title: '段階的な部分復元: 完全復旧モデル'
description: この例では、ログ末尾のバックアップから始まる完全復旧モデルを使用した、SQL Server でのデータベースの段階的な部分復元を示します。
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full recovery model [SQL Server], RESTORE example
- piecemeal restores [SQL Server], full recovery model
- restore sequences [SQL Server], piecemeal
ms.assetid: 0a84892d-2f7a-4e77-b2d0-d68b95595210
author: cawrites
ms.author: chadam
ms.openlocfilehash: 0da932c7e2834074cece2224c1bdb94bc756caf8
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96130412"
---
# <a name="example-piecemeal-restore-of-database-full-recovery-model"></a>例:データベースの部分復元 (完全復旧モデル)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  段階的な部分復元シーケンスでは、プライマリ ファイル グループとすべての読み書き可能なセカンダリ ファイル グループから順に、ファイル グループ レベルで段階的にデータベースが復元され、復旧されます。  
  
 この例では、障害発生後、データベース `adb` を新しいコンピューターに復元します。 データベースでは完全復旧モデルを使用しているため、復元を開始する前に、データベースのログ末尾のバックアップを作成する必要があります。 障害が発生する前は、すべてのファイル グループがオンラインです。 ファイル グループ `B` は読み取り専用です。 すべてのセカンダリ ファイル グループを復元する必要があります。ただし、これらのファイル グループは、重要度に従って `A` 、 `C`、 `B`の順に復元します (重要度が最も高いのは A です)。 この例では、ログ末尾のバックアップを含めて、4 つのログ バックアップがあるとします。  
  
## <a name="tail-log-backup"></a>ログ末尾のバックアップ  
 データベースの管理者は、データベースを復元する前に、ログの末尾をバックアップする必要があります。 データベースが破損しているため、ログ末尾のバックアップを作成するには、NO_TRUNCATE オプションを使用する必要があります。  
  
```  
BACKUP LOG adb TO tailLogBackup WITH NORECOVERY, NO_TRUNCATE  
```  
  
 ログ末尾のバックアップは、次の復元シーケンスの最後に適用されます。  
  
## <a name="restore-sequences"></a>復元シーケンス  
  
> [!NOTE]  
>  オンライン復元シーケンスでは、オフライン復元シーケンスと同じ構文を使用します。  
  
1.  プライマリおよびセカンダリ ファイル グループ `A`の部分復元を行います。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='Primary' FROM backup1   
       WITH PARTIAL, NORECOVERY  
    RESTORE DATABASE adb FILEGROUP='A' FROM backup2   
       WITH NORECOVERY  
    RESTORE LOG adb FROM log_backup3 WITH NORECOVERY  
    RESTORE LOG adb FROM log_backup4 WITH NORECOVERY  
    RESTORE LOG adb FROM log_backup5 WITH NORECOVERY  
    RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
    ```  
  
2.  ファイル グループ `C`をオンライン復元します。  
  
     この時点で、プライマリ ファイル グループとセカンダリ ファイル グループ `A` はオンラインです。 ファイル グループ `B` とファイル グループ `C` のすべてのファイルは復旧が保留されており、ファイル グループはオフラインです。  
  
     最後の `RESTORE LOG` ステートメント (手順 1.) からのメッセージでは、ファイル グループ `C` が使用できないため、このファイル グループを含むトランザクションのロールバックに遅延が生じたことが示されています。 通常の操作は続行できますが、これらのトランザクションによってロックが保持され、ロールバックが完了するまで、ログの切り捨てが行われません。  
  
     2 番目の復元シーケンスでは、データベース管理者がファイル グループ `C`を復元します。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='C' FROM backup2a WITH NORECOVERY  
    RESTORE LOG adb FROM log_backup3 WITH NORECOVERY  
    RESTORE LOG adb FROM log_backup4 WITH NORECOVERY  
    RESTORE LOG adb FROM log_backup5 WITH NORECOVERY  
    RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
    ```  
  
     この時点で、プライマリ ファイル グループ、ファイル グループ `A` 、およびファイル グループ `C` はオンラインです。 ファイル グループ `B` はオフラインで、このファイル グループのファイルは復旧待ち状態のままです。 遅延トランザクションは解決され、ログの切り捨てが行われます。  
  
3.  ファイル グループ `B`をオンライン復元します。  

   3 番目の復元シーケンスでは、データベース管理者がファイル グループ `B`を復元します。 ファイル グループ `B` のバックアップは、ファイル グループ B が読み取り専用になってから行います。このため、復旧中にこのファイル グループをロールフォワードする必要はありません。  
  
   ```sql  
   RESTORE DATABASE adb FILEGROUP='B' FROM backup2b WITH RECOVERY  
   ```  
  
   すべてのファイル グループがオンラインになります。  
  
## <a name="additional-examples"></a>その他の例  
  
-   [例: データベースの段階的な部分復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [例: 一部のファイル グループのみを復元する段階的な部分復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [例: 読み取り専用ファイルのオンライン復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [例: 一部のファイル グループのみを復元する段階的な部分復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [例: 読み取り/書き込みファイルのオンライン復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [例: 読み取り専用ファイルのオンライン復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>参照  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Online Restore &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [トランザクション ログ バックアップの適用 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [段階的な部分復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
