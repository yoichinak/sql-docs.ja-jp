---
description: FILEPROPERTY (Transact-SQL)
title: FILEPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FILEPROPERTY_TSQL
- FILEPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- viewing file properties
- names [SQL Server], files
- displaying file properties
- file properties [SQL Server]
- FILEPROPERTY function
- file names [SQL Server], FILEPROPERTY
ms.assetid: b82244ed-d623-431f-aa06-8017349d847f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 524fe8130742a58da0c806c8ad35c9287c732017
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124714"
---
# <a name="fileproperty-transact-sql"></a>FILEPROPERTY (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベース内のファイル名とプロパティ名を指定したときに、指定されたファイル名のプロパティ値を返します。 現在のデータベース内にないファイルの場合は NULL を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
FILEPROPERTY ( file_name , property )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *file_name*  
 プロパティ情報を返す基になる、現在のデータベースに関連付けられたファイルの名前を含む式を指定します。 *file_name* は **nchar (128)** です。  
  
 *property*  
 返されるファイル プロパティの名前を含む式を指定します。 *プロパティ* は **varchar (128)**, 、値は次のいずれかを指定することができます。  
  
|値|説明|返される値|  
|-----------|-----------------|--------------------|  
|**IsReadOnly**|ファイル グループが読み取り専用であるかどうかを示します。|1 = True<br /><br /> 0 = False<br /><br /> NULL = 入力は無効です。|  
|**IsPrimaryFile**|ファイルはプライマリ ファイルです。|1 = True<br /><br /> 0 = False<br /><br /> NULL = 入力は無効です。|  
|**IsLogFile**|ファイルはログ ファイルです。|1 = True<br /><br /> 0 = False<br /><br /> NULL = 入力は無効です。|  
|**SpaceUsed**|指定されたファイルで使用されている領域のサイズ。|ファイルに割り当てられているページ数|  
  
## <a name="return-types"></a>戻り値の型  
 **int**  
  
## <a name="remarks"></a>解説  
 *file_name* に対応する、 **名前** 内の列、 **sys.master_files** または **sys.database_files** カタログ ビューです。  
  
## <a name="examples"></a>例  
 次の例では、`IsPrimaryFile` データベース内のファイル名 `AdventureWorks_Data` の [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] プロパティに対する設定を返します。  
  
```sql
SELECT FILEPROPERTY('AdventureWorks2012_Data', 'IsPrimaryFile')AS [Primary File];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Primary File   
-------------  
1  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>関連項目  
 [FILEGROUPPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/filegroupproperty-transact-sql.md)   
 [メタデータ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
