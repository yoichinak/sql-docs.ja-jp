---
description: sp_indexes (Transact-SQL)
title: sp_indexes (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_indexes_TSQL
- sp_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sp_indexes
ms.assetid: 25469e72-9d95-463f-912a-193471c8f5e2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 133a7fb36ff65444853c1bdeb44fdefabe4aab4f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547898"
---
# <a name="sp_indexes-transact-sql"></a>sp_indexes (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定されたリモート テーブルに関するインデックス情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_indexes [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_db' ]   
     [ , [ @index_name = ] 'index_name' ]   
     [ , [ @is_unique = ] 'is_unique' ]  
```  
  
## <a name="arguments"></a>引数  
 [ @table_server =] '*table_server*'  
 テーブル情報を要求しているを実行しているリンクサーバーの名前を指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。 *table_server* は **sysname**であり、既定値はありません。  
  
 [ @table_name =] '*table_name*'  
 インデックス情報を提供する対象のリモート テーブルの名前です。 *table_name* は **sysname**,、既定値は NULL です。 NULL の場合、指定したデータベースのすべてのテーブルが返されます。  
  
 [ @table_schema =] '*table_schema*'  
 テーブルスキーマを指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境では、これはテーブル所有者に相当します。 *table_schema* は **sysname**,、既定値は NULL です。  
  
 [ @table_catalog =] '*table_db*'  
 *Table_name*が存在するデータベースの名前を指定します。 *table_db* は **sysname**,、既定値は NULL です。 NULL の場合、 *table_db* の既定値は **master**です。  
  
 [ @index_name =] '*index_name*'  
 情報を要求する対象のインデックスの名前です。 *index* の **sysname**,、既定値は NULL です。  
  
 [ @is_unique =] '*is_unique*'  
 情報を返す対象のインデックスの種類を指定します。 *is_unique* の部分は **bit**で、既定値は NULL です。次のいずれかの値を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|1|一意のインデックスに関する情報を返します。|  
|0|一意ではないインデックスに関する情報を返します。|  
|NULL|すべてのインデックスに関する情報を返します。|  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|TABLE_CAT|**sysname**|指定したテーブルが存在するデータベースの名前です。|  
|TABLE_SCHEM|**sysname**|テーブルのスキーマ。|  
|TABLE_NAME|**sysname**|リモートテーブルの名前。|  
|NON_UNIQUE|**smallint**|インデックスが一意であるか一意でないかを示します。<br /><br /> 0 = 一意<br /><br /> 1 = 一意ではない|  
|INDEX_QUALIFER|**sysname**|インデックス所有者の名前。 一部の DBMS 製品では、テーブル所有者以外のユーザーがインデックスを作成できます。 で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、この列は常に **TABLE_NAME**と同じです。|  
|INDEX_NAME|**sysname**|インデックス名。|  
|TYPE|**smallint**|インデックスの種類:<br /><br /> 0 = テーブルの統計<br /><br /> 1 = クラスター化<br /><br /> 2 = ハッシュされる<br /><br /> 3 = その他|  
|ORDINAL_POSITION|**int**|インデックス内の列の序数位置。 インデックスの最初の列は 1 です。 この列は常に値が返されます。|  
|COLUMN_NAME|**sysname**|返される TABLE_NAME の各列に対応する列名です。|  
|ASC_OR_DESC|**varchar**|照合順序で使用される順序を次に示します。<br /><br /> A = 昇順<br /><br /> D = 降順<br /><br /> NULL = 適用なし<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は常に A を返します。|  
|CARDINALITY|**int**|テーブル内の行数またはインデックス内の一意な値の個数です。|  
|PAGES|**int**|インデックスまたはテーブルを格納するページ数です。|  
|FILTER_CONDITION|**nvarchar (** 4000 **)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では値は返されません。|  
  
## <a name="permissions"></a>アクセス許可  
 スキーマに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、リンクサーバー上のデータベースのテーブルから、すべてのインデックス情報が返さ `Employees` `AdventureWorks2012` `Seattle1` れます。  
  
```  
EXEC sp_indexes @table_server = 'Seattle1',   
   @table_name = 'Employee',   
   @table_schema = 'HumanResources',  
   @table_catalog = 'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>参照  
 [分散クエリストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_catalogs &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_foreignkeys &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_tables_ex &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
