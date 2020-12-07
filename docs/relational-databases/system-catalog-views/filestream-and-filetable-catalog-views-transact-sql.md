---
description: Filestream および FileTable のカタログ ビュー (Transact-SQL)
title: Filestream および FileTable のカタログビュー (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- FileTables [SQL Server], catalog views
ms.assetid: 2c83a4a7-720b-4435-a3b5-788c29f56949
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fb9a8f2daa440386e48e12ab5a25bcb746a26c97
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545090"
---
# <a name="filestream-and-filetable-catalog-views-transact-sql"></a>Filestream および FileTable のカタログ ビュー (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ここでは、FileTable 機能に関係するカタログ ビューについて説明します。  
  
## <a name="filestream-and-filetable-catalog-views-transact-sql"></a>Filestream および filetable のカタログビュー (Transact-sql)
 [sys.database_filestream_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md)  
 FileTable 内の有効化された FILESTREAM データに対する非トランザクション アクセスのレベルに関する情報を表示します。 SQL Server インスタンス内のデータベースごとに1行のデータを格納します。  
  
 [sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md)  
 Filetable に関連するシステム定義のオブジェクトの一覧を表示します。 システム定義オブジェクトごとに1行のレコードを格納します。  
  
 [sys.filetables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetables-transact-sql.md)  
 FileTable ごとに1行の値を返します。 は、 **sys. tables**から継承します。  

## <a name="see-also"></a>参照
[FileStream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetable](../../relational-databases/blob/filetables-sql-server.md)
<br>[Filestream および FileTable の動的管理ビュー (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Filestream および FileTable システム ストアド プロシージャ (Transact-SQL)](../system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)
  
  
