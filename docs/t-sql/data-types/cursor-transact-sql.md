---
description: cursor (Transact-SQL)
title: cursor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- cursor data type
ms.assetid: fbea16ef-f2cc-4734-9149-ec2598fd3cca
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 858a6200e1e1d74f5610d61e85a2b5dde3248e61
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99205483"
---
# <a name="cursor-transact-sql"></a>cursor (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

カーソルへの参照を含む、変数またはストアド プロシージャの OUTPUT パラメーターのデータ型。
  
## <a name="remarks"></a>注釈  
**cursor** 型の変数とパラメーターを参照できる操作は次のとおりです。
-   DECLARE *\@local_variable* ステートメントと SET *\@local_variable* ステートメント。  
-   OPEN、FETCH、CLOSE、DEALLOCATE cursor ステートメント。  
-   ストアド プロシージャの出力パラメーター。  
-   CURSOR_STATUS 関数。  
-   **sp_cursor_list**、**sp_describe_cursor**、**sp_describe_cursor_tables**、および **sp_describe_cursor_columns** の各システム ストアド プロシージャ  
  
**sp_cursor_list** および **sp_describe_cursor** の **cursor_name** 出力列に、カーソル変数の名前が返されます。
  
作成された任意の変数、 **カーソル** データ型は null を許容します。
  
**カーソル** CREATE TABLE ステートメント内の列のデータ型を使用することはできません。
  
## <a name="see-also"></a>関連項目
[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CURSOR_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-status-transact-sql.md)  
[データ型の変換&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  
