---
description: sp_filestream_force_garbage_collection (Transact-SQL)
title: sp_filestream_force_garbage_collection (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_filestream_force_garbage_collection
- sp_filestream_force_garbage_collection_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- FILESTREAM [SQL Server]
- sp_filestream_force_garbage_collection
ms.assetid: 9d1efde6-8fa4-42ac-80e5-37456ffebd0b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 627793d900903a28ce4e4b7ee6a3272b4c63ee32
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753845"
---
# <a name="sp_filestream_force_garbage_collection-transact-sql"></a>sp_filestream_force_garbage_collection (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  FILESTREAM ガベージコレクターを強制的に実行し、不要な FILESTREAM ファイルを削除します。  
  
 FILESTREAM コンテナーは、その中のすべての削除済みファイルがガベージコレクターによってクリーンアップされるまで削除できません。 FILESTREAM ガベージ コレクターは自動的に実行されます。 ただし、ガベージコレクターを実行する前にコンテナーを削除する必要がある場合は、sp_filestream_force_garbage_collection を使用して手動でガベージコレクターを実行できます。  
  
  
## <a name="syntax"></a>構文  
  
```  
sp_filestream_force_garbage_collection
    [ @dbname = ]  'database_name'
    [ , [ @filename = ] 'logical_file_name' ]
```  
  
## <a name="arguments"></a>引数  
 `[ @dbname = ]  'database_name'`  
 ガベージコレクターを実行するデータベースの名前を示します。  
  
> [!NOTE]  
> `@dbname` のデータ型は **sysname** です。 指定しない場合、現在のデータベースが想定されます。  
  
 `[ @filename = ] 'logical_file_name'`  
 ガベージ コレクターを実行する FILESTREAM コンテナーの論理名を指定します。 `@filename` はオプションです。 論理ファイル名が指定されていない場合、ガベージコレクターは、指定されたデータベース内のすべての FILESTREAM コンテナーを消去します。  
  
## <a name="return-code-values"></a>リターン コードの値  
  
| 値 | 説明 |
| ----- | ----------- |   
|0|操作に成功しました。|  
|1|操作エラー|  
  
## <a name="result-sets"></a>結果セット  
  
|値|説明|  
|-----------|-----------------|  
|*file_name*|FILESTREAM コンテナー名を示します。|  
|*num_collected_items*|このコンテナー内の、ガベージ コレクションが実行 (削除) された FILESTREAM アイテム (ファイルまたはディレクトリ) の数を示します。|  
|*num_marked_for_collection_items*|このコンテナー内の、ガベージ コレクションの対象としてマークされた FILESTREAM アイテム (ファイルまたはディレクトリ) の数を示します。 これらの項目はまだ削除されていませんが、ガベージコレクションフェーズに従って削除することができます。|  
|*num_unprocessed_items*|この FILESTREAM コンテナー内の、ガベージ コレクションで処理されなかった対象となる FILESTREAM アイテム (ファイルまたはディレクトリ) の数を示します。 アイテムは次のようなさまざまな理由で処理されないことがあります。<br /><br /> ログのバックアップまたはチェックポイントが作成されていないために、固定する必要があるファイル。<br /><br /> 完全復旧モデルまたは BULK_LOGGED 復旧モデル内のファイル。<br /><br /> 実行時間の長いアクティブなトランザクションが存在している。<br /><br /> レプリケーションログリーダージョブが実行されていません。 詳細については、ホワイトペーパー「 [SQL Server 2008 の FILESTREAM ストレージ](/previous-versions/sql/sql-server-2008/hh461480(v=msdn.10)) 」を参照してください。|  
|*last_collected_xact_seqno*|指定した FILESTREAM コンテナー内の、ガベージ コレクションが実行されたファイルに対応する最後のログ シーケンス番号 (LSN) を返します。|  
  
## <a name="remarks"></a>解説  
 要求されたデータベース (および FILESTREAM コンテナー) で、FILESTREAM ガベージコレクタータスクが明示的に完了するように実行します。 不要になったファイルは、ガベージ コレクション プロセスによって削除されます。 この操作の完了に必要な時間は、そのデータベースまたはコンテナー内の FILESTREAM データのサイズに加え、FILESTREAM データで最近発生した DML アクティビティの量によって異なります。 この操作はデータベースがオンラインのときに実行できますが、ガベージ コレクション プロセスによってさまざまな I/O 操作が行われるため、実行中にデータベースのパフォーマンスに影響を与える可能性があります。  
  
> [!NOTE]  
>  この操作は、必要なときと通常の操作時間外にのみ実行することをお勧めします。  
  
このストアドプロシージャの複数の呼び出しは、個別のコンテナーまたは個別のデータベースでのみ同時に実行できます。  

2フェーズの操作が発生したため、基になる Filestream ファイルを実際に削除するには、ストアドプロシージャを2回実行する必要があります。  

ガベージコレクション (GC) は、ログの切り捨てに依存します。 したがって、完全復旧モデルを使用してデータベースで最近削除されたファイルの場合は、それらのトランザクションログ部分のログバックアップが実行され、ログ部分が非アクティブとマークされた後にのみ、GC が実行されます。 単純復旧モデルを使用するデータベースでは、がデータベースに対して発行された後に、ログの切り捨てが行わ `CHECKPOINT` れます。  


## <a name="permissions"></a>アクセス許可  
 Db_owner データベースロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、データベースの FILESTREAM コンテナーに対してガベージコレクターを実行し `FSDB` ます。  
  
### <a name="a-specifying-no-container"></a>A. コンテナーを指定しない  
  
```sql  
USE FSDB;  
GO  
EXEC sp_filestream_force_garbage_collection @dbname = N'FSDB';  
```  
  
### <a name="b-specifying-a-container"></a>B. コンテナーを指定する  
  
```sql  
USE FSDB;  
GO  
EXEC sp_filestream_force_garbage_collection @dbname = N'FSDB',
    @filename = N'FSContainer';  
```  
  
## <a name="see-also"></a>参照  
[FileStream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetable](../../relational-databases/blob/filetables-sql-server.md)
<br>[Filestream および FileTable の動的管理ビュー (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Filestream および FileTable のカタログ ビュー (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
<br>[sp_kill_filestream_non_transacted_handles (Transact-sql)](filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)
  
