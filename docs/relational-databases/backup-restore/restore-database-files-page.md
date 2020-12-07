---
title: '[データベースの復元] ([ファイル] ページ) | Microsoft Docs'
description: SQL Server でデータベースを復元するときに、[データベースの復元] ダイアログ ボックスの [ファイル] ページを使用して、データベース内で復元するように特定のファイルを管理します。
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restoredb.files.f1
- sql13.swb.restoredb.files.f1 in the code
ms.assetid: 714c36ea-a9f9-43a4-99f9-a6f73d1baf8e
author: cawrites
ms.author: chadam
ms.openlocfilehash: d94a143eae321f7ea01f97a54b351d72f8142ad6
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96129153"
---
# <a name="restore-database-files-page"></a>[データベースの復元]\([ファイル] ページ)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **[データベースの復元]** ダイアログ ボックスの **[ファイル]** ページを使用して、データベース内で復元するように選択した特定のファイルを管理します。  
  
## <a name="options"></a>Options  
  
### <a name="restore-database-files-as"></a>[次のデータベース ファイルに復元]  
 復元されたファイルに新しいファイル パスを割り当て、管理できます。  
  
 **[すべてのファイルをフォルダーに移動]**  
 復元されたファイルを再配置します。  
  
|オプション|説明|  
|------------|-----------------|  
|**データ ファイル フォルダー**|復元されたデータ ファイルが移されるデータ ファイルのフォルダー名を入力または検索します。|  
|**ログ ファイル フォルダー**|復元されたログ ファイルが移されるログ ファイル フォルダーを入力または検索します。|  
  
 **[論理ファイル名]**  
 復元するデータベース ファイルごとに 1 つの行が表示されます。  
  
 **[ファイルの種類]**  
 ファイルの種類を表示します。  
  
 **[元のファイル名]**  
 復元されたファイルの元のファイル パスを表示します。  
  
 **[復元先]**  
 復元されたファイルが保存される際のファイル名が表示されます。 適切なファイル名を入力または検索します。  
  
## <a name="see-also"></a>参照  
 [[データベースの復元] &#40;[全般] ページ&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)   
 [[データベースの復元] &#40;[オプション] ページ&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)   
 [RESTORE の引数 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)   
 [テープ ドライブの論理バックアップ デバイスの定義 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
