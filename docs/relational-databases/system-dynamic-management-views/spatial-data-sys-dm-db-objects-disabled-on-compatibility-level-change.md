---
description: dm_db_objects_disabled_on_compatibility_level_change (Transact-sql)
title: dm_db_objects_disabled_on_compatibility_level_change (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_objects_disabled_on_compatibility_level_change
- dm_db_objects_disabled_on_compatibility_level_change_TSQL
- sys.dm_db_objects_disabled_on_compatibility_level_change
- sys.dm_db_objects_disabled_on_compatibility_level_change_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_objects_disabled_on_compatibility_level_change catalog view
ms.assetid: a5d70064-0330-48b9-b853-01eba50755d0
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f4779675cd37f6f49f90ab01fa17e5f5e9259260
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89519205"
---
# <a name="spatial-data---sysdm_db_objects_disabled_on_compatibility_level_change"></a>空間データ-sys. dm_db_objects_disabled_on_compatibility_level_change
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  で互換性レベルを変更した結果として無効になるインデックスと制約の一覧を示し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 更新または互換性レベルの変更後に、式が空間 Udt を使用する、保存される計算列を含むインデックスおよび制約は無効になります。 互換性レベルの変更の影響を判断するには、この動的管理関数を使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
sys.dm_db_objects_disabled_on_compatibility_level_change ( compatibility_level )   
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 引数  
 *compatibility_level*  
 設定を計画している互換性レベルを識別する**int** 。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**class**|**int**|1 = 制約<br /><br /> 7 = インデックスとヒープ|  
|**class_desc**|**nvarchar(60)**|制約の場合は OBJECT または COLUMN<br /><br /> インデックスとヒープのインデックス|  
|**major_id**|**int**|制約の OBJECT ID <br /><br /> インデックスとヒープを含むテーブルのオブジェクト ID|  
|**minor_id**|**int**|制約の場合は NULL<br /><br /> インデックスおよびヒープの場合は Index_id|  
|**関係**|**nvarchar(60)**|制約またはインデックスが無効になる原因となっている依存関係の説明。 アップグレード中に発生した警告にも同じ値が使用されます。 具体的には次のものがあります。<br /><br /> 組み込み用の "space"<br /><br /> システム UDT の場合は "geometry"<br /><br /> システム UDT のメソッドの場合は "geography::Parse"|  
  
## <a name="general-remarks"></a>全般的な解説  
 互換性レベルを変更すると、一部の組み込み関数を使用している保存される計算列が無効になります。 データベースをアップグレードすると、Geometry メソッドまたは Geography メソッドを使用している保存される計算列も無効になります。  
  
### <a name="which-functions-cause-persisted-computed-columns-to-be-disabled"></a>保存された計算列が無効になる関数を教えてください。  
 保存される計算列の式で次の関数を使用すると、互換性レベルが80から90に変更されたときに、これらの列を参照するインデックスと制約が無効になります。  
  
-   **IsNumeric**  
  
 保存される計算列の式で次の関数が使用されている場合、互換性レベルが 100 から 110 以上に変更されると、これらの列を参照するインデックスと制約が無効になります。  
  
-   **Soundex**  
  
-   **Geography:: GeomFromGML**  
  
-   **Geography:: STGeomFromText**  
  
-   **Geography:: STLineFromText**  
  
-   **Geography:: STPolyFromText**  
  
-   **Geography:: STMPointFromText**  
  
-   **Geography:: STMLineFromText**  
  
-   **Geography:: STMPolyFromText**  
  
-   **Geography:: STGeomCollFromText**  
  
-   **Geography:: STGeomFromWKB**  
  
-   **Geography:: STLineFromWKB**  
  
-   **Geography:: STPolyFromWKB**  
  
-   **Geography:: STMPointFromWKB**  
  
-   **Geography:: STMLineFromWKB**  
  
-   **Geography:: STMPolyFromWKB**  
  
-   **Geography:: STUnion**  
  
-   **Geography:: STIntersection**  
  
-   **Geography:: STDifference**  
  
-   **Geography:: STSymDifference**  
  
-   **Geography:: STBuffer**  
  
-   **Geography:: BufferWithTolerance**  
  
-   **Geography:: Parse**  
  
-   **Geography:: Reduce**  
  
### <a name="behavior-of-the-disabled-objects"></a>無効なオブジェクトの動作  
 **インデックス**  
  
 クラスター化インデックスが無効になっている場合、または非クラスター化インデックスが強制されている場合は、"インデックス '% \* が原因で、クエリプロセッサはプランを作成できません。ls ' テーブルまたはビュー '%。 \*ls ' は無効になっています。 " これらのオブジェクトを再度有効にするには、アップグレード後 **に ALTER INDEX ON...リビルド**。  
  
 **ヒープ**  
  
 無効になったヒープが含まれているテーブルを使用すると、次のエラーが発生します。 これらのオブジェクトを再度有効にするには、アップグレード後 **に ALTER INDEX ALL を呼び出すことによって再構築します...リビルド**。  
  
```  
// ErrorNumber: 8674  
// ErrorSeverity: EX_USER  
// ErrorFormat: The query processor is unable to produce a plan because the table or view '%.*ls' is disabled.  
// ErrorCause: The table has a disabled heap.   
// ErrorCorrectiveAction: Rebuild the disabled heap to enable it.   
// ErrorInserts: table or view name   
// ErrorOwner: mtintor   
// ErrorFirstProduct: SQL11  
```  
  
 オンライン操作中にヒープを再構築しようとすると、エラーが発生します。  
  
 **CHECK 制約と外部キー**  
  
 無効になっている check 制約と外部キーでは、エラーは発生しません。 ただし、行が変更された場合、制約は適用されません。 これらのオブジェクトを再度有効にするには、アップグレード後に **ALTER TABLE... を呼び出して、制約を確認します。CHECK 制約**。  
  
 **保存される計算列**  
  
 1 つの列を無効にすることはできないので、クラスター化インデックスまたはヒープを無効にすると、テーブル全体が無効になります。  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 VIEW DATABASE STATE 権限が必要です。  
  
## <a name="example"></a>例  
 次の例では、互換性レベルを120に変更することによって影響を受けるオブジェクトを検索するために、dm_db_objects_disabled_on_compatibility_level_change に対するクエリを示します **。**  
  
```sql  
SELECT * FROM sys.dm_db_objects_disabled_on_compatibility_level_change(120);  
GO  
  
```  
  
  
