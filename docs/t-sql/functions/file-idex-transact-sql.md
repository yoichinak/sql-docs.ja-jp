---
description: FILE_IDEX (Transact-SQL)
title: FILE_IDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FILE_IDEX
- FILE_IDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- FILE_IDEX function
- IDs [SQL Server], files
- file IDs [SQL Server]
- names [SQL Server], files
- identification numbers [SQL Server], files
- file names [SQL Server], FILE_IDEX
ms.assetid: 7532fea5-ee5e-4edd-b98b-111a7ba56c8e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3ca433b6e802ce492b0ff464fc300d9f7e569964
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128455"
---
# <a name="file_idex-transact-sql"></a>FILE_IDEX (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

この関数は、指定された現在のデータベースのデータ、ログ、フルテキスト ファイルの論理名に対する、ファイル識別 (ID) 番号を返します。 
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql  
FILE_IDEX ( file_name )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *file_name*  
ファイルの名前に対するファイル ID 値 "FILE_IDEX" を返す、**sysname** 型の式です。 
  
## <a name="return-types"></a>戻り値の型  
**int**  
  
エラー時は **NULL**  
  
## <a name="remarks"></a>注釈  
*file_name* は、[sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) カタログ ビューまたは [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) カタログ ビューの **name** 列に表示される論理ファイル名に対応します。  
  
`FILE_IDEX` は、SELECT リスト、WHERE 句、または式の使用がサポートされるあらゆる場所で使用します。 詳細については、「[式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)」を参照してください。  
  
## <a name="examples"></a>例  
  
### <a name="a-retrieving-the-file-id-of-a-specified-file"></a>A. 指定されたファイルのファイル ID を取得する  
この例では、`AdventureWorks_Data` ファイルのファイル ID が返されます。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT FILE_IDEX('AdventureWorks2012_Data') AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
1  
(1 row(s) affected)  
```  
  
### <a name="b-retrieving-the-file-id-when-the-file-name-is-not-known"></a>B. ファイル名が不明な場合ファイル ID を取得する  
この例では、`AdventureWorks` ログ ファイルのファイル ID が返されます。 Transact-SQL (T-SQL) のコード スニペットで、`sys.database_files` カタログ ビューから論理ファイル名が選択されます (ファイルの種類は `1` (ログ) です)。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT FILE_IDEX((SELECT TOP (1) name FROM sys.database_files WHERE type = 1)) AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
2  
```  
  
### <a name="c-retrieving-the-file-id-of-a-full-text-catalog-file"></a>C. フルテキスト カタログ ファイルのファイル ID を取得する  
この例では、フルテキスト ファイルのファイル ID が返されます。 T-SQL のコード スニペットで、`sys.database_files` カタログ ビューから論理ファイル名が選択されます (ファイルの種類は `4` (フルテキスト) です)。 フルテキスト カタログが存在しない場合、このコードは "NULL" を返します。
  
```sql  
SELECT FILE_IDEX((SELECT name FROM sys.master_files WHERE type = 4))  
AS 'File_ID';  
```  
  
## <a name="see-also"></a>関連項目  
 [メタデータ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
