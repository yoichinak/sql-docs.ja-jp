---
description: sys.dm_db_page_info (Transact-SQL)
title: dm_db_page_info (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 09/18/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_db_page_info
- sys.dm_db_page_info_TSQL
- dm_db_page_info
- dm_db_page_info_TSQL
- dbcc page
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_page_info dynamic management view
author: bluefooted
ms.author: pamela
manager: amitban
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 60df2ed8bf279bf7da8193282768124815aa6ab3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493695"
---
# <a name="sysdm_db_page_info-transact-sql"></a>sys.dm_db_page_info (Transact-SQL)

[!INCLUDE[tsql-appliesto-ssver15-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssver15-asdb-xxxx-xxx.md)]

データベース内のページに関する情報を返します。  関数は、、、など、ページのヘッダー情報を含む1行を `object_id` 返し `index_id` `partition_id` ます。  この関数を使用すると、ほとんどの場合に `DBCC PAGE` を使用する必要がなくなります。

> [!NOTE]
> `sys.dm_db_page_info` は、現在以降でのみサポートされてい [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] ます。


## <a name="syntax"></a>構文   
```  
sys.dm_db_page_info ( DatabaseId, FileId, PageId, Mode )  
``` 

## <a name="arguments"></a>引数  
*DatabaseId* |NULL |標準     
データベースの ID を示します。 *DatabaseId* は **smallint**です。 有効な入力値は、データベースの ID 番号です。 既定値は NULL です。ただし、このパラメーターに NULL 値を指定すると、エラーが発生します。
 
*FileId* |NULL |標準   
ファイルの ID を指定します。 *FileId* は **int**です。 有効な入力は、 *DatabaseId*によって指定されたデータベース内のファイルの ID 番号です。 既定値は NULL です。ただし、このパラメーターに NULL 値を指定すると、エラーが発生します。

*ページ id* |NULL |標準   
ページの ID を示します。  *ページ id* は **int**です。 有効な入力値は、 *FileId*によって指定されたファイル内のページの ID 番号です。 既定値は NULL です。ただし、このパラメーターに NULL 値を指定すると、エラーが発生します。

*Mode* |NULL |標準   
関数の出力の詳細レベルを決定します。 ' 制限付き ' は、すべての説明列に対して NULL 値を返します。 ' DETAILED ' は説明列を設定します。  既定値は "制限されています" です。

## <a name="table-returned"></a>返されるテーブル  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|database_id |INT |データベース ID |
|file_id |INT |ファイル ID |
|page_id |INT |ページ ID |
|page_header_version |INT |ページヘッダーのバージョン |
|page_type |INT |ページの種類 |
|page_type_desc |nvarchar (64) |ページの種類の説明 |
|page_type_flag_bits |nvarchar (64) |ページヘッダーにフラグビットを入力 |
|page_type_flag_bits_desc |nvarchar (64) |ページヘッダーの型フラグのビットの説明 |
|page_flag_bits |nvarchar (64) |ページヘッダーのフラグビット |
|page_flag_bits_desc |nvarchar(256) |ページヘッダーのビットの説明にフラグを付ける |
|page_lsn |nvarchar (64) |ログシーケンス番号/タイムスタンプ |
|page_level |INT |インデックス内のページのレベル (リーフ = 0) |
|object_id |INT |ページを所有しているオブジェクトの ID |
|index_id |INT |インデックスの ID (ヒープデータページの場合は 0) |
|partition_id |bigint |パーティションの ID |
|alloc_unit_id |bigint |アロケーションユニットの ID |
|is_encrypted |bit |ページが暗号化されているかどうかを示すビット |
|has_checksum |bit |ページにチェックサム値があるかどうかを示すビット |
|チェックサム (checksum) |INT |データの破損を検出するために使用されるチェックサム値を格納します。 |
|is_iam_pg |bit |ページが IAM ページであるかどうかを示すビット  |
|is_mixed_ext |bit |混合エクステントで割り当てられているかどうかを示すビット |
|has_ghost_records |bit |ページにゴーストレコードが含まれているかどうかを示すビット <br> ゴーストレコードとは、削除対象としてマークされているものの、まだ削除されていないレコードのことです。|
|has_version_records |bit |ページに[データベースの高速復旧](../backup-restore/restore-and-recovery-overview-sql-server.md#adr)に使用されるバージョンレコードが含まれているかどうかを示すビット |
|pfs_page_id |INT |対応する PFS ページのページ ID |
|pfs_is_allocated |bit |対応する PFS ページでページが割り当て済みとしてマークされているかどうかを示すビット |
|pfs_alloc_percent |INT |対応する PFS バイトによって示される割り当て比率 |
|pfs_status |nvarchar (64) |PFS バイト |
|pfs_status_desc |nvarchar (64) |PFS バイトの説明 |
|gam_page_id |INT |対応する GAM ページのページ ID |
|gam_status |bit |GAM で割り当てられているかどうかを示すビット |
|gam_status_desc |nvarchar (64) |GAM ステータスビットの説明 |
|sgam_page_id |INT |対応する SGAM ページのページ ID |
|sgam_status |bit |SGAM で割り当てられているかどうかを示すビット |
|sgam_status_desc |nvarchar (64) |SGAM ステータスビットの説明 |
|diff_map_page_id |INT |対応する差分ビットマップページのページ ID |
|diff_status |bit |Diff の状態が変更されたかどうかを示すビット |
|diff_status_desc |nvarchar (64) |Diff ステータスビットの説明 |
|ml_map_page_id |INT |対応する最小ログ記録ビットマップページのページ ID |
|ml_status |bit |ページが最小ログ記録されるかどうかを示すビット |
|ml_status_desc |nvarchar (64) |最小ログ記録ステータスビットの説明 |
|prev_page_file_id |smallint |前のページファイル ID |
|prev_page_page_id |INT |前のページページ ID |
|next_page_file_id |smallint |次のページファイル ID |
|next_page_page_id |INT |次のページページ ID |
|fixed_length |smallint |固定サイズの行の長さ |
|slot_count |smallint |スロットの合計数 (使用済みおよび未使用) <br> データページの場合、この数値は行の数と同じです。 |
|ghost_rec_count |smallint |ページでゴーストとしてマークされたレコードの数 <br> ゴーストレコードとは、削除対象としてマークされているものの、まだ削除されていないレコードのことです。 |
|free_bytes |smallint |ページの空きバイト数 |
|free_data_offset |INT |データ領域の端にある空き領域のオフセット |
|reserved_bytes |smallint |すべてのトランザクションで予約されている空きバイト数 (ヒープの場合) <br> ゴースト行の数 (インデックスのリーフの場合) |
|reserved_bytes_by_xdes_id |smallint |M_reservedCnt に m_xdesID によって提供される領域 <br> デバッグ目的のみ |
|xdes_id |nvarchar (64) |M_reserved によって提供される最新のトランザクション <br> デバッグ目的のみ |
||||

## <a name="remarks"></a>解説
`sys.dm_db_page_info`動的管理関数は `page_id` 、 `file_id` `index_id` `object_id` ページヘッダーに存在する、、、などのページ情報を返します。 この情報は、さまざまなパフォーマンス (ロックとラッチの競合) と破損の問題に関するトラブルシューティングとデバッグに役立ちます。

`sys.dm_db_page_info` 多くの場合、ステートメントの代わりに使用でき `DBCC PAGE` ますが、ページの本文ではなくページヘッダー情報のみが返されます。 `DBCC PAGE` は、ページのコンテンツ全体が必要な場合にも必要になります。

## <a name="using-in-conjunction-with-other-dmvs"></a>を他の Dmv と組み合わせて使用する
の重要なユースケースの1つ `sys.dm_db_page_info` は、ページ情報を公開する他の dmv と結合することです。  このユースケースを容易にするために、という新しい列 `page_resource` が追加されました。これにより、ページ情報が8バイトの16進形式で公開されます。 この列は、およびに追加されており、必要に応じ `sys.dm_exec_requests` `sys.sysprocesses` て今後他の dmv に追加されます。

新しい関数は、を `sys.fn_PageResCracker` 入力として受け取り、 `page_resource` 、、およびを含む1行を出力し `database_id` `file_id` `page_id` ます。  この関数は、またはとの間の結合を容易にするために使用でき `sys.dm_exec_requests` `sys.sysprocesses` `sys.dm_db_page_info` ます。

## <a name="permissions"></a>アクセス許可  
データベースの権限が必要です `VIEW DATABASE STATE` 。  
  
## <a name="examples"></a>例  
  
### <a name="a-displaying-all-the-properties-of-a-page"></a>A. ページのすべてのプロパティを表示する
次のクエリでは、指定したのすべてのページ情報を含む1行が返されます `database_id` `file_id` `page_id` 。既定のモード (' 制限付き ') と組み合わせて使用します。

```sql
SELECT *  
FROM sys.dm_db_page_info (5, 1, 15, DEFAULT)
```

### <a name="b-using-sysdm_db_page_info-with-other-dmvs"></a>B. 他の Dmv での dm_db_page_info の使用 

次のクエリは、行に `wait_resource` `sys.dm_exec_requests` null 以外のが含まれている場合に、によって公開される1行を返します。 `page_resource`

```sql
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 'LIMITED') AS page_info
```

## <a name="see-also"></a>関連項目  
[動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Transact-sql&#41;&#40;データベース関連の動的管理ビュー ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)     
[sys.fn_PageResCracker](../../relational-databases/system-functions/sys-fn-pagerescracker-transact-sql.md)


