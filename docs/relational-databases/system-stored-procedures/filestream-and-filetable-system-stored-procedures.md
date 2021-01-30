---
description: Filestream および FileTable システム ストアド プロシージャ (Transact-SQL)
title: Filestream および FileTable システムストアドプロシージャ (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- FileTables [SQL Server], catalog views
ms.assetid: 2c83a4a7-720b-4435-a3b5-788c29f56949
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 41dbdba8212b9896f1a864ff39cf3623eb71c2f3
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99165219"
---
# <a name="filestream-and-filetable-system-stored-procedures-transact-sql"></a>Filestream および FileTable システムストアドプロシージャ (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ここでは、FileTable および Filestream 機能に対するシステムストアドプロシージャについて説明します。  

## <a name="filestream-and-filetable-system-stored-procedures"></a>Filestream および Filetable システムストアドプロシージャ
  [sp_filestream_force_garbage_collection (Transact-SQL)](filestream-and-filetable-sp-filestream-force-garbage-collection.md)

   FILESTREAM ガベージコレクターを強制的に実行し、不要な FILESTREAM ファイルを削除します。

  [sp_kill_filestream_non_transacted_handles (Transact-sql)](filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)

  FileTable データに対する非トランザクション ファイル ハンドルを閉じます。


## <a name="see-also"></a>関連項目
[FileStream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetable](../../relational-databases/blob/filetables-sql-server.md)
<br>[Filestream および FileTable の動的管理ビュー (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Filestream および FileTable のカタログ ビュー (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
  
  
