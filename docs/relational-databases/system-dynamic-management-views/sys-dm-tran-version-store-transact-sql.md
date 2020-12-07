---
description: sys.dm_tran_version_store (Transact-SQL)
title: dm_tran_version_store (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_version_store_TSQL
- sys.dm_tran_version_store
- dm_tran_version_store
- dm_tran_version_store_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_version_store dynamic management view
ms.assetid: 7ab44517-0351-4f91-bdd9-7cf940f03c51
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cd71e1c70ef06d5e669158aea06b7f3dde720951
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546454"
---
# <a name="sysdm_tran_version_store-transact-sql"></a>sys.dm_tran_version_store (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  バージョンストア内のすべてのバージョンレコードを表示する仮想テーブルを返します。 バージョンストア全体に対してクエリを実行し、バージョンストアが非常に大きくなる可能性があるため、dm_tran_version_store を実行するのは効率的ではあり**ません。**  
  
 バージョン管理された各レコードは、追跡情報や状態情報と共にバイナリデータとして格納されます。 データベース テーブル内のレコードと同様、バージョン ストア レコードは 8,192 バイトのページに格納されます。 レコードが 8,192 バイトを超える場合は、2 つのレコードに分割されます。  
  
 バージョン付きのレコードはバイナリとして格納されるため、異なるデータベースからの異なる照合順序に関する問題はありません。 バージョンストアに存在する行の以前のバージョンをバイナリ表現で検索するには、 **dm_tran_version_store** を使用します。  
  
  
## <a name="syntax"></a>構文  
  
```  
sys.dm_tran_version_store  
```  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**transaction_sequence_num**|**bigint**|レコードのバージョンを生成するトランザクションのシーケンス番号。|  
|**version_sequence_num**|**bigint**|バージョン レコードのシーケンス番号。 この値は、バージョン生成トランザクション内で一意です。|  
|**database_id**|**int**|バージョン管理されたレコードのデータベース ID。|  
|**rowset_id**|**bigint**|レコードの行セット ID。|  
|**status**|**tinyint**|バージョン付きのレコードが2つのレコードに分割されているかどうかを示します。 値が 0 の場合、レコードは 1 ページに格納されています。 値が1の場合、レコードは2つの異なるページに格納されている2つのレコードに分割されます。|  
|**min_length_in_bytes**|**smallint**|レコードの最小長 (バイト単位)。|  
|**record_length_first_part_in_bytes**|**smallint**|バージョン レコードの最初の部分の長さ (バイト単位)。|  
|**record_image_first_part**|**varbinary(8000)**|バージョンレコードの最初の部分のバイナリイメージ。|  
|**record_length_second_part_in_bytes**|**smallint**|バージョンレコードの2番目の部分の長さ (バイト単位)。|  
|**record_image_second_part**|**varbinary(8000)**|バージョンレコードの2番目の部分のバイナリイメージ。|  
  
## <a name="permissions"></a>アクセス許可

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   
  
## <a name="examples"></a>例  
 次の例では、4 つの同時実行トランザクションが存在するテスト シナリオを使用します。これらのトランザクションはそれぞれトランザクション シーケンス番号 (XSN) で識別され、ALLOW_SNAPSHOT_ISOLATION オプションと READ_COMMITTED_SNAPSHOT オプションが ON に設定されているデータベース内で実行されます。 実行されるトランザクションは次のとおりです。  
  
-   XSN-57。SERIALIZABLE 分離での更新操作です。  
  
-   XSN-58 は、XSN-57 と同じです。  
  
-   XSN-59 は、スナップショット分離での選択操作です。  
  
-   XSN-60 は、XSN-59 と同じです。  
  
 次のクエリが実行されます。  
  
```  
SELECT  
    transaction_sequence_num,  
    version_sequence_num,  
    database_id rowset_id,  
    status,  
    min_length_in_bytes,  
    record_length_first_part_in_bytes,  
    record_image_first_part,  
    record_length_second_part_in_bytes,  
    record_image_second_part  
  FROM sys.dm_tran_version_store;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
transaction_sequence_num version_sequence_num database_id  
------------------------ -------------------- -----------  
57                      1                    9             
57                      2                    9             
57                      3                    9             
58                      1                    9             
  
rowset_id            status min_length_in_bytes  
-------------------- ------ -------------------  
72057594038321152    0      12                   
72057594038321152    0      12                   
72057594038321152    0      12                   
72057594038386688    0      16                   
  
record_length_first_part_in_bytes  
---------------------------------  
29                                 
29                                 
29                                 
33                                 
  
record_image_first_part                                               
--------------------------------------------------------------------  
0x50000C0073000000010000000200FCB000000001000000270000000000          
0x50000C0073000000020000000200FCB000000001000100270000000000          
0x50000C0073000000030000000200FCB000000001000200270000000000          
0x500010000100000002000000030000000300F800000000000000002E0000000000  
  
record_length_second_part_in_bytes record_image_second_part  
---------------------------------- ------------------------  
0                                  NULL  
0                                  NULL  
0                                  NULL  
0                                  NULL  
```  
  
 この出力は、XSN-57 で 1 つのテーブルから 3 つの行バージョンが作成され、XSN-58 で他のテーブルから 1 つの行バージョンが作成されたことを示しています。  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [トランザクション関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
