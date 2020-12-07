---
title: ファイルの完全バックアップ (SQL Server) | Microsoft Docs
description: SQL Server では、各ファイルを個別に指定する代わりにファイル グループ全体をバックアップし、復元することができます。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full backups [SQL Server]
- backing up [SQL Server], files or filegroups
- backups [SQL Server], files or filegroups
- full recovery model [SQL Server], full file backups
- file backups [SQL Server], full
- files [SQL Server], backing up
- filegroups [SQL Server], backing up
- file backups [SQL Server]
ms.assetid: a716bf8d-0c5a-490d-aadd-597b3b0fac0c
author: cawrites
ms.author: chadam
ms.openlocfilehash: 18b2c89a69a49fe45a066cba136f49039a734cfd
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96130383"
---
# <a name="full-file-backups-sql-server"></a>ファイルの完全バックアップ (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このトピックは、複数のファイルまたはファイル グループが含まれている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに適用されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース内のファイルは、個別にバックアップおよび復元できます。 また、構成する各ファイルを個別に指定する代わりにファイル グループ全体を指定できます。 ファイル グループにオフラインのファイルが含まれている場合 (たとえば、ファイルが復元中である場合)、ファイル グループ全体がオフラインになり、バックアップできないことに注意してください。  
  
 読み取り専用ファイル グループのファイル バックアップは、部分バックアップと組み合わせることができます。 部分バックアップには、読み取りと書き込みが可能なファイル グループすべて、および必要に応じて 1 つ以上の読み取り専用ファイル グループが含まれます。 詳細については、「[部分バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/partial-backups-sql-server.md)」を参照してください。  
  
 ファイル バックアップは、ファイルの差分バックアップの *差分ベース* として使用できます。 詳細については、「 [差分バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)」を参照してください。  
  
> [!NOTE]  
>  ファイルの完全バックアップは、通常、 *ファイルの差分バックアップ* と明確に区別する場合を除き、 *ファイル バックアップ* と呼ばれます。  
  
 **このトピックの内容**  
  
-   [ファイル バックアップの利点](#Benefits)  
  
-   [ファイル バックアップの欠点](#Disadvantages)  
  
-   [ファイル バックアップの概要](#Overview)  
  
-   [関連タスク](#RelatedTasks)  
  
##  <a name="benefits-of-file-backups"></a><a name="Benefits"></a> ファイル バックアップの利点  
 ファイル バックアップは、データベース バックアップよりも次の点で優れています。  
  
-   ファイル バックアップを使用すると、残りのデータベースを復元しないで損傷したファイルだけを復元できるので、復旧を高速化できます。  
  
     たとえば、異なるディスクに配置されている複数のファイルからデータベースが構成されていて、1 つのディスクに障害が発生した場合は、障害が発生したディスク上のファイルだけを復元する必要があります。 破損したファイルを高速に復元し、データベース全体を復元するよりも速く復旧できます。  
  
-   ファイル バックアップでは、データベースの完全バックアップよりもスケジュール設定とメディア処理を柔軟に行うことができます。非常に大規模なデータベースの場合、データベースの完全バックアップは管理しきれません。 柔軟性に優れたファイルまたはファイル グループのバックアップは、さまざまな更新特性を備えたデータを含む大規模なデータベースでも役に立ちます。  
  
##  <a name="disadvantages-of-file-backups"></a><a name="Disadvantages"></a> ファイル バックアップの欠点  
  
-   データベースの完全バックアップと比較した場合のファイル バックアップの大きな欠点は、管理の複雑さです。 これらのバックアップの完全なセットを保持および追跡するタスクは、データベースの完全バックアップの領域要件よりも重要な、時間のかかるタスクであることがあります。  
  
-   破損したファイルのバックアップがない場合、メディア障害が発生したときに、データベース全体を復旧できなくなります。 したがって、ファイル バックアップの完全なセットを保持しておく必要があります。また、完全復旧モデルまたは一括ログ復旧モデルの場合は、1 つ以上のログ バックアップが、最低でも、最初のファイルの完全バックアップと最新のファイルの完全バックアップの間に対応している必要があります。  
  
##  <a name="overview-of-file-backups"></a><a name="Overview"></a> ファイル バックアップの概要  
 ファイルの完全バックアップでは、1 つ以上のファイルまたはファイル グループに含まれるすべてのデータがバックアップされます。 ファイル バックアップには、バックアップ操作の最後までロール フォワードできる十分なログ レコードが既定で含まれています。  
  
 読み取り専用ファイルまたはファイル グループのバックアップはすべての復旧モデルで同じです。 完全復旧モデルでは、ファイルの完全バックアップの完全なセットと、ファイル バックアップのすべての範囲に対応したログ バックアップを併用することで、データベースの完全バックアップに等しくなります。  
  
 ファイル バックアップ操作は、一度に 1 回のみ実行できます。 1 回の操作で複数のファイルをバックアップできますが、ファイルを 1 つだけ復元する必要がある場合でも、復旧に時間がかかる可能性があります。 これは、対象のファイルを探すために、バックアップ全体が読み取られるためです。  
  
> [!NOTE]  
>  個別のファイルは、データベース バックアップから復元できますが、データベース バックアップからファイルの検索と復元を行うと、ファイル バックアップから行う場合よりも時間がかかります。  
  
### <a name="file-backups-and-the-simple-recovery-model"></a>ファイル バックアップと単純復旧モデル  
 単純復旧モデルでは、読み取りと書き込みが可能なファイルはすべてまとめてバックアップする必要があります。 これにより、データベースを一貫性のある時点に復元できます。 読み取りと書き込みが可能なファイルまたはファイル グループを個別に指定するのではなく、READ_WRITE_FILEGROUPS オプションを使用します。 このオプションにより、読み取りと書き込みが可能なすべてのファイル グループがデータベースにバックアップされます。 READ_WRITE_FILEGROUPS を指定して作成されたファイル グループは、部分バックアップと呼ばれます。 詳細については、「[部分バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/partial-backups-sql-server.md)」を参照してください。  
  
### <a name="file-backups-and-the-full-recovery-model"></a>ファイル バックアップと完全復旧モデル  
 完全復旧モデルでは、バックアップ ストラテジの残りの部分に関係なく、トランザクション ログをバックアップする必要があります。 ファイルの完全バックアップの完全なセットと、ファイル バックアップのすべての範囲に対応したログ バックアップを併用することで、データベースの完全バックアップに等しくなります。  
  
 ファイル バックアップとログ バックアップだけを使用したデータベースの復元は、複雑になることがあります。 したがって、可能であれば、データベースの完全バックアップを実行して、最初のファイル バックアップの前にログ バックアップを開始することをお勧めします。 次の図は、データベースが作成された直後 (時間 t0) に、データベースの完全バックアップを行う (時間 t1) という方法を示しています。 この最初のデータベース バックアップによって、トランザクション ログのバックアップを開始できるようになります。 トランザクション ログのバックアップは、設定された間隔で実行するようにスケジュールが設定されています。 ファイル バックアップは、データベースに対するビジネス要件を最もよく満たす間隔で実行されます。 この図は、一度に 1 つずつバックアップされる 4 つのファイル グループのそれぞれを示します。 バックアップされる順序 (A、C、B、A) は、データベースのビジネス要件を反映しています。  
  
 ![データベース、ファイル、ログのバックアップを結合する方法](../../relational-databases/backup-restore/media/bnr-rmfull-3-fulldb-filegrps-log-backups.gif "データベース、ファイル、ログのバックアップを結合する方法")  
  
> [!NOTE]  
>  完全復旧モデルで読み取り/書き込みファイルのバックアップを復元する際には、そのファイルとデータベースのそれ以外の部分との一貫性を確保するために、トランザクション ログをロールフォワードする必要があります。 トランザクション ログのバックアップをロールフォワードする数が多くなりすぎないようにするには、ファイルの差分バックアップの使用を検討してください。 詳細については、「 [差分バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)」を参照してください。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 関連タスク  
 **ファイルまたはファイル グループのバックアップを作成するには**  
  
-   [ファイルおよびファイル グループのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
> [!NOTE]  
>  ファイル バックアップはメンテナンス プラン ウィザードでサポートされません。  
  
## <a name="see-also"></a>参照  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [バックアップの概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [バックアップと復元: 相互運用性と共存 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-and-restore-interoperability-and-coexistence-sql-server.md)   
 [差分バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [ファイルの復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [ファイルの復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [Online Restore &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [段階的な部分復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
