---
description: sp_columns_ex (Transact-SQL)
title: sp_columns_ex (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_columns_ex
- sp_columns_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_columns_ex
ms.assetid: c12ef6df-58c6-4391-bbbf-683ea874bd81
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9ea62e350628099685b372362a3d6d075a90367b
ms.sourcegitcommit: b3a711a673baebb2ff10d7142b209982b46973ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2020
ms.locfileid: "93364841"
---
# <a name="sp_columns_ex-transact-sql"></a>sp_columns_ex (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定したリンク サーバー テーブルに対し、1 列あたり 1 行の列情報を返します。 *列* が指定されている場合、 **sp_columns_ex** は特定の列についてのみ列情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_columns_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @column_name = ] 'column' ]   
     [ , [ @ODBCVer = ] 'ODBCVer' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @table_server = ] 'table_server'` 列情報を返すリンクサーバーの名前を指定します。 *table_server* は **sysname** であり、既定値はありません。  
  
`[ @table_name = ] 'table_name'` 列情報を返すテーブルの名前を指定します。 *table_name* は **sysname** ,、既定値は NULL です。  
  
`[ @table_schema = ] 'table_schema'` 列情報を返すテーブルのスキーマ名を指定します。 *table_schema* は **sysname** ,、既定値は NULL です。  
  
`[ @table_catalog = ] 'table_catalog'` 列情報を返すテーブルのカタログ名を指定します。 *table_catalog* は **sysname** ,、既定値は NULL です。  
  
`[ @column_name = ] 'column'` 情報を提供するデータベース列の名前を指定します。 *列* は **sysname** ,、既定値は NULL です。  
  
`[ @ODBCVer = ] 'ODBCVer'` 使用されている ODBC のバージョンを示します。 *Odbcver* は **int** ,、既定値は2です。 これは、ODBC バージョン2を示します。 有効な値は2または3です。 バージョン 2 と 3 の動作の相違については、ODBC の SQLColumns 仕様を参照してください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|テーブルまたはビュー修飾子の名前。 さまざまな DBMS 製品では、3つの要素で構成するテーブル ( _修飾子_ ) がサポート **しています。**_所有者_**。**_名前_ )。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]この列のは、データベース名を表します。 一部の製品では、テーブルのデータベース環境のサーバー名を表します。 このフィールドは NULL にすることができます。|  
|**TABLE_SCHEM**|**sysname**|テーブルまたはビュー所有者の名前。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、この列は、テーブルを作成したデータベース ユーザーの名前を表します。 このフィールドは常に値を返します。|  
|**TABLE_NAME**|**sysname**|テーブルまたはビューの名前。 このフィールドは常に値を返します。|  
|**COLUMN_NAME**|**sysname**|返される **TABLE_NAME** の各列の列名。 このフィールドは常に値を返します。|  
|**DATA_TYPE**|**smallint**|ODBC のデータ型を表す整数値。 ODBC のデータ型にマップできないデータ型の場合、この値は NULL になります。 ネイティブデータ型の名前が **TYPE_NAME** 列に返されます。|  
|**TYPE_NAME**|**varchar (** 13 **)**|データ型を表す文字列。 基になる DBMS は、このデータ型の名前を提示します。|  
|**COLUMN_SIZE**|**int**|有効桁数。 **有効桁数** 列の戻り値は、10進数値です。|  
|**BUFFER_LENGTH**|**int**|データの転送サイズ。1|  
|**DECIMAL_DIGITS**|**smallint**|小数点の右側の桁数。|  
|**NUM_PREC_RADIX**|**smallint**|数値型の基数。|  
|**NULLABLE**|**smallint**|Null 値の許容属性を指定します。<br /><br /> 1 = NULL 値を許容します。<br /><br /> 0 = NULL 値を許容しません。|  
|**備考**|**varchar (** 254 **)**|このフィールドは常に NULL を返します。|  
|**COLUMN_DEF**|**varchar (** 254 **)**|列の既定値です。|  
|**SQL_DATA_TYPE**|**smallint**|記述子の TYPE フィールドでの SQL データ型の値です。 この列は、 **datetime** および SQL-92 **interval** データ型を除き、 **DATA_TYPE** 列と同じです。 この列は常に値が返されます。|  
|**SQL_DATETIME_SUB**|**smallint**|**Datetime** および SQL-92 **interval** データ型のサブタイプコード。 他のデータ型の場合、この列は NULL を返します。|  
|**CHAR_OCTET_LENGTH**|**int**|文字型または整数型の列の最大長 (バイト単位)。 他のすべてのデータ型については、この列は NULL を返します。|  
|**ORDINAL_POSITION**|**int**|テーブル内の列の序数位置。 テーブルの最初の列は1です。 この列は常に値が返されます。|  
|**IS_NULLABLE**|**varchar (** 254 **)**|テーブル内の列の null 値の許容属性。 ISO ルールの後に、null 値の許容属性が決定されます。 ISO SQL に準拠している DBMS では、空の文字列を返すことはできません。<br /><br /> YES = 列に NULL を含むことができます。<br /><br /> NO = 列に NULL を含めることはできません。<br /><br /> Null 値許容属性が不明の場合、この列は長さ0の文字列を返します。<br /><br /> この列に返される値は、 **Null 許容** 列に対して返される値とは異なります。|  
|**SS_DATA_TYPE**|**tinyint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型。拡張ストアドプロシージャによって使用されます。|  
  
 1 詳細については、Microsoft ODBC のドキュメントを参照してください。  
  
## <a name="remarks"></a>注釈  
- **sp_columns_ex** は、 *table_server* に対応する OLE DB プロバイダーの **IDBSchemaRowset** インターフェイスの columns 行セットを照会することによって実行されます。 返される行を制限するために、 *table_name* 、 *table_schema* 、 *table_catalog* 、および *列* の各パラメーターがこのインターフェイスに渡されます。  
  
- 指定されたリンクサーバーの OLE DB プロバイダーが **IDBSchemaRowset** インターフェイスの columns 行セットをサポートしていない場合、 **sp_columns_ex** は空の結果セットを返します。  
  
- **sp_columns_ex** は、区切られた識別子の要件に従います。 詳細については、「[データベース識別子](../../relational-databases/databases/database-identifiers.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 スキーマに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、リンク サーバー `JobTitle` 上の [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースにある、`HumanResources.Employee` テーブルの `Seattle1` 列のデータ型を返します。  
  
```  
EXEC sp_columns_ex 'Seattle1',   
   'Employee',   
   'HumanResources',   
   'AdventureWorks2012',   
   'JobTitle';  
```  
  
## <a name="see-also"></a>参照  
 [sp_catalogs &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_foreignkeys &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_indexes &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_primarykeys &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [sp_tables_ex &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
