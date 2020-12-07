---
description: sp_primarykeys (Transact-sql)
title: sp_primarykeys (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_primarykeys_TSQL
- sp_primarykeys
dev_langs:
- TSQL
helpviewer_keywords:
- sp_primarykeys
ms.assetid: 0f76dd31-5b7b-4209-9e2e-b9ed5cac164d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c5b967d8ac3d30147e583ffa6268cdd8d2a8d282
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89534999"
---
# <a name="sp_primarykeys-transact-sql"></a>sp_primarykeys (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定されたリモート テーブルの主キー列を、キー列ごとに 1 行ずつ返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_primarykeys [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @table_server = ] 'table_server'_` 主キー情報を返すリンクサーバーの名前を指定します。 *table_server* は **sysname**であり、既定値はありません。  
  
`[ @table_name = ] 'table_name'` 主キー情報を提供するテーブルの名前を指定します。 *table_name*は **sysname**,、既定値は NULL です。  
  
`[ @table_schema = ] 'table_schema'` テーブルスキーマを示します。 *table_schema* は **sysname**,、既定値は NULL です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境では、これはテーブル所有者に相当します。  
  
`[ @table_catalog = ] 'table_catalog'` 指定した *table_name* が存在するカタログの名前を指定します。 環境では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、これはデータベース名に対応しています。 *table_catalog* は **sysname**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|テーブルカタログ。|  
|**TABLE_SCHEM**|**sysname**|テーブル スキーマ。|  
|**TABLE_NAME**|**sysname**|テーブルの名前。|  
|**COLUMN_NAME**|**sysname**|列の名前です。|  
|**KEY_SEQ**|**int**|複数列の主キーの列のシーケンス番号。|  
|**PK_NAME**|**sysname**|主キー識別子。 データソースに該当しない場合は NULL を返します。|  
  
## <a name="remarks"></a>解説  
 **sp_primarykeys**は、 *table_server*に対応する OLE DB プロバイダーの**IDBSchemaRowset**インターフェイスの PRIMARY_KEYS 行セットを照会することによって実行されます。 返される行を制限するために、 *table_name*、 *table_schema*、 *table_catalog*、および *列* の各パラメーターがこのインターフェイスに渡されます。  
  
 指定されたリンクサーバーの OLE DB プロバイダーが**IDBSchemaRowset**インターフェイスの PRIMARY_KEYS 行セットをサポートしていない場合、 **sp_primarykeys**は空の結果セットを返します。  
  
## <a name="permissions"></a>アクセス許可  
 スキーマに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、データベース内のテーブルの主キー列をサーバーから返し `LONDON1` `HumanResources.JobCandidate` [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ます。  
  
```  
EXEC sp_primarykeys @table_server = N'LONDON1',   
   @table_name = N'JobCandidate',  
   @table_catalog = N'AdventureWorks2012',   
   @table_schema = N'HumanResources';  
```  
  
## <a name="see-also"></a>参照  
 [分散クエリストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_catalogs &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_foreignkeys &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_indexes &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_tables_ex &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
