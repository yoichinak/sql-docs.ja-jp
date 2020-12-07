---
description: sp_lock (Transact-SQL)
title: sp_lock (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_lock_TSQL
- sp_lock
dev_langs:
- TSQL
helpviewer_keywords:
- sp_lock
ms.assetid: 9eaa0ec2-2ad9-457c-ae48-8da92a03dcb0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6af5955121813edaf0580c1c3204f8337d1deade
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545980"
---
# <a name="sp_lock-transact-sql"></a>sp_lock (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ロックに関する情報を報告します。  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] のロックに関する情報を取得するには、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] [dm_tran_locks](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md) 動的管理ビューを使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_lock [ [ @spid1 = ] 'session ID1' ] [ , [@spid2 = ] 'session ID2' ]  
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
`[ @spid1 = ] 'session ID1'` ユーザーが [!INCLUDE[ssDE](../../includes/ssde-md.md)] ロック情報を必要とする、 **dm_exec_sessions** のセッション ID 番号を指定します。 *SESSION ID1* は **int** で、既定値は NULL です。 **Sp_who**を実行して、セッションに関するプロセス情報を取得します。 *SESSION ID1*が指定されていない場合は、すべてのロックに関する情報が表示されます。  
  
`[ @spid2 = ] 'session ID2'`は、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ID1 からの別のセッション ID 番号であり、*セッション*と同時にロックが設定されていて、ユーザーが情報を必要とする場合もあります**dm_exec_sessions。** *SESSION ID2* は **int** で、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 成功した場合は 0 を返します。  
  
## <a name="result-sets"></a>結果セット  
 **Sp_lock**の結果セットには、 ** \@ spid1**パラメーターと** \@ spid2**パラメーターで指定したセッションによって保持されているロックごとに1つの行が含まれます。 ** \@ Spid1**も** \@ spid2**も指定しない場合、結果セットはのインスタンスで現在アクティブなすべてのセッションのロックを報告し [!INCLUDE[ssDE](../../includes/ssde-md.md)] ます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**spid**|**smallint**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]ロックを要求しているプロセスのセッション ID 番号。|  
|**dbid**|**smallint**|ロックが保持されているデータベースの ID 番号です。 データベースを識別するには、DB_NAME () 関数を使用します。|  
|**ObjId**|**int**|ロックが保持されているオブジェクトの識別番号。 関連するデータベースの OBJECT_NAME () 関数を使用すると、オブジェクトを識別できます。 値99は、データベース内のページの割り当てを記録するために使用されるシステムページの1つをロックすることを示す特殊なケースです。|  
|**IndId**|**smallint**|ロックが保持されているインデックスの識別番号を指定します。|  
|**型**|**nchar (4)**|ロックの種類:<br /><br /> RID = 行識別子 (RID) で識別されるテーブル内の1つの行をロックします。<br /><br /> KEY = シリアル化可能なトランザクションのキーの範囲を保護するインデックス内のロック。<br /><br /> PAG = データまたはインデックス ページのロック。<br /><br /> EXT = エクステントに対するロック。<br /><br /> TAB = すべてのデータとインデックスを含むテーブル全体のロック。<br /><br /> DB = データベースのロック。<br /><br /> FIL = データベース ファイルのロック。<br /><br /> APP = アプリケーションで指定されたリソースのロック。<br /><br /> MD = メタデータまたはカタログ情報のロック。<br /><br /> HBT = ヒープまたは B-tree のロック (HoBT)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではこの情報は不完全です。<br /><br /> AU = アロケーション ユニットのロック。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではこの情報は不完全です。|  
|**リソース**|**nchar(32)**|ロックされているリソースを識別する値。 値の形式は、 **type** 列で識別されるリソースの種類によって異なります。<br /><br /> **型** 値: **リソース** 値<br /><br /> RID: fileid: pagenumber: rid という形式の識別子。ここで、fileid はページを含むファイルを識別し、pagenumber は行を含むページを識別し、rid はページ上の特定の行を識別します。 fileid は、 **database_files**カタログビューの**file_id**列と一致します。<br /><br /> KEY : [!INCLUDE[ssDE](../../includes/ssde-md.md)]が内部的に使用する 16 進数です。<br /><br /> PAG: fileid: pagenumber という形式の数値。ここで、fileid はページを含むファイルを識別し、pagenumber はページを識別します。<br /><br /> EXT: エクステント内の最初のページを識別する番号。 この番号は、fileid:pagenumber というフォーマットで指定します。<br /><br /> TAB: テーブルが **ObjId** 列で既に識別されているため、情報は提供されません。<br /><br /> DB: データベースが **dbid** 列で既に識別されているため、情報は提供されませんでした。<br /><br /> FIL: ファイルの識別子。 **database_files**カタログビューの**file_id**列と一致します。<br /><br /> アプリ: ロックされているアプリケーションリソースに固有の識別子。 DbPrincipleId: の形式で指定 \<first two to 16 characters of the resource string> \<hashed value> します。<br /><br /> MD: リソースの種類によって異なります。 詳細については、「 [transact-sql&#41;&#40;dm_tran_locks](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)の**resource_description**列の説明を参照してください。<br /><br /> HBT : 情報は提供されません。 代わりに、 **dm_tran_locks** 動的管理ビューを使用してください。<br /><br /> AU: 情報は提供されません。 代わりに、 **dm_tran_locks** 動的管理ビューを使用してください。|  
|**モード**|**nvarchar(8)**|要求されたロック モードです。 次の値をとります。<br /><br /> NULL = リソースへのアクセスは許可されていません。 プレースホルダーとして機能します。<br /><br /> Sch-S = スキーマ安定度。 スキーマ要素に対するスキーマの安定性ロックを保持しているセッションがある間、テーブルやインデックスなどのスキーマ要素が削除されないようにします。<br /><br /> Sch-M = スキーマ修正。 は、指定されたリソースのスキーマを変更する必要があるすべてのセッションによって保持される必要があります。 指定されたオブジェクトを参照している他のセッションがないことを確認します。<br /><br /> S = 共有。 保持しているセッションに、リソースへの共有アクセスが許可されます。<br /><br /> U = 更新。 リソース上で取得された更新ロックが、最終的に更新されることが許可されます。 これは、複数のセッションが、後で潜在的な更新のためにリソースをロックするときに発生する一般的な形式のデッドロックを防ぐために使用されます。<br /><br /> X = 排他。 保持しているセッションで、リソースへの排他アクセスが許可されます。<br /><br /> IS = インテント共有。 ロック階層の下位のリソースに S ロックを配置することを示します。<br /><br /> IU = インテント更新。 ロック階層の下位のリソースに U ロックを設定するよう指定します。<br /><br /> IX = インテント排他。 ロック階層の下位のリソースに X ロックを設定するよう指定します。<br /><br /> SIU = 共有インテント更新。 ロック階層の下位のリソースに更新ロックを設定する目的で、リソースへの共有アクセスを指定します。<br /><br /> 6 = 共有インテント排他。 ロック階層内の下位のリソースに排他ロックを取得する目的で、リソースへの共有アクセスを示します。<br /><br /> UIX = 更新インテント排他。 ロック階層の下位のリソースに排他ロックを設定する目的で、リソースに保持する更新ロックを指定します。<br /><br /> BU = 一括更新。 一括操作で使用されます。<br /><br /> RangeS_S = 共有キー範囲と共有リソースロック。 シリアル化可能な範囲スキャンを示します。<br /><br /> RangeS_U = 共有キー範囲と更新リソースロック。 シリアル化可能な更新プログラムのスキャンを示します。<br /><br /> RangeI_N = 挿入キー範囲と NULL リソース ロック。 インデックスに新しいキーを挿入する前に範囲をテストするために使用されます。<br /><br /> RangeI_S = キー範囲変換ロック。 RangeI_N と S ロックの重複によって作成されます。<br /><br /> RangeI_U = RangeI_N と U ロックの重なりによって作成されるキー範囲変換ロック。<br /><br /> RangeI_X = RangeI_N と X ロックの重なりによって作成されるキー範囲変換ロック。<br /><br /> RangeX_S = RangeI_N と RangeS_S の重なりによって作成されるキー範囲変換ロック。 固定.<br /><br /> RangeX_U = 範囲 I_N と範囲 S_U ロックの重複によって作成されるキー範囲変換ロックです。<br /><br /> RangeX_X = 排他キー範囲と排他リソース ロック。 範囲内のキーを更新する場合に使用する変換ロックです。|  
|**状態**|**nvarchar (5)**|ロック要求の状態:<br /><br /> CNVRT: ロックは別のモードから変換されていますが、競合するモードでロックを保持している別のプロセスによって変換がブロックされています。<br /><br /> GRANT : ロックが取得されたことを示します。<br /><br /> WAIT : 競合するモードでロックを保持している別のプロセスによってロックがブロックされていることを示します。|  
  
## <a name="remarks"></a>解説  
 ユーザーは、次の方法で読み取り操作のロックを制御できます。  
  
-   SET TRANSACTION ISOLATION LEVEL を使用してセッションのロック レベルを指定します。 構文と制限については、「 [SET TRANSACTION 分離レベル &#40;transact-sql&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)」を参照してください。  
  
-   ロック テーブル ヒントを使用して、FROM 句での個々のテーブル参照のロック レベルを指定します。 構文と制限については、「 [transact-sql&#41;&#40;テーブルヒント ](../../t-sql/queries/hints-transact-sql-table.md)」を参照してください。  
  
 セッションに関連付けられていないすべての分散トランザクションは、孤立しているトランザクションです。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]では、孤立しているすべての分散トランザクションに、-2 の SPID 値が割り当てられます。このため、ユーザーは、孤立している分散トランザクションを簡単に識別できます。 詳細については、「 [マークされたトランザクションを使用して関連するデータベースを一貫した状態に復元する方法 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 VIEW SERVER STATE 権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-listing-all-locks"></a>A. すべてのロックを一覧表示する  
 次の例では、[!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスで現在保持されているすべてのロックに関する情報を表示します。  
  
```sql  
USE master;  
GO  
EXEC sp_lock;  
GO  
```  
  
### <a name="b-listing-a-lock-from-a-single-server-process"></a>B. 1 つのサーバー プロセスからロックを表示する  
 次の例では、プロセス ID `53` に関する情報を表示します。ロックなどの情報も含まれます。  
  
```sql  
USE master;  
GO  
EXEC sp_lock 53;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)   
 [DB_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)   
 [KILL &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-transact-sql.md)   
 [OBJECT_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/object-name-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [dm_os_tasks &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)   
 [sys.dm_os_threads &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md)  
  
  
