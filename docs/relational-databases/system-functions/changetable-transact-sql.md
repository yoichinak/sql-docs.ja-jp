---
description: CHANGETABLE (Transact-SQL)
title: CHANGETABLE (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CHANGETABLE_TSQL
- CHANGETABLE
dev_langs:
- TSQL
helpviewer_keywords:
- CHANGETABLE
- change tracking [SQL Server], CHANGETABLE
ms.assetid: d405fb8d-3b02-4327-8d45-f643df7f501a
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4f142f5de6f5580e7b0e21658e4b3c276984cd88
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474702"
---
# <a name="changetable-transact-sql"></a>CHANGETABLE (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  テーブルの変更追跡情報を返します。このステートメントを使用すると、テーブルのすべての変更を返すことも、特定の行の変更追跡情報を取得することもできます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql
CHANGETABLE (  
    { CHANGES table , last_sync_version  
    | VERSION table , <primary_key_values> } )  
[AS] table_alias [ ( column_alias [ ,...n ] )  
  
<primary_key_values> ::=  
( column_name [ , ...n ] ) , ( value [ , ...n ] )  
```  
  
## <a name="arguments"></a>引数  
 変更 *テーブル* 、 *last_sync_version*  
 *Last_sync_version*によって指定されたバージョン以降に発生したテーブルに対するすべての変更の追跡情報を返します。  
  
 *テーブル*  
 追跡した変更を取得するユーザー定義テーブルを指定します。 テーブルで変更の追跡を有効にする必要があります。 1 つ、2 つ、3 つ、または 4 つの部分で構成されるテーブル名を使用できます。 テーブル名は、テーブルのシノニムにすることができます。  
  
 *last_sync_version*  
 変更を取得するときは、呼び出し元のアプリケーションで、変更が必要なポイントを指定する必要があります。 last_sync_version は、その時点を指定します。 この関数により、そのバージョン以降に変更されたすべての行に関する情報が返されます。 アプリケーションは、last_sync_version よりも大きいバージョンの変更を受信するようにクエリを実行しています。  
  
 通常、変更を取得する前に、アプリケーションは **CHANGE_TRACKING_CURRENT_VERSION ()** を呼び出して、次回の変更が必要になったときに使用されるバージョンを取得します。 そのため、アプリケーションは実際の値を解釈または理解する必要はありません。  
  
 last_sync_version は呼び出し元アプリケーションによって取得されるため、アプリケーションで値を保存する必要があります。 アプリケーションでこの値が失われた場合は、データを再初期化する必要があります。  
  
 *last_sync_version* は **bigint**です。 値はスカラーである必要があります。 式によって構文エラーが発生します。  
  
 値が NULL の場合は、追跡されたすべての変更が返されます。  
  
 変更情報の一部またはすべてが、データベース用に構成された保有期間に従ってクリーンアップされている可能性があるため、 *last_sync_version*を検証して、古くなっていないことを確認する必要があります。 詳細については、「transact-sql [&#41;の &#40;transact-sql の CHANGE_TRACKING_MIN_VALID_VERSION ](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md) 」および「 [ALTER DATABASE SET オプション &#40;transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)」を参照してください。  
  
 VERSION *table*, { <primary_key_values> }  
 指定された行の最新の変更追跡情報を返します。 行は主キー値によって識別される必要があります。 <primary_key_values> は主キー列を識別し、値を指定します。 主キー列の名前は、任意の順序で指定できます。  
  
 *Table*  
 変更追跡情報を取得するユーザー定義テーブルを指定します。 テーブルで変更の追跡を有効にする必要があります。 1 つ、2 つ、3 つ、または 4 つの部分で構成されるテーブル名を使用できます。 テーブル名は、テーブルのシノニムにすることができます。  
  
 *column_name*  
 主キー列の名前を指定します。 複数の列名を任意の順序で指定できます。  
  
 *Value*  
 主キーの値を指定します。 複数の主キー列がある場合は、 *column_name* リストに表示される列と同じ順序で値を指定する必要があります。  
  
 と *table_alias* [(*column_alias* [,...*n* ])]  
 CHANGETABLE によって返される結果の名前を提供します。  
  
 *table_alias*  
 CHANGETABLE によって返されるテーブルの別名を指定します。 *table_alias* は必須であり、有効な [識別子](../../relational-databases/databases/database-identifiers.md)である必要があります。  
  
 *column_alias*  
 CHANGETABLE によって返される列の別名または列の別名を指定します (省略可能)。 これにより、結果に重複する名前がある場合に備えて、列名をカスタマイズできます。  
  
## <a name="return-types"></a>戻り値の型  
 **テーブル**  
  
## <a name="return-values"></a>戻り値  
  
### <a name="changetable-changes"></a>CHANGETABLE の変更  
 CHANGES を指定すると、次の列を含む 0 以上の行が返されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|SYS_CHANGE_VERSION|**bigint**|行の最後の変更に関連付けられているバージョンの値|  
|SYS_CHANGE_CREATION_VERSION|**bigint**|最後の挿入操作に関連付けられているバージョンの値。|  
|SYS_CHANGE_OPERATION|**nchar(1)**|変更の種類を示します。<br /><br /> **U** = 更新<br /><br /> **I** = 挿入<br /><br /> **D** = 削除|  
|SYS_CHANGE_COLUMNS|**varbinary(4100)**|Last_sync_version (ベースライン) 以降に変更された列を一覧表示します。 計算列は、変更されたものとして表示されないことに注意してください。<br /><br /> 次のいずれかの条件に該当する場合、値は NULL になります。<br /><br /> 列の変更の追跡が有効になっていない場合。<br /><br /> 操作は挿入操作または削除操作です。<br /><br /> すべての非プライマリキー列が1回の操作で更新されました。 このバイナリ値を直接解釈しないでください。 代わりに、を解釈するには、 [CHANGE_TRACKING_IS_COLUMN_IN_MASK ()](../../relational-databases/system-functions/change-tracking-is-column-in-mask-transact-sql.md)を使用します。|  
|SYS_CHANGE_CONTEXT|**varbinary (128)**|必要に応じて、INSERT、UPDATE、または DELETE ステートメントの一部として [WITH](../../relational-databases/system-functions/with-change-tracking-context-transact-sql.md) 句を使用して指定できるコンテキスト情報を変更します。|  
|\<primary key column value>|ユーザーテーブルの列と同じ|追跡対象テーブルの主キー値。 これらの値は、ユーザーテーブル内の各行を一意に識別します。|  
  
### <a name="changetable-version"></a>CHANGETABLE バージョン  
 VERSION を指定すると、次の列を含む 1 つの行が返されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|SYS_CHANGE_VERSION|**bigint**|現在の行に関連付けられている変更バージョンの値です。<br /><br /> 変更の追跡の保有期間より長い期間にわたって変更が行われていない場合、または変更の追跡が有効になってから行が変更されていない場合、この値は NULL になります。|  
|SYS_CHANGE_CONTEXT|**varbinary (128)**|INSERT、UPDATE、DELETE の各ステートメントの一部として WITH 句を使用することによってオプションで指定できる変更のコンテキスト情報です。|  
|\<primary key column value>|ユーザーテーブルの列と同じ|追跡対象テーブルの主キー値。 これらの値は、ユーザーテーブル内の各行を一意に識別します。|  
  
## <a name="remarks"></a>解説  
 CHANGETABLE 関数は、クエリの FROM 句の中でテーブルとして使用されるのが一般的です。  
  
## <a name="changetablechanges"></a>CHANGETABLE(CHANGES...)  
 新規または変更された行の行データを取得するには、主キー列を使用して、結果セットをユーザーテーブルに結合します。 *Last_sync_version*値以降に同じ行に複数の変更が加えられた場合でも、変更されたユーザーテーブルの各行に対して1行だけが返されます。  
  
 主キー列の変更は更新としてマークされません。 主キーの値が変更された場合は、古い値の削除と新しい値の挿入と見なされます。  
  
 行を削除した後、古い主キーを持つ行を挿入すると、その変更は行のすべての列に対する更新として表示されます。  
  
 SYS_CHANGE_OPERATION 列と SYS_CHANGE_COLUMNS 列に対して返される値は、指定されたベースライン (last_sync_version) に対して相対的です。 たとえば、バージョン10で挿入操作が実行され、バージョン15で更新操作が行われた場合、ベースライン *last_sync_version* が12の場合、更新が報告されます。 *Last_sync_version*値が8の場合は、挿入がレポートされます。 SYS_CHANGE_COLUMNS では、計算列は更新された列として報告されません。  
  
 一般に、ユーザー テーブルに対するデータの挿入、更新、または削除の操作は、MERGE ステートメントも含め、すべて追跡されます。  
  
 ユーザー テーブルのデータに影響する操作のうち、追跡されない操作は次のとおりです。  
  
-   UPDATETEXT ステートメントの実行  
  
     このステートメントは将来のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では削除される予定であり、非推奨とされます。 ただし、を使用して行われた変更は、です。UPDATE ステートメントの WRITE 句は追跡されます。  
  
-   TRUNCATE TABLE を使用した行の削除  
  
     テーブルが切り捨てられると、テーブルに関連付けられている変更追跡バージョン情報はリセットされ、変更の追跡を有効にした直後と同じ状態になります。 クライアントアプリケーションは、常に最終同期バージョンを検証する必要があります。 テーブルが切り捨てられている場合、検証は失敗します。  
  
## <a name="changetableversion"></a>CHANGETABLE(VERSION...)  
 存在しない主キーが指定されている場合は、空の結果セットが返されます。  
  
 保有期間より長い期間にわたって変更が行われていない場合 (クリーンアップによって変更情報が削除されている場合など) や、テーブルに対して変更の追跡を有効にしてからまだ行が変更されていない場合、SYS_CHANGE_VERSION の値は NULL になります。  
  
## <a name="permissions"></a>アクセス許可  
 変更追跡情報を取得するには、 *テーブル* 値によって指定されたテーブルに対する次の権限が必要です。  
  
-   主キー列に対する SELECT 権限  
  
-   VIEW CHANGE TRACKING  
  
## <a name="examples"></a>例  
  
### <a name="a-returning-rows-for-an-initial-synchronization-of-data"></a>A. データの初期同期のための行を返す  
 次の例は、テーブル データを初期同期するためにデータを取得する方法を示しています。 このクエリは、すべての行データとそれに関連付けられたバージョンを返します。 その後、同期されたデータを格納するシステムにこのデータを挿入または追加できます。  
  
```sql  
-- Get all current rows with associated version  
SELECT e.[Emp ID], e.SSN, e.FirstName, e.LastName,  
    c.SYS_CHANGE_VERSION, c.SYS_CHANGE_CONTEXT  
FROM Employees AS e  
CROSS APPLY CHANGETABLE   
    (VERSION Employees, ([Emp ID], SSN), (e.[Emp ID], e.SSN)) AS c;  
```  
  
### <a name="b-listing-all-changes-that-were-made-since-a-specific-version"></a>B. 特定のバージョン以降に加えられたすべての変更を一覧表示する  
 次の例では、指定したバージョン (`@last_sync_version)` 以降にテーブルで行われたすべての変更を一覧表示します。 [Emp ID] と SSN は、複合主キーの列です。  
  
```sql  
DECLARE @last_sync_version bigint;  
SET @last_sync_version = <value obtained from query>;  
SELECT [Emp ID], SSN,  
    SYS_CHANGE_VERSION, SYS_CHANGE_OPERATION,  
    SYS_CHANGE_COLUMNS, SYS_CHANGE_CONTEXT   
FROM CHANGETABLE (CHANGES Employees, @last_sync_version) AS C;  
```  
  
### <a name="c-obtaining-all-changed-data-for-a-synchronization"></a>C. 同期のために変更されたすべてのデータを取得する  
 次の例は、変更されたデータをすべて取得する方法を示しています。 このクエリでは、変更追跡情報をユーザー テーブルと結合して、ユーザー テーブルの情報が返されるようにしています。 は、削除された `LEFT OUTER JOIN` 行に対して行が返されるように使用されます。  
  
```sql  
-- Get all changes (inserts, updates, deletes)  
DECLARE @last_sync_version bigint;  
SET @last_sync_version = <value obtained from query>;  
SELECT e.FirstName, e.LastName, c.[Emp ID], c.SSN,  
    c.SYS_CHANGE_VERSION, c.SYS_CHANGE_OPERATION,  
    c.SYS_CHANGE_COLUMNS, c.SYS_CHANGE_CONTEXT   
FROM CHANGETABLE (CHANGES Employees, @last_sync_version) AS c  
    LEFT OUTER JOIN Employees AS e  
        ON e.[Emp ID] = c.[Emp ID] AND e.SSN = c.SSN;  
```  
  
### <a name="d-detecting-conflicts-by-using-changetableversion"></a>D. CHANGETABLE (VERSION...) を使用して競合を検出する  
 次の例は、行が前回の同期以降に変更されていない場合にのみ、行を更新する方法を示しています。 `CHANGETABLE` を使用して、特定の行のバージョン番号を取得しています。 行が更新されている場合、変更は行われず、クエリは行に対する最新の変更に関する情報を返します。  
  
```sql  
-- @last_sync_version must be set to a valid value  
UPDATE  
    SalesLT.Product  
SET  
    ListPrice = @new_listprice  
FROM  
    SalesLT.Product AS P  
WHERE  
    ProductID = @product_id AND  
    @last_sync_version >= ISNULL (  
        (SELECT CT.SYS_CHANGE_VERSION FROM   
            CHANGETABLE(VERSION SalesLT.Product,  
            (ProductID), (P.ProductID)) AS CT),  
        0);  
```  
  
## <a name="see-also"></a>参照  
 [変更追跡関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [データ変更の追跡 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [CHANGE_TRACKING_IS_COLUMN_IN_MASK &#40;Transact-sql&#41;](../../relational-databases/system-functions/change-tracking-is-column-in-mask-transact-sql.md)   
 [CHANGE_TRACKING_CURRENT_VERSION &#40;Transact-sql&#41;](../../relational-databases/system-functions/change-tracking-current-version-transact-sql.md)   
 [CHANGE_TRACKING_MIN_VALID_VERSION &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)  
  
  
