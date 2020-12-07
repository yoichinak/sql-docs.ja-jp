---
description: sys.syslockinfo (Transact-SQL)
title: sys.syslockinfo (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syslockinfo_TSQL
- sys.syslockinfo_TSQL
- sys.syslockinfo
- syslockinfo
dev_langs:
- TSQL
helpviewer_keywords:
- syslockinfo system table
- sys.syslockinfo compatibility view
ms.assetid: d8cae434-807a-473e-b94f-f7a0e1b2daf0
author: rothja
ms.author: jroth
ms.openlocfilehash: 9714fab678f8466daf76d5963e1383b5e7d2dc52
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490062"
---
# <a name="syssyslockinfo-transact-sql"></a>sys.syslockinfo (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  すべての許可、変換、および待機中のロック要求に関する情報を格納します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
> [!IMPORTANT]  
>  この機能は、以前のバージョンのから変更されてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 詳細については、「 [SQL Server 2016 のデータベースエンジン機能における重大な変更](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)」を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**rsc_text**|**nchar(32)**|ロックリソースの説明テキスト。 リソース名の一部が含まれています。|  
|**rsc_bin**|**binary(16)**|バイナリロックリソース。 ロック マネージャーに格納されている実際のロック リソースが含まれます。 この列は、独自に書式設定されたロックリソースを生成するためのロックリソース形式を認識するツールや、 **syslockinfo**での自己結合を実行するために用意されています。|  
|**rsc_valblk**|**binary(16)**|ロック値ブロック。 リソースの種類によっては、ロック マネージャーによってハッシュされず、特定のロック リソースの所有権が判断されないロック リソース内の追加データが含まれることがあります。 たとえば、ページ ロックは特定のオブジェクト ID で所有されません。 ロックのエスカレーションなどの目的があるためです。 ただし、ロック値ブロックにページ ロックのオブジェクト ID が含まれることがあります。|  
|**rsc_dbid**|**smallint**|リソースに関連付けられているデータベース ID。|  
|**rsc_indid**|**smallint**|該当する場合、リソースに関連付けられているインデックス ID。|  
|**rsc_objid**|**int**|リソースに関連付けられているオブジェクト ID (該当する場合)。|  
|**rsc_type**|**tinyint**|リソースの種類:<br /><br /> 1 = NULL リソース (未使用)<br /><br /> 2 = データベース<br /><br /> 3 = ファイル<br /><br /> 4 = インデックス<br /><br /> 5 = テーブル<br /><br /> 6 = ページ<br /><br /> 7 = キー<br /><br /> 8 = エクステント<br /><br /> 9 = RID (行 ID)<br /><br /> 10 = アプリケーション|  
|**rsc_flag**|**tinyint**|内部リソース フラグ。|  
|**req_mode**|**tinyint**|ロック要求モード。 この列は、要求元のロックモードであり、許可されたモード、または変換モードまたは待機モードのいずれかを表します。<br /><br /> 0 = NULL。 リソースへのアクセス権は付与されません。 プレースホルダーとして機能します。<br /><br /> 1 = sch-m (スキーマの安定性)。 スキーマ要素に対するスキーマの安定性ロックを保持しているセッションがある間、テーブルやインデックスなどのスキーマ要素が削除されないようにします。<br /><br /> 2 = Sch-M (スキーマ修正)。 は、指定されたリソースのスキーマを変更する必要があるすべてのセッションによって保持される必要があります。 指定されたオブジェクトを参照している他のセッションがないことを確認します。<br /><br /> 3 = S (共有)。 保持しているセッションに、リソースへの共有アクセスが許可されます。<br /><br /> 4 = U (更新)。 リソース上で取得された更新ロックが、最終的に更新されることが許可されます。 これは、後で更新される可能性があるリソースが複数のセッションによってロックされるとき、一般的な形式のデッドロックが発生するのを防止するために使用します。<br /><br /> 5= X (排他)。 保持しているセッションで、リソースへの排他アクセスが許可されます。<br /><br /> 6 = IS (共有インテント)。 ロック階層の下位のリソースに S ロックを配置することを示します。<br /><br /> 7= IU (更新インテント)。 ロック階層の下位のリソースに U ロックを設定するよう指定します。<br /><br /> 8 = IX (排他インテント)。 ロック階層の下位のリソースに X ロックを設定するよう指定します。<br /><br /> 9 = SIU (共有更新インテント)。 ロック階層の下位のリソースに更新ロックを設定する目的で、リソースへの共有アクセスを指定します。<br /><br /> 10 = 6 (共有インテント排他)。 ロック階層内の下位のリソースに排他ロックを取得する目的で、リソースへの共有アクセスを示します。<br /><br /> 11 = IX (更新排他インテント)。 ロック階層の下位のリソースに排他ロックを設定する目的で、リソースに保持する更新ロックを指定します。<br /><br /> 12 = BU。 一括操作で使用されます。<br /><br /> 13 = RangeS_S (共有キー範囲と共有リソース ロック)。 シリアル化可能な範囲スキャンを示します。<br /><br /> 14 = RangeS_U (共有キー範囲と更新リソース ロック)。 シリアル化可能な更新プログラムのスキャンを示します。<br /><br /> 15 = RangeI_N (挿入キー範囲と NULL リソース ロック)。 インデックスに新しいキーを挿入する前に範囲をテストするために使用されます。<br /><br /> 16 = RangeI_S。 RangeI_N と S ロックの重なりによって作成されるキー範囲変換ロック。<br /><br /> 17 = RangeI_U。 RangeI_N と U ロックの重複によって作成されるキー範囲変換ロック。<br /><br /> 18 = RangeI_X。 RangeI_N と X ロックの重なりによって作成されるキー範囲変換ロック。<br /><br /> 19 = RangeX_S。 RangeI_N と RangeS_S の重なりによって作成されるキー範囲変換ロック。 固定.<br /><br /> 20 = RangeX_U。 RangeI_N と RangeS_U ロックの重なりによって作成されるキー範囲変換ロックです。<br /><br /> 21 = RangeX_X (排他キー範囲と排他リソースロック)。 範囲内のキーを更新する場合に使用する変換ロックです。|  
|**req_status**|**tinyint**|ロック要求の状態。<br /><br /> 1 = 許可<br /><br /> 2 = 変換<br /><br /> 3 = 待機中|  
|**req_refcnt**|**smallint**|ロック参照カウント。 トランザクションが特定のリソースのロックを要求するたびに、参照カウントがインクリメントされます。 参照カウントが0になるまで、ロックを解放できません。|  
|**req_cryrefcnt**|**smallint**|将来使用するために予約されています。 常に0に設定されます。|  
|**req_lifetime**|**int**|ロックの有効期限のビットマップ。 特定のクエリ処理方法の実行中は、クエリ プロセッサによってクエリの特定のフェーズが完了するまで、リソース上のロックは保持される必要があります。 ロックの有効期間のビットマップは、クエリの特定のフェーズの実行が終了したときに解放できるロックのグループを示すために、クエリプロセッサおよびトランザクションマネージャーによって使用されます。 ビットマップ内の特定のビットは、参照カウントが0の場合でも、トランザクションの終了まで保持されるロックを示すために使用されます。|  
|**req_spid**|**int**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ロックを要求しているセッションの内部プロセス ID。|  
|**req_ecid**|**int**|実行コンテキスト ID (関連する d)。 並列操作内のどのスレッドが特定のロックを所有しているかを示すために使用されます。|  
|**req_ownertype**|**smallint**|ロックに関連付けられているオブジェクトの種類。<br /><br /> 1 = トランザクション<br /><br /> 2 = カーソル<br /><br /> 3 = セッション<br /><br /> 4 = 前回のセッション<br /><br /> 3 と 4 は、特殊なセッション ロックで、それぞれデータベースとファイル グループのロックを追跡します。|  
|**req_transactionID**|**bigint**|**Syslockinfo**および profiler イベントで使用される一意のトランザクション ID|  
|**req_transactionUOW**|**uniqueidentifier**|DTC トランザクションの作業単位 ID (UOW) を識別します。 MS DTC 以外のトランザクションの場合、UOW は 0 に設定されます。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [システムビューへのシステムテーブルのマッピング &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
