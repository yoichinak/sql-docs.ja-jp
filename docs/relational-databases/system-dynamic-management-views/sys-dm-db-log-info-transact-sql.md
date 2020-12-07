---
description: dm_db_log_info (Transact-sql)
title: dm_db_log_info (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_db_log_info
- sys.dm_db_log_info_TSQL
- dm_db_log_info
- dm_db_log_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_log_info dynamic management view
ms.assetid: f6b40060-c17d-472f-b0a3-3b350275d487
author: savjani
ms.author: pariks
manager: ajayj
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: aba965d4a0289db9ef7def58b90f15a1479cb485
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447664"
---
# <a name="sysdm_db_log_info-transact-sql"></a>dm_db_log_info (Transact-sql)
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

トランザクションログの [仮想ログファイル (値)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) を返します。 メモすべてのトランザクションログファイルがテーブル出力で結合されていることに注意してください。 出力の各行は、トランザクションログの "1" を表し、ログ内のその中に関連する情報を提供します。

## <a name="syntax"></a>構文  
  
```  
sys.dm_db_log_info ( database_id )  
``` 

## <a name="arguments"></a>引数  
 *database_id* |NULL |標準  
 データベースの ID を示します。 *database_id* は **int**です。有効な入力値は、データベースの ID 番号、NULL、または DEFAULT です。 既定値は NULL です。 現在のデータベースのコンテキストでは、NULL および DEFAULT は同じ値になります。
 
 NULL を指定すると、現在のデータベースのすべての情報が返されます。

 組み込み関数 [DB_ID](../../t-sql/functions/db-id-transact-sql.md) を指定できます。 データベース名を指定せずにを使用する場合は、 `DB_ID` 現在のデータベースの互換性レベルが90以上である必要があります。  

## <a name="table-returned"></a>返されるテーブル  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|database_id|**int**|データベース ID。|
|file_id|**smallint**|トランザクションログのファイル id。|  
|vlf_begin_offset|**bigint** |トランザクションログファイルの先頭からの [仮想ログファイル (%)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) のオフセット位置。|
|vlf_size_mb |**float** |[仮想ログファイル](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) のサイズ (単位は MB)。小数点以下2桁に丸められます。|     
|vlf_sequence_number|**bigint** |作成された順序での[仮想ログファイル (列)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)のシーケンス番号。 ログファイル内の Vlf を一意に識別するために使用されます。|
|vlf_active|**bit** |[仮想ログファイル (無効)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)が使用中かどうかを示します。 <br />0: の場合、使用されていません。<br />1-状態がアクティブです。|
|vlf_status|**int** |[仮想ログファイル](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)の状態 (%)。 使用できる値は次のとおりです。 <br />0: 1-1 が非アクティブです <br />1-1-2 は初期化されていますが、未使用です <br /> 2-状態がアクティブです。|
|vlf_parity|**tinyint** |[仮想ログファイル (%)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)のパリティ。指定した範囲内のログの末尾を特定するために内部的に使用されます。|
|vlf_first_lsn|**nvarchar (48)** |[仮想ログファイル (](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)列 1) 内の最初のログレコードの[ログシーケンス番号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) 。|
|vlf_create_lsn|**nvarchar (48)** |[仮想ログファイル](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)を作成したログレコードの[ログシーケンス番号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) 。|
|vlf_encryptor_thumbprint|**varbinary(20)**| **適用対象:** [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] <br><br> 値が [Transparent Data Encryption](../../relational-databases/security/encryption/transparent-data-encryption.md)を使用して暗号化されている場合は、オフの暗号化の拇印を表示します。それ以外の場合は NULL を示します。 |

## <a name="remarks"></a>解説
`sys.dm_db_log_info`動的管理関数は、ステートメントを置き換え `DBCC LOGINFO` ます。    
 
## <a name="permissions"></a>アクセス許可  
データベースの権限が必要です `VIEW DATABASE STATE` 。  
  
## <a name="examples"></a>例  
  
### <a name="a-determing-databases-in-a-sql-server-instance-with-high-number-of-vlfs"></a>A. 多数の Vlf がある SQL Server インスタンスでデータベースを決定する
次のクエリでは、ログファイルに 100 Vlf 以上のデータベースがあるかどうかを確認します。これは、データベースの起動、復元、および復旧時間に影響を与える可能性があります。

```sql
SELECT [name], COUNT(l.database_id) AS 'vlf_count' 
FROM sys.databases s
CROSS APPLY sys.dm_db_log_info(s.database_id) l
GROUP BY [name]
HAVING COUNT(l.database_id) > 100
```

### <a name="b-determing-the-position-of-the-last-vlf-in-transaction-log-before-shrinking-the-log-file"></a>B. `VLF`ログファイルを圧縮する前に、トランザクションログの最後の位置を決定する

次のクエリを使用すると、トランザクションログで shrinkfile を実行してからトランザクションログを圧縮できるかどうかを判断する前に、最後にアクティブ化された状態の位置を確認できます。

```sql
USE AdventureWorks2016
GO

;WITH cte_vlf AS (
SELECT ROW_NUMBER() OVER(ORDER BY vlf_begin_offset) AS vlfid, DB_NAME(database_id) AS [Database Name], vlf_sequence_number, vlf_active, vlf_begin_offset, vlf_size_mb
    FROM sys.dm_db_log_info(DEFAULT)),
cte_vlf_cnt AS (SELECT [Database Name], COUNT(vlf_sequence_number) AS vlf_count,
    (SELECT COUNT(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 0) AS vlf_count_inactive,
    (SELECT COUNT(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS vlf_count_active,
    (SELECT MIN(vlfid) FROM cte_vlf WHERE vlf_active = 1) AS ordinal_min_vlf_active,
    (SELECT MIN(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS min_vlf_active,
    (SELECT MAX(vlfid) FROM cte_vlf WHERE vlf_active = 1) AS ordinal_max_vlf_active,
    (SELECT MAX(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS max_vlf_active
    FROM cte_vlf
    GROUP BY [Database Name])
SELECT [Database Name], vlf_count, min_vlf_active, ordinal_min_vlf_active, max_vlf_active, ordinal_max_vlf_active,
((ordinal_min_vlf_active-1)*100.00/vlf_count) AS free_log_pct_before_active_log,
((ordinal_max_vlf_active-(ordinal_min_vlf_active-1))*100.00/vlf_count) AS active_log_pct,
((vlf_count-ordinal_max_vlf_active)*100.00/vlf_count) AS free_log_pct_after_active_log
FROM cte_vlf_cnt
GO
```

## <a name="see-also"></a>参照  
[動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Transact-sql&#41;&#40;データベース関連の動的管理ビュー ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)

