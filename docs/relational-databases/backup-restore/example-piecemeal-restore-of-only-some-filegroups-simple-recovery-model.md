---
title: '段階的な部分復元: 一部のファイル グループのみ (単純復旧モデル)'
description: この例では、単純復旧モデルを使用して、SQL Server のデータベースの一部のファイル グループのみを復元する段階的な部分復元を示します。
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- piecemeal restores [SQL Server], simple recovery model
- restore sequences [SQL Server], piecemeal
- simple recovery model [SQL Server], RESTORE examples
ms.assetid: d7ad026c-5355-4308-9560-0dc843940d4f
author: cawrites
ms.author: chadam
ms.openlocfilehash: 977945ad8d48996c55da7125fa8f58af0a53782d
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96126920"
---
# <a name="example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model"></a>例:一部のファイル グループのみを復元する段階的な部分復元 (単純復旧モデル)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  このトピックは、読み取り専用のファイル グループを含む、単純復旧モデルの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに関連しています。  
  
 段階的な部分復元シーケンスでは、プライマリ ファイル グループからすべての読み取り/書き込みセカンダリ ファイル グループの順に、ファイル グループレベルで段階的にデータベースが復元および復旧されます。  
  
 この例では、単純復旧モデルを使用する `adb`というデータベースに 3 つのファイル グループが含まれているとします。 ファイル グループ `A` は読み取り/書き込みが可能で、ファイル グループ `B` とファイル グループ `C` は読み取り専用です。 最初は、すべてのファイル グループがオンラインです。  
  
 データベース `B` のプライマリ ファイル グループとファイル グループ `adb` が破損しているようなので、データベース管理者は段階的な部分復元シーケンスを使用して、これらを復元することにしました。 単純復旧モデルでは、すべての読み取り/書き込みファイル グループは、同じ部分バックアップから復元する必要があります。 ファイル グループ `A` は破損していませんが、プライマリ ファイル グループと共に復元して一貫性を維持する必要があります (データベースは前回の部分バックアップの末尾で定義されている時点まで復元されます)。 ファイル グループ `C` も破損していませんが、復旧してオンラインにする必要があります。 ファイル グループ `B`は破損していますが、ファイル グループ `C`に比べて重要なデータが少ないため、最後に `B` を復元します。  
  
## <a name="restore-sequences"></a>復元シーケンス  
  
> [!NOTE]  
>  オンライン復元シーケンスでは、オフライン復元シーケンスと同じ構文を使用します。  
  
1.  部分バックアップからプライマリ ファイル グループとファイル グループ `A` を部分復元します。  
  
    ```  
    RESTORE DATABASE adb READ_WRITE_FILEGROUPS FROM partial_backup   
    WITH PARTIAL, RECOVERY  
    ```  
  
     この時点では、プライマリ ファイル グループとファイル グループ `A` がオンラインです。 ファイル グループ `B` と `C` のファイルは、復旧待ち状態なので、オフラインです。  
  
2.  ファイル グループ `C`をオンライン復旧します。  
  
     上記で復元された部分バックアップはファイル グループ `C` が読み取り専用になった後で作成されているため、復元によりデータベースがある時点の状態に戻されていても、ファイル グループ `C` の一貫性は維持されます。 データベース管理者は、ファイル グループ `C`を復元せずにそのままオンラインに復旧します。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='C' WITH RECOVERY  
    ```  
  
     この時点で、プライマリ ファイル グループ、ファイル グループ `A` 、およびファイル グループ `C` はオンラインです。 ファイル グループ B のファイルは復旧が保留になったままで、ファイル グループはオフラインになっています。  
  
3.  ファイル グループ  をオンライン復元します。 `B.`  
  
     ファイル グループ `B` のファイルは、復元する必要があります。 データベース管理者は、ファイル グループ `B` が読み取り専用になってから部分バックアップが作成されるまでの間に作成されたファイル グループ `B` のバックアップから、復元を行います。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup   
    WITH RECOVERY  
    ```  
  
     すべてのファイル グループがオンラインになります。  
  
## <a name="additional-examples"></a>その他の例  
  
-   [例: データベースの段階的な部分復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [例: 読み取り専用ファイルのオンライン復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [例: データベースの段階的な部分復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [例: 一部のファイル グループのみを復元する段階的な部分復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [例: 読み取り/書き込みファイルのオンライン復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [例: 読み取り専用ファイルのオンライン復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>参照  
 [Online Restore &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [段階的な部分復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
