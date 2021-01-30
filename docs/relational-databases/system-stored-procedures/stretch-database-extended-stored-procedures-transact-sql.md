---
title: 拡張ストアドプロシージャ (Transact-sql)
description: Stretch 対応データベースを操作するときに使用できる拡張ストアドプロシージャについて説明します。 列を調整し、その他のタスクを実行する方法について説明します。
titleSuffix: SQL Server Stretch Database
ms.custom: seo-dt-2019
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- Stretch Database, stored procedures
ms.assetid: bda29952-4b8b-4295-ab78-f24dcb0b03c6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 556e74812ca328a42f1332f20b2576b4cc1b9359
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99178072"
---
# <a name="stretch-database-extended-stored-procedures-transact-sql"></a>Stretch Database の拡張ストアドプロシージャ (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

 ここでは、Stretch Database に関連する拡張ストアドプロシージャについて説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
[sys.sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md) ローカル Stretch 対応データベースとリモート Azure データベース間の認証された接続を削除します。

[sys.sp_rda_get_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md) 復元が必要な場合に、リモートの Azure データベースの完全復元を確実に行うためにステージングテーブルに保持 SQL Server れる、移行されたデータの時間数を取得します。
  
 [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) Stretch が有効なローカルデータベースとリモートデータベースとの間の認証された接続を復元します。
  
 [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)  
 リモート Azure テーブルに格納されているバッチ ID を使用して、最新の移行データに対して、Stretch が有効な SQL Server テーブルに格納されているバッチ ID を調整します。 
 
[sys.sp_rda_reconcile_columns](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-columns-transact-sql.md) リモート Azure テーブルの列を、Stretch が有効な SQL Server テーブルの列に調整します。
 
 [sys.sp_rda_reconcile_indexes](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-indexes-transact-sql.md) リモートテーブルのインデックスを調整するために、スキーマタスクをキューに入れます。
 
 [sys.sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) 現在の Stretch が有効なデータベースとそのテーブルに対するクエリがローカルデータとリモートデータの両方を返すかどうかを指定します (既定)。またはローカルデータのみを返します。
 
 [sys.sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md) 復元が必要な場合に、リモートの Azure データベースの完全な復元を確実に行うために、ステージングテーブルに保持 SQL Server れる移行データの時間数を設定します。
 
 [sys.sp_rda_test_connection](../../relational-databases/system-stored-procedures/sys-sp-rda-test-connection-transact-sql.md) SQL Server からリモート Azure サーバーへの接続をテストし、データ移行を妨げる可能性のある問題を報告します。
 
## <a name="see-also"></a>参照  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
