---
description: sp_clean_db_free_space (Transact-SQL)
title: sp_clean_db_free_space (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_clean_db_free_space_TSQL
- sp_clean_db_free_space
dev_langs:
- TSQL
helpviewer_keywords:
- sp_clean_db_free_space
- ghost records
ms.assetid: faa96f7e-be92-47b1-8bc5-4dbba5331655
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 508ead96133a178e5abbe939defcefa4d6c33492
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546279"
---
# <a name="sp_clean_db_free_space-transact-sql"></a>sp_clean_db_free_space (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ変更ルーチンのためにデータベース ページに残った残存情報を削除します。 sp_clean_db_free_space、データベースのすべてのファイルのすべてのページを消去します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql 
sp_clean_db_free_space   
  [ @dbname = ] 'database_name'   
  [ , [ @cleaning_delay = ] 'delay_in_seconds' ] [;]  
```  
  
## <a name="arguments"></a>引数  
 @dbname = '*database_name*'  
 クリーニングするデータベースの名前です。 *dbname* は **sysname** であり、NULL にすることはできません。  
  
 @cleaning_delay = '*delay_in_seconds*'  
 ページをクリーニングする間隔を指定します。 これにより、i/o システムへの影響が軽減されます。 *delay_in_seconds* は **int** で、既定値は0です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 行の移動を発生させるテーブルまたは更新操作の削除操作では、行への参照を削除することによって、ページ上の領域をすぐに解放できます。 ただし、特定の状況下では、行がゴースト レコードとして、物理的にデータ ページ上に残ってしまう場合があります。 ゴーストレコードは、バックグラウンドプロセスによって定期的に削除されます。 この残存データは、クエリへの応答としてによって返されることはありません [!INCLUDE[ssDE](../../includes/ssde-md.md)] 。 ただし、データまたはバックアップファイルの物理的なセキュリティが危険にさらされている環境では、を使用してこれらのゴーストレコードをクリーニングすることができ `sp_clean_db_free_space` ます。 データベースファイルごとにこの操作を実行するには、 [sp_clean_db_file_free_space (transact-sql)](../../relational-databases/system-stored-procedures/sp-clean-db-file-free-space-transact-sql.md)を使用します。 
  
 sp_clean_db_free_space の実行にかかる時間は、ファイルのサイズ、使用可能な空き領域、および、ディスク容量によって異なります。 を実行すると i/o `sp_clean_db_free_space` アクティビティに大きな影響を与える可能性があるため、通常の操作時間外にこの手順を実行することをお勧めします。  
  
 を実行する前に `sp_clean_db_free_space` 、データベースの完全バックアップを作成することをお勧めします。  
  
 関連する [sp_clean_db_file_free_space](../../relational-databases/system-stored-procedures/sp-clean-db-file-free-space-transact-sql.md) ストアドプロシージャは、1つのファイルをクリーンアップできます。  
  
## <a name="permissions"></a>アクセス許可  
 データベースロールのメンバーシップが必要です `db_owner` 。  
  
## <a name="examples"></a>例  
 次の例では、データベースからすべての残存情報を消去し `AdventureWorks2012` ます。  
  
```sql  
USE master;  
GO  
EXEC sp_clean_db_free_space @dbname = N'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ゴーストクリーンアッププロセスガイド](../ghost-record-cleanup-process-guide.md)    
 [sp_clean_db_file_free_space (Transact-sql)](../../relational-databases/system-stored-procedures/sp-clean-db-file-free-space-transact-sql.md)
  
  
