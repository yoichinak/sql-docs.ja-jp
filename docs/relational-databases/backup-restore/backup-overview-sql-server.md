---
title: バックアップの概要 (SQL Server) | Microsoft Docs
description: バックアップの種類と制限、バックアップ デバイスとバックアップ メディアなど、SQL Server のバックアップ コンポーネントについて説明します。
ms.custom: ''
ms.date: 07/15/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- tables [SQL Server], backing up data
- backups [SQL Server]
- database backups [SQL Server]
- backup types [SQL Server]
- data backups [SQL Server]
- backing up tables [SQL Server]
- database restores [SQL Server], backups
- backing up [SQL Server], about backing up
- restoring [SQL Server], backup types
- backups [SQL Server], about
- backups [SQL Server], table-level backups unsupported
ms.assetid: 09a6e0c2-d8fd-453f-9aac-4ff24a97dc1f
author: cawrites
ms.author: chadam
ms.openlocfilehash: 08a9360ae2f9fa7f1ff109b4d9b6075dd5536481
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96129321"
---
# <a name="backup-overview-sql-server"></a>Backup Overview (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバックアップ コンポーネントについて説明します。 データを保護するためには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースをバックアップすることが不可欠です。 ここでは、バックアップの種類およびバックアップの制限事項について説明します。 また、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバックアップ デバイスとバックアップ メディアについても取り上げます。  
  
  
## <a name="terms"></a>用語
 
 **バックアップ (back up) (動詞)**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースまたはそのトランザクション ログからバックアップ デバイス (ディスクなど) にデータまたはログ レコードをコピーすることによって、データ バックアップまたはログ バックアップを作成します。  
  
**バックアップ (backup) (名詞)**  
 障害の発生後、データの復元と復旧に使用できる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データのコピー。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データのバックアップは、データベース レベル、あるいは 1 つまたは複数のデータベース ファイル (ファイル グループ) レベルで作成されます。 テーブルレベルのバックアップは作成できません。 完全復旧モデルでは、データのバックアップに加えて、トランザクション ログのバックアップを作成する必要があります。  
  
**[復旧モデル (recovery model)](../../relational-databases/backup-restore/recovery-models-sql-server.md)**  
 データベースのトランザクション ログのメンテナンスを制御するデータベース プロパティ。 復旧モデルの種類は、単純、完全、および一括ログの 3 種類です。 データベースのバックアップと復元の要件は、その復旧モデルによって決まります。  
  
 **[復元 (restore)](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)**  
 データを直近の状態まで戻す複数フェーズから成る処理。指定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップからすべてのデータおよびログ ページを指定されたデータベースにコピーするフェーズと、バックアップにログとして記録されているすべてのトランザクションをロールフォワード (ログに記録されている変更を適用) するフェーズとで構成されます。  
  
 ## <a name="types-of-backups"></a>バックアップの種類  
  
 **[コピーのみのバックアップ (copy-only backup)](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の通常のバックアップ シーケンスから独立した特殊な用途のバックアップ。  
  
**データ バックアップ (data backup)**    
 データのバックアップ。データベース全体 (データベース バックアップ)、データベースの一部 (部分バックアップ)、または一連のデータ ファイルやファイルグループ (ファイル バックアップ) の形式で存在します。  
  
**[データベース バックアップ (database backup)](../../relational-databases/backup-restore/full-database-backups-sql-server.md)**  
 データベースのバックアップ。 データベースの完全バックアップは、バックアップが完了した時点のデータベース全体を表します。 差分データベース バックアップには、最新の完全バックアップ以降に行われたデータベースへの変更のみが含まれます。  
  
 **[差分バックアップ (differential backup)](../../relational-databases/backup-restore/full-database-backups-sql-server.md)**  
 データベース全体、データベースの一部、または一連のデータ ファイル (またはファイル グループ) の最新の完全バックアップ ( *差分ベース*) をベースとし、その差分ベース以後に変更されたデータ エクステントのみを含んだデータ バックアップ。  
  
 部分的な差分バックアップでは、ファイル グループのデータのうち、前回の部分バックアップ以降に変更されたデータだけが記録されます。この前回の部分バックアップを差分に対するベースと呼びます。  
  
**完全バックアップ (full backup)**  
 特定のデータベース (または一連のファイルやファイル グループ) 内のデータがすべて含まれ、さらに、データを復旧するために必要なログも含んだデータ バックアップ。  
  
**[ログ バックアップ (log backup)](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)**  
 前回のログ バックアップでバックアップされなかったすべてのログ レコードを含むトランザクション ログのバックアップ (完全復旧モデル)。  
  
 **[ファイル バックアップ (file backup)](../../relational-databases/backup-restore/full-file-backups-sql-server.md)**  
 1 つ以上のデータベース ファイルまたはファイル グループから成るバックアップ。  
  
 **[部分バックアップ (partial backup)](../../relational-databases/backup-restore/partial-backups-sql-server.md)**  
 データベースの一部のファイル グループのデータのみを格納します。プライマリ ファイル グループ、すべての読み取り/書き込みファイル グループのほか、必要に応じて指定した読み取り専用ファイルが含まれます。  
  
## <a name="backup-media-terms-and-definitions"></a>バックアップ メディアの用語と定義  
  
 **[バックアップ デバイス (backup device)](../../relational-databases/backup-restore/backup-devices-sql-server.md)**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップの書き込みと復元に使用されるディスクまたはテープ デバイス。 SQL Server のバックアップは、Azure Blob Storage サービスに書き込むこともできます。バックアップ先とバックアップ ファイルの名前を指定するには **URL** 形式を使用します。 詳細については、「[Windows Azure BLOB ストレージ サービスを使用した SQL Server のバックアップと復元](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)」を参照してください。  
  
 **[バックアップ メディア (backup media)](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)**  
 バックアップの書き込み先となる 1 つまたは複数のテープまたはディスク ファイル。  
  
 **[バックアップ セット (backup set)](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)**  
 正常に完了したバックアップ操作によってメディア セットに追加されるバックアップ コンテンツ。  
  
 **[メディア ファミリ (media family)](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)**  
 ミラー化されていない単一のデバイスまたはメディア セット内のミラー化されている一連のデバイスで作成されたバックアップ。  
  
 **[メディア セット (media set)](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)**  
 テープやディスク ファイルなどのバックアップ メディアに順番を付けてまとめたもの。バックアップ メディアには、1 回以上のバックアップ操作によって、固定型の複数のバックアップ デバイスを使用して書き込まれます。  
  
 **[ミラー化メディア セット (mirrored media set)](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)**  
 メディア セットの複数のコピー (ミラー)。  
  
##  <a name="backup-compression"></a><a name="BackupCompression"></a> バックアップ圧縮  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 以降のバージョンでは、バックアップの圧縮がサポートされ、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンでは、圧縮されたバックアップを復元することができます。 詳細については、「[バックアップの圧縮 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md)」を参照してください。  
  
##  <a name="backup-operations-restrictions"></a><a name="Restrictions"></a>  バックアップ操作の制限 
 オンラインでデータベースを使用中であってもバックアップを行うことができます。 ただし、次の制限事項があります。  
  
### <a name="cannot-back-up-offline-data"></a>オフライン データをバックアップできません。  
 オフライン データを暗黙的または明示的に参照するバックアップ操作は失敗します。 よく見られる例を次に示します。  
  
-   データベースの完全バックアップを要求したが、データベースのいずれかのファイル グループがオフラインである場合。 データベースの完全バックアップにはすべてのファイル グループが暗黙的に含まれるため、この操作は失敗します。  
  
     このデータベースをバックアップするには、ファイル バックアップを使用し、オンラインのファイル グループのみを指定します。  
  
-   部分バックアップを要求したが、読み取り/書き込みファイル グループがオフラインの場合。 部分バックアップにはすべての読み取り/書き込みファイル グループが必要なので、この操作は失敗します。  
  
-   特定のファイルのファイル バックアップを要求したが、いずれかのファイルがオンラインでない場合。 操作は失敗します。 オンライン ファイルをバックアップするには、ファイル一覧からオフライン ファイルを削除し、操作を繰り返します。  
  
 通常、1 つ以上のデータ ファイルを使用できない状態でも、ログ バックアップは続行できます。 ただし、一括ログ復旧モデルで行われた一括ログ変更がいずれかのファイルに含まれている場合、バックアップを続行するにはすべてのファイルをオンラインにする必要があります。  
  
### <a name="concurrency-restrictions"></a>コンカレンシーの制限事項   
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、オンライン バックアップを使って、使用中のデータベースをバックアップできます。 バックアップ中はほとんどの操作が可能です。たとえば、INSERT、UPDATE、または DELETE ステートメントはバックアップ操作中でも使用できます。 ただし、データベースの作成中または削除中にバックアップ操作を開始しようとすると、データベースの作成または削除操作が完了するまで、またはバックアップがタイムアウトするまで、バックアップ操作が待機します。  
  
 データベース バックアップやトランザクション ログ バックアップ中に、次の操作を実行することはできません。  
  
-   ADD FILE または REMOVE FILE のいずれかのオプションが指定された ALTER DATABASE ステートメントなどのファイル管理操作。  
  
-   データベースまたはファイルの圧縮操作。 これには自動圧縮操作も含まれます。  
  
-   バックアップ操作実行中にデータベース ファイルを作成または削除しようとすると、作成操作または削除操作は失敗します。  
  
 バックアップ操作がファイル管理操作または圧縮操作の実行と重複すると、競合が発生します。 競合する操作のどちらが先に開始されたかにかかわらず、1 つ目の操作によって設定されたロックのタイムアウトを 2 つ目の操作が待機します(タイムアウト期間はセッション タイムアウトの設定によって制御されます)。ロックがタイムアウト期間内に解放されると、2 番目の操作が開始されます。 ロックがタイムアウトになると、2 番目の操作は実行されません。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 関連タスク  
 **バックアップ デバイスとバックアップ メディア**  
  
-   [ディスク ファイルの論理バックアップ デバイスの定義 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [テープ ドライブの論理バックアップ デバイスの定義 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [バックアップ先としてディスクまたはテープを指定する &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [バックアップ デバイスの削除 &#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)  
  
-   [バックアップの有効期限の設定 &#40;SQL Server&#41;](../../relational-databases/backup-restore/set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [バックアップ テープまたはバックアップ ファイルの内容の表示 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [バックアップ セットに含まれているデータ ファイルおよびログ ファイルの表示 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [論理バックアップ デバイスのプロパティと内容の表示 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [デバイスからのバックアップ復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)  
  
-   [チュートリアル:Azure Blob Storage サービスへの SQL Server のバックアップと復元](~/relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
 **バックアップを作成する**  
  
> [!NOTE]  
>  部分、またはコピーのみのバックアップでは、[!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md) ステートメントにそれぞれ PARTIAL オプションまたは COPY_ONLY オプションを使う必要があります。  
  
-   [データベースの完全バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [ファイルおよびファイル グループのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [データベースの差分バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
-   [データベースが破損したときのトランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
-   [バックアップ中または復元中にバックアップ チェックサムを有効または無効にする &#40;SQL Server&#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
-   [バックアップまたは復元の操作をエラー発生後に続行するか停止するかを指定する &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  
-   [リソース ガバナーを使用してバックアップの圧縮による CPU 使用率を制限する方法 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [チュートリアル:Azure Blob Storage サービスへの SQL Server のバックアップと復元](~/relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
## <a name="and-more"></a>その他 
 [SQL Server データベースのバックアップと復元](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [復元と復旧の概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [メンテナンス プラン](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [トランザクション ログ &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [復旧モデル &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
  
