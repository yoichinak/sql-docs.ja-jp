---
description: sys.column_store_row_groups (Transact-SQL)
title: sys.column_store_row_groups (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/28/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.column_store_row_groups_TSQL
- column_store_row_groups
- sys.column_store_row_groups
- column_store_row_groups_TSQL
- deleted bitmap
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_store_row_groups catalog view
ms.assetid: 76e7fef2-d1a4-4272-a2bb-5f5dcd84aedc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 95d7d35ad00eb1e134f7eec2165c2c59dea933e2
ms.sourcegitcommit: 9c6130d498f1cfe11cde9f2e65c306af2fa8378d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93036079"
---
# <a name="syscolumn_store_row_groups-transact-sql"></a>sys.column_store_row_groups (Transact-SQL)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  では、管理者がシステム管理の決定を行うのに役立つ、セグメント単位でクラスター化列ストアインデックス情報が提供されます。 **sys.column_store_row_groups** には、物理的に格納された行の総数 (削除済みとしてマークされている行を含む) と、削除済みとしてマークされた行の数の列があります。 **Sys.column_store_row_groups** を使用して、削除された行の割合が高く、再構築が必要な行グループを特定します。  
   
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|int|このインデックスが定義されているテーブルの ID。|  
|**index_id**|int|この列ストアインデックスを持つテーブルのインデックスの ID。|  
|**partition_number**|int|行グループ row_group_id を保持するテーブル パーティションの ID。 Partition_number を使用して、この DMV を sys パーティションに参加させることができます。|  
|**row_group_id**|int|この行グループに関連付けられている行グループ番号。 これは、パーティション内で一意です。<br /><br /> -1 = メモリ内のテーブルの末尾。|  
|* * delta_store_hobt_id|bigint * *|デルタストア内の開いている行グループの hobt_id。<br /><br /> 行グループがデルタストアに存在しない場合は NULL になります。<br /><br /> メモリ内のテーブルの末尾の場合は NULL です。|  
|**state**|tinyint|State_description に関連付けられている ID 番号。<br /><br /> 0 = 非表示<br /><br /> 1 = OPEN <br /><br /> 2 = CLOSED <br /><br /> 3 = 圧縮 <br /><br /> 4 = 廃棄標識|  
|**state_description**|nvarchar(60)|行グループの永続的な状態の説明。<br /><br /> 非表示-デルタストア内のデータから構築されるプロセス内の非表示の圧縮セグメント。 非表示の圧縮されたセグメントが完了するまで、読み取りアクションでデルタ ストアが使用されます。 その後、新しいセグメントが表示されると、ソース デルタ ストアは削除されます。<br /><br /> OPEN-新しいレコードを受け入れる読み取り/書き込み行グループ。 開いている行グループは、行ストア形式のままであり、列ストア形式に圧縮されていません。<br /><br /> CLOSED-組ムーバープロセスによってまだ圧縮されていない、いっぱいになっている行グループ。<br /><br /> 圧縮-格納され、圧縮された行グループ。|  
|**total_rows**|bigint|行グループに物理的に格納されている行の合計。 削除されたものの、まだ保存されているものもあります。 行グループ内の行の最大数は 1048576 (16 進数 FFFFF) です。|  
|**deleted_rows**|bigint|削除済みとマークされた行グループ内の行の合計数。 これはデルタ行グループの場合は常に 0 です。|  
|**size_in_bytes**|bigint|デルタ列と列ストア行グループの両方について、この行グループ内のすべてのデータのサイズ (メタデータや共有ディクショナリを除く) のサイズ (バイト単位)。|  
  
## <a name="remarks"></a>注釈  
 クラスター化または非クラスター化列ストアインデックスを持つ各テーブルの列ストア行グループごとに1行の値を返します。  
  
 **Sys.column_store_row_groups** を使用して、行グループに含まれる行の数と行グループのサイズを決定します。  
  
 行グループ内の削除済みの行の数が合計行数に対して占める割合が高くなると、テーブルの効率が低下します。 テーブルのサイズが小さくなるよう列ストア インデックスを再構築して、テーブルを読み取るために必要なディスク I/O を削減します。 列ストアインデックスを再構築するには、 **ALTER index** ステートメントの **rebuild** オプションを使用します。  
  
 更新可能な列ストアは、まず、行ストア形式の、 **開い** ている行グループに新しいデータを挿入します。これは、デルタテーブルと呼ばれることもあります。  開いている行グループがいっぱいになると、その状態は **CLOSED** に変わります。 閉じた行グループは、組ムーバーによって列ストア形式に圧縮され、状態が **圧縮** に変わります。  組ムーバーは、定期的にウェイクアップし、列ストア行グループに圧縮できる閉じた行グループがあるかどうかを確認するバックグラウンドプロセスです。  また、組ムーバーは、すべての行が削除された行グループの割り当てを解除します。 割り当てが解除された行グループは、 **廃棄** 済みとしてマークされます。 組ムーバーをすぐに実行するには、 **ALTER INDEX** ステートメントの **再構成** オプションを使用します。  
  
 列ストア行グループは、いっぱいになると圧縮され、新しい行の受け入れを停止します。 圧縮されたグループから行が削除されると、削除された行は、保持されますが、削除済みとしてマークされます。 圧縮されたグループに対する更新は、圧縮されたグループからの削除、および OPEN 状態のグループへの挿入として実装されます。  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーがテーブルに対する権限を持っている場合、テーブルに関する情報を返し `VIEW DEFINITION` ます。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="examples"></a>例  
 次の例では、 **sys.column_store_row_groups** テーブルを他のシステムテーブルに結合して、特定のテーブルに関する情報を返します。 計算済みの `PercentFull` 列は、行グループの効率の推定値を示します。 1つのテーブルに関する情報を検索するには、 **WHERE** 句の前にあるコメントハイフンを削除し、テーブル名を指定します。  
  
```sql  
SELECT i.object_id, object_name(i.object_id) AS TableName,   
i.name AS IndexName, i.index_id, i.type_desc,   
CSRowGroups.*,   
100*(total_rows - ISNULL(deleted_rows,0))/total_rows AS PercentFull    
FROM sys.indexes AS i  
JOIN sys.column_store_row_groups AS CSRowGroups  
    ON i.object_id = CSRowGroups.object_id  
AND i.index_id = CSRowGroups.index_id   
--WHERE object_name(i.object_id) = '<table_name>'   
ORDER BY object_name(i.object_id), i.name, row_group_id;  
```  
  
## <a name="see-also"></a>関連項目  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server システムカタログに対するクエリについてよく寄せられる質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.all_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.computed_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [列ストア インデックス ガイド](~/relational-databases/indexes/columnstore-indexes-overview.md)     
 [sys.column_store_dictionaries &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)   
 [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
  

