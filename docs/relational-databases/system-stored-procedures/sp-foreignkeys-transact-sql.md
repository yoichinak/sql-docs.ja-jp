---
description: sp_foreignkeys (Transact-sql)
title: sp_foreignkeys (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_foreignkeys_TSQL
- sp_foreignkeys
dev_langs:
- TSQL
helpviewer_keywords:
- sp_foreignkeys
ms.assetid: 935fe385-19ff-41a4-8d0b-30618966991d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8a87d51fff7179ece3442e2459d8d2c5a96c8029
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543404"
---
# <a name="sp_foreignkeys-transact-sql"></a>sp_foreignkeys (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  リンクサーバー内のテーブルの主キーを参照する外部キーを返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_foreignkeys [ @table_server = ] 'table_server'   
     [ , [ @pktab_name = ] 'pktab_name' ]   
     [ , [ @pktab_schema = ] 'pktab_schema' ]   
     [ , [ @pktab_catalog = ] 'pktab_catalog' ]   
     [ , [ @fktab_name = ] 'fktab_name' ]   
     [ , [ @fktab_schema = ] 'fktab_schema' ]   
     [ , [ @fktab_catalog = ] 'fktab_catalog' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @table_server = ] 'table_server'` テーブル情報を返すリンクサーバーの名前を指定します。 *table_server* は **sysname**であり、既定値はありません。  
  
`[ @pktab_name = ] 'pktab_name'` 主キーを持つテーブルの名前を指定します。 *pktab_name* は **sysname**,、既定値は NULL です。  
  
`[ @pktab_schema = ] 'pktab_schema'` 主キーを持つスキーマの名前を指定します。 *pktab_schema*は **sysname**,、既定値は NULL です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、所有者名に相当します。  
  
`[ @pktab_catalog = ] 'pktab_catalog'` 主キーを持つカタログの名前を指定します。 *pktab_catalog*は **sysname**,、既定値は NULL です。 では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] これにはデータベース名が含まれます。  
  
`[ @fktab_name = ] 'fktab_name'` 外部キーを持つテーブルの名前を指定します。 *fktab_name*は **sysname**,、既定値は NULL です。  
  
`[ @fktab_schema = ] 'fktab_schema'` 外部キーを持つスキーマの名前を指定します。 *fktab_schema*は **sysname**,、既定値は NULL です。  
  
`[ @fktab_catalog = ] 'fktab_catalog'` 外部キーを持つカタログの名前を指定します。 *fktab_catalog*は **sysname**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
 さまざまな DBMS 製品では、3つの要素で構成するテーブル (_カタログ_) がサポート**しています。**_スキーマ_**。**_テーブル_)。これは、結果セットで表されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**PKTABLE_CAT**|**sysname**|主キーが設定されたテーブルのカタログです。|  
|**PKTABLE_SCHEM**|**sysname**|主キーが設定されたテーブルのスキーマです。|  
|**PKTABLE_NAME**|**sysname**|テーブルの名前 (主キーを含む)。 このフィールドは常に値を返します。|  
|**PKCOLUMN_NAME**|**sysname**|返される **TABLE_NAME** の各列の主キー列の名前。 このフィールドは常に値を返します。|  
|**FKTABLE_CAT**|**sysname**|外部キーが設定されたテーブルのカタログです。|  
|**FKTABLE_SCHEM**|**sysname**|外部キーが設定されたテーブルのスキーマです。|  
|**FKTABLE_NAME**|**sysname**|外部キーが設定されたテーブルの名前です。 このフィールドは常に値を返します。|  
|**FKCOLUMN_NAME**|**sysname**|返される TABLE_NAME の各列の外部キー列の名前。 このフィールドは常に値を返します。|  
|**KEY_SEQ**|**smallint**|複数列の主キーの列のシーケンス番号。 このフィールドは常に値を返します。|  
|**UPDATE_RULE**|**smallint**|SQL 操作が更新である場合に、外部キーに適用されるアクションです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、次の列に対して0、1、または2を返します。<br /><br /> 0 = 外部キーに対して連鎖変更を行います。<br /><br /> 1 = 外部キーが存在する場合、アクションの変更はありません。<br /><br /> 2=SET_NULL: 外部キーを NULL に設定します。|  
|**DELETE_RULE**|**smallint**|SQL 操作が削除の場合に、外部キーに適用されるアクションです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、次の列に対して0、1、または2を返します。<br /><br /> 0 = 外部キーに対して連鎖変更を行います。<br /><br /> 1 = 外部キーが存在する場合、アクションの変更はありません。<br /><br /> 2=SET_NULL: 外部キーを NULL に設定します。|  
|**FK_NAME**|**sysname**|外部キー識別子。 データ ソースに適用されない場合は NULL になります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、FOREIGN KEY 制約の名前を返します。|  
|**PK_NAME**|**sysname**|主キー識別子。 データ ソースに適用されない場合は NULL になります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PRIMARY KEY 制約の名前を返します。|  
|**DEFERRABILITY**|**smallint**|制約チェックを遅延できるかどうかを示します。|  
  
 結果セットでは、FK_NAME 列と PK_NAME 列は常に NULL を返します。  
  
## <a name="remarks"></a>解説  
 **sp_foreignkeys**は、 *table_server*に対応する OLE DB プロバイダーの**IDBSchemaRowset**インターフェイスの FOREIGN_KEYS 行セットを照会します。 返される行を制限するために、 *table_name*、 *table_schema*、 *table_catalog*、および *列* の各パラメーターがこのインターフェイスに渡されます。  
  
## <a name="permissions"></a>アクセス許可  
 スキーマに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、 `Department` リンクサーバー上のデータベース内のテーブルに関する外部キー情報を返し [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] `Seattle1` ます。  
  
```  
EXEC sp_foreignkeys @table_server = N'Seattle1',   
   @pktab_name = N'Department',   
   @pktab_catalog = N'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>参照  
 [sp_catalogs &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_indexes &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_primarykeys &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [sp_tables_ex &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
