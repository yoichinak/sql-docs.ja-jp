---
description: JSON_VALUE (Transact-SQL)
title: JSON_VALUE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2020
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- JSON_VALUE
- JSON_VALUE_TSQL
helpviewer_keywords:
- JSON_VALUE function
- JSON, extracting
- JSON, querying
ms.assetid: cd016e14-11eb-4eaf-bf05-c7cfcc820a10
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
monikerRange: = azuresqldb-current||= azure-sqldw-latest||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: f22175349162bac226d41f63ca66743de0668b6e
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88364418"
---
# <a name="json_value-transact-sql"></a>JSON_VALUE (Transact-SQL)

[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

 JSON 文字列からスカラー値を抽出します。  
  
 JSON 文字列からスカラー値ではなくオブジェクトまたは配列を抽出する場合は、「[JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)」を参照してください。 **JSON_VALUE** と **JSON_QUERY** の違いについては、「[JSON_VALUE と JSON_QUERY を比較する](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md#JSONCompare)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
JSON_VALUE ( expression , path )  
```  
  
## <a name="arguments"></a>引数

 *式 (expression)*  
 式。 通常、変数または JSON テキストを含む列の名前。  

 **JSON_VALUE** が、*path* によって識別される値を検出する前に *expression* で無効な JSON を検出した場合、関数はエラーを返します。 **JSON_VALUE** が *path* によって識別される値を検出できない場合、テキスト全体がスキャンされ、*expression* のどこかで無効な JSON を検出した場合はエラーを返します。
  
 *path*  
 抽出するプロパティを指定する JSON のパス。 詳細については、「[JSON パス式 &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)」を参照してください。  

[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] と [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)] では、*path* の値として変数を指定できます。
  
 *path* の書式が有効でない場合、**JSON_VALUE** はエラーを返します。  
  
## <a name="return-value"></a>戻り値

 型 nvarchar (4000) の 1 つのテキスト値を返します。 返される値の照合順序は、入力された式の照合順序と同じです。  
  
 値が 4,000 文字を超える場合:  
  
- 厳密でないモードでは、**JSON_VALUE** は null を返します。  
  
- 厳格モードでは、**JSON_VALUE** はエラーを返します。  
  
 4,000 文字を超えるスカラー値を返す必要がある場合は、**JSON_VALUE** の代わりに **OPENJSON** を使用します。 詳細については、「 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)」をご覧ください。  
  
## <a name="remarks"></a>解説

### <a name="lax-mode-and-strict-mode"></a>厳密でないモードと厳格モード

 次の JSON テキストを考えてみます。  
  
```json  
DECLARE @jsonInfo NVARCHAR(MAX)

SET @jsonInfo=N'{  
     "info":{    
       "type":1,  
       "address":{    
         "town":"Bristol",  
         "county":"Avon",  
         "country":"England"  
       },  
       "tags":["Sport", "Water polo"]  
    },  
    "type":"Basic"  
 }'  
```  
  
 次の表は、厳密でないモードと厳格モードでの **JSON_VALUE** の動作を比較します。 省略可能なパス モード (厳密でない、または厳格) の指定について詳しくは、「[JSON パス式 &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)」を参照してください。  
  
|Path|厳密でないモードでの戻り値|厳格モードでの戻り値|詳細情報|  
|----------|------------------------------|---------------------------------|---------------|  
|$|NULL|エラー|スカラー値ではありません。<br /><br /> 代わりに **JSON_QUERY** を使用します。|  
|$.info.type|N'1'|N'1'|該当なし|  
|$.info.address.town|N'Bristol'|N'Bristol'|該当なし|  
|$.info."address"|NULL|エラー|スカラー値ではありません。<br /><br /> 代わりに **JSON_QUERY** を使用します。|  
|$.info.tags|NULL|エラー|スカラー値ではありません。<br /><br /> 代わりに **JSON_QUERY** を使用します。|  
|$.info.type[0]|NULL|エラー|配列ではありません。|  
|$.info.none|NULL|エラー|プロパティが存在しません。|  
| &nbsp; | &nbsp; | &nbsp; | &nbsp; |
  
## <a name="examples"></a>例  
  
### <a name="example-1"></a>例 1
 次の例では、クエリの結果に JSON のプロパティの値 `town` と `state` を使用します。 **JSON_VALUE** がソースの照合順序を保持するため、結果の並べ替え順序が `jsonInfo` 列の照合順序に依存します。 

> [!NOTE]
> (この例では、`Person.Person` という名前のテーブルが JSON テキストの `jsonInfo` 列を含み、またこの列が、前の厳密でないモードと厳格モードの説明で示した構造を持っていることを前提としています。 AdventureWorks サンプル データベースでは、`Person` テーブルは実は `jsonInfo` 列を含んでいません。)
  
```sql  
SELECT FirstName, LastName,
 JSON_VALUE(jsonInfo,'$.info.address[0].town') AS Town
FROM Person.Person
WHERE JSON_VALUE(jsonInfo,'$.info.address[0].state') LIKE 'US%'
ORDER BY JSON_VALUE(jsonInfo,'$.info.address[0].town')
```  
  
### <a name="example-2"></a>例 2
 次の例では、ローカル変数に JSON プロパティの値 `town` を抽出します。  
  
```sql
DECLARE @jsonInfo NVARCHAR(MAX)
DECLARE @town NVARCHAR(32)

SET @jsonInfo=N'{"info":{"address":[{"town":"Paris"},{"town":"London"}]}}';

SET @town=JSON_VALUE(@jsonInfo,'$.info.address[0].town'); -- Paris
SET @town=JSON_VALUE(@jsonInfo,'$.info.address[1].town'); -- London
```  
  
### <a name="example-3"></a>例 3
 次の例では、JSON のプロパティの値に基づいて、計算列を作成します。  
  
```sql  
CREATE TABLE dbo.Store
 (
  StoreID INT IDENTITY(1,1) NOT NULL,
  Address VARCHAR(500),
  jsonContent NVARCHAR(4000),
  Longitude AS JSON_VALUE(jsonContent, '$.address[0].longitude'),
  Latitude AS JSON_VALUE(jsonContent, '$.address[0].latitude')
 )
```  
  
## <a name="see-also"></a>関連項目
 [JSON パス式 &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [JSON データ &#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md)  
  
