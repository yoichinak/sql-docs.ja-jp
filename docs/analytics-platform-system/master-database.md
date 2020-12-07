---
title: Master データベース
description: Parallel Data Warehouse の master データベースについて説明します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 7bf3928bfb21d34d0f60e6c52be8dae43621e4bd
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2020
ms.locfileid: "88766741"
---
# <a name="master-database---parallel-data-warehouse"></a>Master データベース-並列データウェアハウス
SQL Server PDW master データベースには、アプライアンスレベルのログイン情報とデータベースカタログが格納されます。 これは、コントロールノードに存在する SQL Server マスターデータベースです。 そのため、master が SQL Server に提供するのと同様の機能を SQL Server PDW に提供します。  
  
システムデータベースの詳細については、「 [システムデータベース](system-databases.md)」を参照してください。  
  
## <a name="limitations-and-restrictions"></a>制限事項と制約事項  
次の一覧では、SQL Server PDW master データベースに対して実行できない操作について説明します。  
  
*次のことはできません。*  
  
-   Master の差分バックアップを実行します。  
  
-   Master にユーザーオブジェクトを作成します。  
  
-   Master の照合順序を変更します。  
  
-   Master の所有者を変更します。  
  
-   マスターを削除または名前変更します。  
  
-   Master に対するアクセス許可を変更します。  
  
-   **DBCC SHRINKLOG**を実行します。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスク|説明|  
|--------|---------------|  
|Master の完全バックアップを作成します。|例:<br /><br />`BACKUP DATABASE master TO backup_directory;`<br /><br />詳細については、「 [BACKUP DATABASE](../t-sql/statements/backup-transact-sql.md?view=aps-pdw-2016)」を参照してください。|  
|master データベースの復元|Master データベースを復元するには、Configuration Manager ツールの [ [Master データベースの復元](restore-the-master-database.md) ] ページを使用します。|  
|データベースカタログ情報を表示します。|`SELECT * FROM master.sys.databases;`|  
|システム全体のログインとアクセス許可の情報を表示します。|`SELECT * FROM master.sys.server_permissions;`<br /><br />`SELECT * FROM master.sys.server_principals;`<br /><br />`SELECT * FROM master.sys.sql_logins;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
