---
title: バックアップの圧縮 (SQL Server) | Microsoft Docs
description: 制限、パフォーマンスのトレードオフ、バックアップの圧縮の構成、圧縮率など、SQL Server バックアップの圧縮について説明します。
ms.custom: ''
ms.date: 07/08/2020
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], backup compression
- backup compression [SQL Server], about backup compression
- compression [SQL Server], backup compression
- backups [SQL Server], compression
- backing up [SQL Server], backup compression
- backup compression [SQL Server]
ms.assetid: 05bc9c4f-3947-4dd4-b823-db77519bd4d2
author: cawrites
ms.author: chadam
ms.openlocfilehash: c39b9520bebf08cf523bece5b2c9bab78675138d
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96129345"
---
# <a name="backup-compression-sql-server"></a>バックアップの圧縮 (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、バックアップの圧縮の制限、パフォーマンス面のトレードオフ、バックアップの圧縮の構成、圧縮比率など、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップの圧縮について説明します。  バックアップの圧縮は、次の [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] エディションでサポートされています (Enterprise、Standard、Developer)。  圧縮されたバックアップは、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降の各エディションで復元できます。 
 
  
##  <a name="benefits"></a><a name="Benefits"></a> 利点  
  
-   圧縮されたバックアップは、同じデータの圧縮されていないバックアップよりも小さいため、バックアップを圧縮すると一般には必要なデバイス I/O が少なくなり、通常はバックアップの速度が大きく短縮されます。  
  
     詳細については、このトピックの「 [バックアップの圧縮がパフォーマンスに与える影響](#PerfImpact)」を参照してください。  
  
  
##  <a name="restrictions"></a><a name="Restrictions"></a> 制限  
 圧縮されたバックアップには次の制限が適用されます。  
  
-   圧縮されたバックアップと圧縮されていないバックアップを 1 つのメディア セット内に共存させることはできません。  
  
-   以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、圧縮されたバックアップを読み取ることができません。  
  
-   圧縮された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップのテープを複数の Ntbackup で共有することはできません。  
  
  
##  <a name="performance-impact-of-compressing-backups"></a><a name="PerfImpact"></a> バックアップの圧縮がパフォーマンスに与える影響  
 既定の設定では、圧縮によって CPU 使用率が著しく増加し、圧縮処理によって CPU がさらに消費されるために、同時に実行される操作が悪影響を受ける場合があります。 このため、[リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)によって CPU 使用率が制限されるセッションでは、優先度の低い圧縮バックアップを作成することができます。 詳細については、「 [リソース ガバナーを使用してバックアップの圧縮による CPU 使用率を制限する方法 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)」を参照してください。  
  
 バックアップ I/O パフォーマンスの実態を把握するためには、次のようなパフォーマンス カウンターを評価することで、デバイスに対するバックアップ I/O を特定できます。  
  
-   物理ディスク カウンターなどの Windows I/O パフォーマンス カウンター  
  
-   **SQLServer:Backup Device** オブジェクトの [Device Throughput Bytes/sec](../../relational-databases/performance-monitor/sql-server-backup-device-object.md) カウンター  
  
-   **SQLServer:Databases** オブジェクトの [Backup/Restore Throughput/sec](../../relational-databases/performance-monitor/sql-server-databases-object.md) カウンター  
  
 Windows カウンターの詳細については、Windows ヘルプを参照してください。 SQL Server カウンターの使用方法の詳細については、「 [SQL Server オブジェクトの使用](../../relational-databases/performance-monitor/use-sql-server-objects.md)」をご覧ください。  
  
   
##  <a name="calculate-the-compression-ratio-of-a-compressed-backup"></a><a name="CompressionRatio"></a> 圧縮されたバックアップの圧縮比率の計算  
 バックアップの圧縮比率を計算するには、 **backupset** 履歴テーブルの **backup_size** 列と [compressed_backup_size](../../relational-databases/system-tables/backupset-transact-sql.md) 列にある値を次のように使用します。  
  
 **backup_size**:**compressed_backup_size**  
  
 たとえば、圧縮比率が 3:1 の場合、ディスク領域を約 66% 節約できることを意味します。 これらの列に対するクエリを実行するには、次の Transact-SQL ステートメントを使用できます。  
  
```sql  
SELECT backup_size/compressed_backup_size FROM msdb..backupset;  
```  
  
 圧縮されたバックアップの圧縮比率は、圧縮対象のデータによって異なります。 実際の圧縮比率は、さまざまな要因の影響を受けます。 主な要因は次のとおりです。  
  
-   データの型  
  
     文字データは、他のデータ型よりも圧縮されます。  
  
-   ページ上の各行のデータの一貫性  
  
     一般に、ページ内の複数の行でフィールドに同じ値が格納されている場合、その値が大幅に圧縮される可能性があります。 これに対して、ランダムなデータが格納されたデータベースや、各ページにサイズの大きい行が 1 つだけ含まれているデータベースの場合、圧縮されたバックアップは、圧縮されていないバックアップとそれほど変わらないサイズになります。  
  
-   データが暗号化されているかどうか  
  
     暗号化されたデータは、暗号化されていない同等のデータより、圧縮比率が大幅に下がります。 たとえば、データが Always Encrypted またはその他のアプリケーション レベルの暗号化を使用して列レベルで暗号化されている場合は、バックアップを圧縮しても、サイズの大幅な削減には至らない可能性があります。

     Transparent Data Encryption (TDE) を使用して暗号化されたデータベースの圧縮に関する詳細については、「[TDE を使用したバックアップの圧縮](#backup-compression-with-tde)」を参照してください。

-   データベースが圧縮されているかどうか  
  
     データベースが圧縮されている場合、バックアップを圧縮しても、サイズが大幅に減少することはありません。  

## <a name="backup-compression-with-tde"></a>TDE を使用したバックアップの圧縮

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降では、`MAXTRANSFERSIZE` を **65536 (64 KB)** より大きく設定することにより、最初にページを暗号化解除し、圧縮してから再度暗号化する、[Transparent Data Encryption (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) で暗号化されたデータベースの最適化された圧縮アルゴリズムが有効になります。 `MAXTRANSFERSIZE` が指定されていない場合、または `MAXTRANSFERSIZE = 65536` (64 KB) が使用される場合、TDE で暗号化されたデータベースでのバックアップの圧縮では暗号化されたページが直接圧縮され、適切な圧縮比率が得られない可能性があります。 詳細については、「[Backup Compression for TDE-enabled Databases](/archive/blogs/sqlcat/sqlsweet16-episode-1-backup-compression-for-tde-enabled-databases)」 (TDE が有効になっているデータベースのバックアップの圧縮) を参照してください。

[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CU5 以降では、この最適化された圧縮アルゴリズムを TDE で有効にするために `MAXTRANSFERSIZE` を設定する必要がなくなりました。 バックアップ コマンドに `WITH COMPRESSION` が指定されている場合、または *backup compression default* サーバー構成が 1 に設定されている場合、最適化されたアルゴリズムを有効にするために、`MAXTRANSFERSIZE` は自動的に 128 K に増加されます。 バックアップ コマンドに `MAXTRANSFERSIZE` が 64 K より大きい値で指定されている場合は、指定された値が使用されます。 言い換えると、SQL Server によって値は増加されるのみであり、自動的に減少されることはありません。 `MAXTRANSFERSIZE = 65536` で TDE で暗号化されたデータベースをバックアップする必要がある場合は、`WITH NO_COMPRESSION` を指定するか、*backup compression default* サーバー構成が 0 に設定されていることを確認する必要があります。

詳細については、「[BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)」を参照してください。

##  <a name="allocation-of-space-for-the-backup-file"></a><a name="Allocation"></a> バックアップ ファイルの使用領域の割り当て  
 圧縮されたバックアップの場合、最終的なバックアップ ファイルのサイズは、データをどれくらい圧縮できるかによりますが、それはバックアップ操作が終了するまで不明です。  そのため、既定では、圧縮を使用してデータベースをバックアップする場合、データベース エンジンはバックアップ ファイルのために事前割り当てアルゴリズムを使用します。 このアルゴリズムでは、バックアップ ファイルに、データベースのサイズに対する定義済みの割合のサイズを事前に割り当てます。 バックアップ操作中に、より多くの領域が必要になった場合は、データベース エンジンによってファイルが拡張されます。 バックアップ操作の終了時の最終的なサイズが、割り当てられた領域のサイズを下回る場合は、データベース エンジンによってファイルがバックアップの実際の最終的なサイズに縮小されます。  
  
 バックアップ ファイルが、最終的なサイズに達するために必要な分だけを拡張できるようにするには、トレース フラグ 3042 を使用します。 トレース フラグ 3042 は、バックアップ操作が既定のバックアップ圧縮の事前割り当てアルゴリズムを使用しないようにします。 このトレース フラグは、圧縮されたバックアップに実際に必要なサイズだけを割り当てることによって、容量を節約する必要がある場合に便利です。 ただし、このトレース フラグを使用すると、わずかなパフォーマンスの低下 (バックアップ操作の期間が長くなる可能性) が発生することがあります。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 関連タスク  
  
-   [バックアップの圧縮の構成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/configure-backup-compression-sql-server.md)  
  
-   [backup compression default サーバー構成オプションの表示または構成](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
-   [リソース ガバナーを使用してバックアップの圧縮による CPU 使用率を制限する方法 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [DBCC TRACEON &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)  
  
-   [DBCC TRACEOFF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)  
  
## <a name="see-also"></a>参照  
 [バックアップの概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [トレース フラグ &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
  
