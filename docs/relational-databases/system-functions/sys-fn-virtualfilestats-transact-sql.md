---
description: sys.fn_virtualfilestats (Transact-sql)
title: sys.fn_virtualfilestats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_virtualfilestats_TSQL
- fn_virtualfilestats
dev_langs:
- TSQL
helpviewer_keywords:
- I/O [SQL Server], statistics
- fn_virtualfilestats function
- sys.fn_virtualfilestats function
- statistical information [SQL Server], I/O
ms.assetid: 96b28abb-b059-48db-be2b-d60fe127f6aa
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4c49575ef666cf35c26dd4e924cbb75b17cb9c4e
ms.sourcegitcommit: f29f74e04ba9c4d72b9bcc292490f3c076227f7c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2021
ms.locfileid: "98170144"
---
# <a name="sysfn_virtualfilestats-transact-sql"></a>sys.fn_virtualfilestats (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  ログファイルを含む、データベースファイルの i/o 統計を返します。 では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、この情報は [ [sys.dm_io_virtual_file_stats](../../relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql.md) 動的管理] ビューからも利用できます。  

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
fn_virtualfilestats ( { database_id | NULL } , { file_id | NULL } )  
```  
  
## <a name="arguments"></a>引数  
 *database_id* | NULL  
 データベースの ID を示します。 *database_id* は **int**, 、既定値はありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのすべてのデータベースに関する情報を返すには NULL を指定します。  
  
 *file_id* | NULL  
 ファイルの ID を指定します。 *file_id* は **int**,、既定値はありません。 NULL を指定すると、データベース内のすべてのファイルに関する情報が返されます。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**DbId**|**smallint**|データベース ID。|  
|**FileId**|**smallint**|ファイル ID。|  
|**タイムスタンプ**|**bigint**|データが取り出されたデータベース タイムスタンプです。 以前のバージョンの **int** [!INCLUDE[ssSQL15_md](../../includes/sssql16-md.md)] 。 |  
|**NumberReads**|**bigint**|ファイルに対して発行された読み取りの数。|  
|**BytesRead**|**bigint**|ファイルに対して発行された読み取りバイト数。|  
|**IoStallReadMS**|**bigint**|ファイルの読み取り i/o の完了をユーザーが待機した時間の合計 (ミリ秒単位)。|  
|**NumberWrites**|**bigint**|そのファイルで実行された書き込みの数です。|  
|**BytesWritten**|**bigint**|ファイルに書き込まれたバイト数。|  
|**IoStallWriteMS**|**bigint**|ファイルの書き込み i/o の完了をユーザーが待機した時間の合計 (ミリ秒単位)。|  
|**IoStallMS**|**bigint**|**Iostallreadms** と **Iostallreadms** の合計。|  
|**FileHandle**|**bigint**|ファイルハンドルの値。|  
|**BytesOnDisk**|**bigint**|ディスク上の物理ファイルサイズ (バイト数)。<br /><br /> データベースファイルの場合、この値は **sys.database_files** の **サイズ** と同じですが、ページではなくバイト単位で表現されます。<br /><br /> データベーススナップショットのスパースファイルの場合、これはオペレーティングシステムがファイルに対して使用している領域です。|  
  
## <a name="remarks"></a>Remarks  
 **fn_virtualfilestats** は、ファイルで実行された i/o の合計数などの統計情報を提供するシステムテーブル値関数です。 この関数を使用すると、ユーザーがファイルの読み取りまたは書き込みを待機する時間の長さを追跡できます。 また、関数は、大量の i/o アクティビティが発生しているファイルを特定するのにも役立ちます。  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-displaying-statistical-information-for-a-database"></a>A. データベースの統計情報を表示する  
 次の例では、ID がのデータベースのファイル ID 1 の統計情報を表示 `1` します。  
  
```sql  
SELECT *  
FROM fn_virtualfilestats(1, 1);  
GO  
```  
  
### <a name="b-displaying-statistical-information-for-a-named-database-and-file"></a>B. 名前付きデータベースとファイルの統計情報を表示する  
 次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] サンプル データベースのログ ファイルの統計情報を表示します。 システム関数 `DB_ID` は、 *database_id* パラメーターを指定するために使用されます。  
  
```sql  
SELECT *  
FROM fn_virtualfilestats(DB_ID(N'AdventureWorks2012'), 2);  
GO  
```  
  
### <a name="c-displaying-statistical-information-for-all-databases-and-files"></a>C. すべてのデータベースおよびファイルの統計情報を表示する  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内のすべてのデータベースにあるすべてのファイルの統計情報を表示します。  
  
```sql  
SELECT *  
FROM fn_virtualfilestats(NULL,NULL);  
GO  
```  
  
## <a name="see-also"></a>参照  
 [DB_ID &#40;Transact-sql&#41;](../../t-sql/functions/db-id-transact-sql.md)   
 [FILE_IDEX &#40;Transact-SQL&#41;](../../t-sql/functions/file-idex-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
