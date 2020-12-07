---
description: TRUNCATE TABLE (Transact-SQL)
title: TRUNCATE TABLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TRUNCATE
- TRUNCATE TABLE
- TRUNCATE_TSQL
- TRUNCATE_TABLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- row removal [SQL Server], TRUNCATE TABLE statement
- table truncating [SQL Server]
- removing rows
- TRUNCATE TABLE statement
- deleting rows
- dropping rows
ms.assetid: 3d544eed-3993-4055-983d-ea334f8c5c58
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3a4e4aa7795ad7ddb4a8c321afd5eb8f33b49db5
ms.sourcegitcommit: 8f062015c2a033f5a0d805ee4adabbe15e7c8f94
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2020
ms.locfileid: "91227036"
---
# <a name="truncate-table-transact-sql"></a>TRUNCATE TABLE (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

個々の行の削除をログに記録せず、テーブルまたはテーブルの指定したパーティションからすべての行を削除します。 TRUNCATE TABLE は、WHERE 句を伴わない DELETE ステートメントに似ています。ただし、TRUNCATE TABLE の方が高速で、使用するシステム リソースとトランザクション ログ リソースも少なくなります。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database  
  
TRUNCATE TABLE   
    { database_name.schema_name.table_name | schema_name.table_name | table_name }  
    [ WITH ( PARTITIONS ( { <partition_number_expression> | <range> }   
    [ , ...n ] ) ) ]  
[ ; ]  
  
<range> ::=  
<partition_number_expression> TO <partition_number_expression>  
```  
  
```syntaxsql
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
TRUNCATE TABLE { database_name.schema_name.table_name | schema_name.table_name | table_name }  
[;]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *database_name*  
 データベースの名前です。  
  
 *schema_name*  
 テーブルが所属するスキーマの名前を指定します。  
  
 *table_name*  
 切り捨てるまたはすべての行を削除するテーブルの名前を指定します。 *table_name* はリテラルで指定する必要があります。 *table_name* することはできません、 **OBJECT_ID()** 関数または変数です。  
  
 WITH ( PARTITIONS ( { \<*partition_number_expression*> | \<*range*> } [ , ...n ] ) )    
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から[現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)
  
 切り捨てるパーティション、またはすべての行を削除するパーティションを指定します。 テーブルがパーティション分割されていない場合に `WITH PARTITIONS` 引数を使用すると、エラーが発生します。 `WITH PARTITIONS` 句が指定されていない場合、テーブル全体が切り捨てられます。  
  
 *\<partition_number_expression>* は以下の方法で指定できます。 
  
-   `WITH (PARTITIONS (2))` などのようにパーティション番号を指定します  
  
-   コンマで区切った複数の個別のパーティションのパーティション番号を提供します。たとえば次のとおりです: `WITH (PARTITIONS (1, 5))`  
  
-   範囲と個別のパーティションの両方を提供します。たとえば次のとおりです: `WITH (PARTITIONS (2, 4, 6 TO 8))`  
  
-   *\<range>* はパーティション番号として、**TO** で区切って指定できます。たとえば `WITH (PARTITIONS (6 TO 8))` のようになります。  
  
 パーティション テーブルの切り捨てを行うには、テーブルとインデックスが連携している (同じパーティション関数でパーティション分割されている) 必要があります。  
  
## <a name="remarks"></a>解説  
 DELETE ステートメントと比較して、`TRUNCATE TABLE` には次の利点があります。  
  
-   トランザクション ログが使用する領域が削減されます。  
  
     DELETE ステートメントは、一度に 1 行ずつ削除し、削除した各行のエントリをトランザクション ログに記録します。 `TRUNCATE TABLE` は、テーブル データを格納するのに使用するデータ ページの割り当てを解除することによってデータを削除し、ページの割り当ての解除だけをトランザクション ログに記録します。  
  
-   通常、使用されるロックの数が削減されます。  
  
     DELETE ステートメントが行ロックを使用して実行される場合、テーブル内の各行は削除対象としてロックされます。 `TRUNCATE TABLE` では、(スキーマ (SCH-M) ロックを含め) 常にテーブルとページがロックされますが、各行はロックされません。  
  
-   テーブル内にページは一切残されません。  
  
     DELETE ステートメントが実行された後には、テーブルに空のページが残る場合があります。 たとえば、少なくとも 1 つの排他 (LCK_M_X) テーブル ロックを使用しない限り、ヒープ内の空のページの割り当てを解除できません。 削除操作がテーブル ロックを使用しない場合は、テーブル (ヒープ) には多数の空のページが含まれます。 インデックスの場合、削除操作によって空のページが残る場合がありますが、これらのページの割り当てはバックグラウンドのクリーンアップ プロセスによってすばやく解除されます。  
  
 `TRUNCATE TABLE` はテーブルからすべての行を削除しますが、テーブル構造と、テーブルの列、制約、インデックスなどは残ります。 テーブルのデータとテーブル定義を削除する場合は、`DROP TABLE` ステートメントを使用します。  
  
 テーブルに ID 列が含まれている場合は、その列に対するカウンターは、その列に対して定義されたシード値にリセットされます。 シードが定義されていなかった場合は、既定値である 1 が使用されます。 ID カウンターを保持するには、代わりに DELETE を使用します。  
 
 > [!NOTE]
 > `TRUNCATE TABLE` 操作はロールバックできます。
  
## <a name="restrictions"></a>制限  
 次のようなテーブルでは、`TRUNCATE TABLE` は使用できません。  
  
-   FOREIGN KEY 制約で参照されるテーブル それ自体を参照する外部キーを持つテーブルは切り捨てることができます。 
  
-   インデックス付きビューで使用されているテーブル。  
  
-   トランザクション レプリケーションとマージ レプリケーションを使用してパブリッシュされているテーブル。  

-   システムのバージョン情報のテンポラル テーブル。

-   エッジ制約によって参照されるテーブル。  
  
 これらの特性を 1 つ以上持つテーブルには、代わりに DELETE ステートメントを使用します。  
  
 TRUNCATE TABLE では、個別の行の削除がログに記録されないため、この操作によってトリガーをアクティブ化することはできません。 詳細については、「[CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)」を参照してください。 
 
 [!INCLUDE[sssdwfull](../../includes/sssdwfull-md.md)] と [!INCLUDE[sspdw](../../includes/sspdw-md.md)] では:

- EXPLAIN ステートメントでは `TRUNCATE TABLE` を使用できません。

- `TRUNCATE TABLE` は、トランザクション内で実行できません。
  
## <a name="truncating-large-tables"></a>大きなテーブルの切り捨て  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、削除に必要なすべてのエクステントに対する同時ロックを保持することなく、128 を超えるエクステントを持つテーブルの削除または切り捨てを行う機能を備えています。  
  
## <a name="permissions"></a>アクセス許可  
 *table_name* で必要な最小限の権限は `ALTER` です。 `TRUNCATE TABLE` 権限は、特に指定のない限り、テーブル所有者、`sysadmin` 固定サーバー ロール、`db_owner` 固定データベース ロール、および `db_ddladmin` 固定データベース ロールのメンバーに与えられ、譲渡できません。 ただし、`TRUNCATE TABLE` ステートメントをストアド プロシージャなどのモジュール内に組み込み、`EXECUTE AS` 句を使用してそのモジュールに適切な権限を与えることはできます。  
  
## <a name="examples"></a>例  
  
### <a name="a-truncate-a-table"></a>A. テーブルを切り捨てる  
 次の例では、`JobCandidate` テーブルからすべてのデータを削除しています。 `SELECT` ステートメントを `TRUNCATE TABLE` ステートメントの前後に挿入して結果を比較しています。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT COUNT(*) AS BeforeTruncateCount   
FROM HumanResources.JobCandidate;  
GO  
TRUNCATE TABLE HumanResources.JobCandidate;  
GO  
SELECT COUNT(*) AS AfterTruncateCount   
FROM HumanResources.JobCandidate;  
GO  
```  
  
### <a name="b-truncate-table-partitions"></a>B. テーブル パーティションを切り捨てる  
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から[現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)
  
 次の例では、パーティション分割されたテーブルの指定パーティションを切り捨てます。 `WITH (PARTITIONS (2, 4, 6 TO 8))` 構文によりパーティション番号、2、4、6、7、および 8 が切り捨てられます。  
  
```sql  
TRUNCATE TABLE PartitionTable1   
WITH (PARTITIONS (2, 4, 6 TO 8));  
GO  
```  
  
## <a name="see-also"></a>参照  
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [IDENTITY &#40;Property&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)  
  
  

