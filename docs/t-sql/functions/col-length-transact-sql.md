---
description: COL_LENGTH (Transact-SQL)
title: COL_LENGTH (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COL_LENGTH
- COL_LENGTH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- lengths [SQL Server], columns
- COL_LENGTH function
- column properties [SQL Server]
- column length [SQL Server]
ms.assetid: cf891206-c49f-40eb-858e-eefd2b638a33
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 862e7aa70a3d26f5555c5f809d5fb24137de1a40
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128546"
---
# <a name="col_length-transact-sql"></a>COL_LENGTH (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

この関数は、定義されている列の長さをバイト単位で返します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```syntaxsql
COL_LENGTH ( 'table' , 'column' )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
**'** *table* **'**  
列の長さ情報を定義するテーブルの名前。 *テーブル* 型の式は、 **nvarchar** です。
  
**'** *column* **'**  
長さを定義する列名。 *列* 型の式は、 **nvarchar** です。
  
## <a name="return-type"></a>の戻り値の型 :
**smallint**
  
## <a name="exceptions"></a>例外  
エラーが発生した場合、または呼び出し元にオブジェクトを表示するための適切な権限がない場合は、NULL が返されます。
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、そのユーザーが所有している、または権限を与えられている、セキュリティ保護可能なアイテムのメタデータのみを表示できます。 つまり、オブジェクトに対する適切な権限がユーザーに与えられていない場合、メタデータを生成する組み込み関数 (COL_LENGTH など) が NULL を返す可能性があります。 詳細については、「[メタデータ表示の構成](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。
  
## <a name="remarks"></a>解説  
**max** 指定子 (**varchar (max)**) で宣言された **varchar** 列の場合、COL_LENGTH では値 -1 が返されます。
  
## <a name="examples"></a>例  
この例では、`varchar(40)` 型と `nvarchar(40)` 型の列の値を返します。
  
```sql
USE AdventureWorks2012;  
GO  
CREATE TABLE t1(c1 VARCHAR(40), c2 NVARCHAR(40) );  
GO  
SELECT COL_LENGTH('t1','c1')AS 'VarChar',  
      COL_LENGTH('t1','c2')AS 'NVarChar';  
GO  
DROP TABLE t1;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
VarChar     NVarChar  
40          80  
```  
  
## <a name="see-also"></a>関連項目
[式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[メタデータ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[COL_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/col-name-transact-sql.md)  
[COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)
  
  
