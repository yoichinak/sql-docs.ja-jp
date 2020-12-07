---
description: database_mirroring (Transact-sql)
title: database_mirroring (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_mirroring
- database_mirroring
- sys.database_mirroring_TSQL
- database_mirroring_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_mirroring catalog view
ms.assetid: 480de2b0-2c16-497d-a6a3-bf7f52a7c9a0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cf5b55565a97669b78deedeb2487881e2aa1d808
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546855"
---
# <a name="sysdatabase_mirroring-transact-sql"></a>database_mirroring (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  のインスタンス内のデータベースごとに1行のデータを格納 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。 データベースがオンラインでないかデータベース ミラーリングが有効でない場合、database_id を除くすべての列の値は NULL になります。  
  
 master または tempdb 以外のデータベースの行を表示するには、データベースの所有者であるか、少なくとも ALTER ANY DATABASE または VIEW ANY DATABASE のサーバー レベルの権限が与えられているか、master データベースの CREATE DATABASE 権限が与えられている必要があります。 ミラーデータベースで NULL 以外の値を表示するには、 **sysadmin** 固定サーバーロールのメンバーである必要があります。  
  
> [!NOTE]  
>  データベースがミラーリングに参加していない場合は、"mirroring_" というプレフィックスが付いたすべての列が NULL になります。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|データベースの ID です。 のインスタンス内で一意です [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**mirroring_guid**|**uniqueidentifier**|ミラーリングパートナーシップの ID。<br /><br /> NULL = データベースにアクセスできないか、ミラー化されていません。<br /><br /> 注: データベースがミラーリングに参加していない場合は、"mirroring_" というプレフィックスが付いたすべての列が NULL になります。|  
|**mirroring_state**|**tinyint**|ミラーデータベースとデータベースミラーリングセッションの状態。<br /><br /> 0 = 中断<br /><br /> 1 = 他のパートナーから切断<br /><br /> 2 = 同期中<br /><br /> 3 = フェールオーバー保留中<br /><br /> 4 = 同期済み<br /><br /> 5 = パートナーが同期されていません。 現在、フェールオーバーは実行できません。<br /><br /> 6 = パートナーが同期されています。 フェールオーバーが可能な可能性があります。 フェールオーバーの要件の詳細については、「 [データベースミラーリングの動作モード](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)」を参照してください。<br /><br /> NULL= データベースにアクセスできないか、ミラー化されていません。|  
|**mirroring_state_desc**|**nvarchar(60)**|ミラーデータベースとデータベースミラーリングセッションの状態の説明。次のいずれかを指定できます。<br /><br /> DISCONNECTED<br /><br /> SYNCHRONIZED<br /><br /> SYNCHRONIZING<br /><br /> PENDING_FAILOVER<br /><br /> SUSPENDED<br /><br /> 非同期<br /><br /> SYNCHRONIZED<br /><br /> NULL<br /><br /> 詳細については、「[ミラーリング状態 &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)」を参照してください。|  
|**mirroring_role**|**tinyint**|データベース ミラーリング セッションにおけるローカル データベースの現在のロールです。<br /><br /> 1 = プリンシパル<br /><br /> 2 = ミラー<br /><br /> NULL= データベースにアクセスできないか、ミラー化されていません。|  
|**mirroring_role_desc**|**nvarchar(60)**|ミラー化におけるローカル データベースのロールの説明。次のいずれかになります。<br /><br /> PRINCIPAL<br /><br /> MIRROR|  
|**mirroring_role_sequence**|**int**|フェールオーバーまたは強制されたサービスにより、ミラーリングパートナーがプリンシパルロールとミラーロールを切り替えた回数。<br /><br /> NULL= データベースにアクセスできないか、ミラー化されていません。|  
|**mirroring_safety_level**|**tinyint**|ミラーデータベースでの更新の安全性設定:<br /><br /> 0 = 状態不明<br /><br /> 1 = オフ [非同期]<br /><br /> 2 = 完全 [同期]<br /><br /> NULL= データベースにアクセスできないか、ミラー化されていません。|  
|**mirroring_safety_level_desc**|**nvarchar(60)**|ミラー データベースの更新に関するトランザクションの安全性の設定。次のいずれかになります。<br /><br /> UNKNOWN<br /><br /> OFF<br /><br /> FULL<br /><br /> NULL|  
|**mirroring_safety_sequence**|**int**|トランザクションの安全性レベルの変更のシーケンス番号を更新します。<br /><br /> NULL= データベースにアクセスできないか、ミラー化されていません。|  
|**mirroring_partner_name**|**nvarchar(128)**|データベース ミラーリング パートナーのサーバー名。<br /><br /> NULL= データベースにアクセスできないか、ミラー化されていません。|  
|**mirroring_partner_instance**|**nvarchar(128)**|他のパートナーに対するインスタンス名とコンピューター名。 クライアントがプリンシパルサーバーになると、この情報がパートナーに接続する必要があります。<br /><br /> NULL= データベースにアクセスできないか、ミラー化されていません。|  
|**mirroring_witness_name**|**nvarchar(128)**|データベース ミラーリング監視サーバーのサーバー名。<br /><br /> NULL = ミラーリング監視サーバーが存在しません。|  
|mirroring_witness_state|**tinyint**|データベースのデータベースミラーリングセッションにおけるミラーリング監視サーバーの状態。次のいずれかを指定できます。<br /><br /> 0 = 不明<br /><br /> 1 = 接続済み<br /><br /> 2 = 切断<br /><br /> NULL = ミラーリング監視サーバーが存在しない、データベースがオンラインではない、またはデータベースがミラー化されていません。|  
|**mirroring_witness_state_desc**|**nvarchar(60)**|状態の説明。次のいずれかを指定できます。<br /><br /> UNKNOWN<br /><br /> CONNECTED<br /><br /> DISCONNECTED<br /><br /> NULL|  
|**mirroring_failover_lsn**|**numeric(25,0)**|両方のパートナーのディスクに書き込まれることが保証されている最新のトランザクションログレコードのログシーケンス番号 (LSN)。 フェールオーバー後、 **mirroring_failover_lsn** は、新しいミラーサーバーが新しいミラーデータベースと新しいプリンシパルデータベースとの同期を開始するときに、パートナーによってパートナーによって使用されます。|  
|**mirroring_connection_timeout**|**int**|ミラーリング接続のタイムアウト (秒)。 これは、パートナーまたはミラーリング監視サーバーからの返信を待機する秒数です。この時間を過ぎるとパートナーまたはミラーリング監視サーバーは使用できないものと見なされます。 タイムアウトの既定値は 10 秒です。<br /><br /> NULL= データベースにアクセスできないか、ミラー化されていません。|  
|**mirroring_redo_queue**|**int**|ミラー化で再実行されるログの最大サイズ。 mirroring_redo_queue_type が既定の UNLIMITED に設定されている場合、この列は NULL になります。 データベースがオンラインでない場合も、この列は NULL になります。<br /><br /> 上記以外の場合、この列にはログの最大サイズ (MB 単位) が格納されます。 最大値に達すると、ミラーサーバーが追いつくときに、ログがプリンシパルで一時的に停止します。 この機能は、フェールオーバー時間を制限します。<br /><br /> 詳しくは、「 [役割の交代中に発生するサービスの中断時間の算出 &#40;データベース ミラーリング&#41;](../../database-engine/database-mirroring/estimate-the-interruption-of-service-during-role-switching-database-mirroring.md)という処理により、一般的にプリンシパルとミラーの役割を相互交換できます。|  
|**mirroring_redo_queue_type**|**nvarchar(60)**|無制限は、ミラーリングによって再実行キューが妨げられないことを示します。 これが既定の設定です。<br /><br /> メガバイト単位での再実行キューの最大サイズの MB。 キューのサイズがキロバイトまたはギガバイトとして指定されている場合、は [!INCLUDE[ssDE](../../includes/ssde-md.md)] 値をメガバイトに変換します。<br /><br /> データベースがオンラインでない場合、この列は NULL になります。|  
|**mirroring_end_of_log_lsn**|**numeric(25,0)**|ディスクにフラッシュされたローカルのログ末尾。 これは、ミラーサーバーから書き込まれた LSN に相当します (「 **mirroring_failover_lsn** 」列を参照してください)。|  
|**mirroring_replication_lsn**|**numeric(25,0)**|レプリケーションが送信できる最大 LSN。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [database_mirroring_witnesses &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)   
 [データベースとファイルのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [SQL Server システム カタログに対するクエリに関してよく寄せられる質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
