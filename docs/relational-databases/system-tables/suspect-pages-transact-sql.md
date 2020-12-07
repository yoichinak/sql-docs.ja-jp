---
description: suspect_pages (Transact-SQL)
title: suspect_pages (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- suspect_page_table
- suspect_page_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- suspect_pages system table
- suspect pages [SQL Server]
ms.assetid: 119c8d62-eea8-44fb-bf72-de469c838c50
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0c601496075c71d70af89b0413e5bcbf3a6ba8b2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544483"
---
# <a name="suspect_pages-transact-sql"></a>suspect_pages (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  マイナー823エラーまたは824エラーによって失敗したページごとに1行の値を格納します。 ページは問題の疑いがあると考えられるので、この表に記載されていますが、実際には問題ありません。 問題のあるページが修復されると、[ **event_type** ] 列の状態が更新されます。  
  
 次の表では、1000行の制限があり、 **msdb** データベースに格納されています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|このページが適用されるデータベースの ID。|  
|**file_id**|**int**|データベース内のファイルの ID。|  
|**page_id**|**bigint**|問題があると考えられるページの ID。 すべてのページには、データベース内のページの場所を識別する32ビット値であるページ ID があります。 **Page_id**は、8 KB ページのデータファイル内のオフセットです。 各ページ ID はファイル内で一意です。|  
|**event_type**|**int**|エラーの種類です。次のいずれか:<br /><br /> 1 = 問題があると考えられるページ (ディスク エラーなど) の原因となった 823 エラー、または、不正なチェックサムまたは破損ページ (不適切なページ ID) 以外の 824 エラー。<br /><br /> 2 = 不適切なチェックサムです。<br /><br /> 3 = 破損ページ。<br /><br /> 4 = 復元済み (ページは不適切とマークされた後に復元されました)。<br /><br /> 5 = 修復済み (DBCC によってページが修復されました)。<br /><br /> 7 = DBCC により割り当て解除。|  
|**error_count**|**int**|エラーが発生した回数。|  
|**last_update_date**|**datetime**|最後に更新された日付と時刻のタイムスタンプ。|  
  
## <a name="permissions"></a>アクセス許可  
 **msdb** に対するアクセスを持つユーザー は、 **suspect_pages** テーブルのデータを読み取ることができます。 suspect_pages テーブルに対する UPDATE 権限を持つすべてのユーザーは、そのレコードを更新できます。 **msdb** の **db_owner** 固定データベース ロールのメンバーまたは **sysadmin** 固定サーバー ロールのメンバーは、レコードの挿入、更新、および削除を行うことができます。  
  
## <a name="see-also"></a>参照  
 [ページ復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [Database Suspect Data Page イベントクラス](../../relational-databases/event-classes/database-suspect-data-page-event-class.md)   
 [システムテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)   
 [suspect_pages テーブルの管理 &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
