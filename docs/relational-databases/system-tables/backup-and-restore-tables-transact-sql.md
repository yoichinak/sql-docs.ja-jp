---
description: テーブルのバックアップと復元 (Transact-sql)
title: テーブルのバックアップと復元 (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system tables [SQL Server], backup tables
- backup system tables [SQL Server]
- system tables [SQL Server], restore tables
- restore system tables [SQL Server]
ms.assetid: aa615add-54e6-40f5-8b55-3728b26884ee
author: markingmyname
ms.author: maghan
ms.openlocfilehash: abb69d6cefa270330a41d90bea0352981dd7ee8a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540982"
---
# <a name="backup-and-restore-tables-transact-sql"></a>テーブルのバックアップと復元 (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  このセクションのトピックでは、データベースのバックアップ操作と復元操作で使用される情報を格納するシステムテーブルについて説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md)  
 データベースの各データまたは各ログ ファイルに対して 1 行のデータを格納します。  
  
 [backupfilegroup](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)  
 バックアップ時に、データベース内のファイルグループごとに1行のデータを格納します。  
  
 [backupmediafamily](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)  
 メディア ファミリごとに 1 行のデータを格納します。  
  
 [backupmediaset](../../relational-databases/system-tables/backupmediaset-transact-sql.md)  
 バックアップ メディア セットごとに 1 行のデータを格納します。  
  
 [backupset](../../relational-databases/system-tables/backupset-transact-sql.md)  
 バックアップ セットごとに 1 行のデータを格納します。  
  
 [logmarkhistory](../../relational-databases/system-tables/logmarkhistory-transact-sql.md)  
 予約されているマークされたトランザクションごとに1行のレコードを格納します。  
  
 [restorefile](../../relational-databases/system-tables/restorefile-transact-sql.md)  
 復元されたファイルごとに 1 行のデータを格納します。 これには、ファイルグループ名によって間接的に復元されるファイルが含まれます。  
  
 [restorefilegroup](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)  
 復元されたファイル グループごとに 1 行のデータを格納します。  
  
 [restorehistory](../../relational-databases/system-tables/restorehistory-transact-sql.md)  
 復元操作ごとに 1 行のデータを格納します。  
  
 [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md)  
 824エラーで失敗したページごとに1行の行が含まれています (上限は1000行)。  
  
 [sysopentapes](../../relational-databases/system-tables/sysopentapes-transact-sql.md)  
 現在開いているテープ デバイスごとに 1 行のデータを格納します。  
  
  
