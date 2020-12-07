---
description: sp_kill_filestream_non_transacted_handles (Transact-sql)
title: sp_kill_filestream_non_transacted_handles (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_kill_filestream_non_transacted_handles_TSQL
- sp_kill_filestream_non_transacted_handles
dev_langs:
- TSQL
helpviewer_keywords:
- sp_kill_filestream_non_transacted_handles
ms.assetid: 7188353e-ab29-49a0-8f25-7fb8ab122589
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ba045dc68e5e032478d26caaa7790ed357f4e087
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550090"
---
# <a name="sp_kill_filestream_non_transacted_handles-transact-sql"></a>sp_kill_filestream_non_transacted_handles (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  FileTable データに対する非トランザクション ファイル ハンドルを閉じます。  
  
## <a name="syntax"></a>構文  
  
```sql  
sp_kill_filestream_non_transacted_handles [[ @table_name = ] 'table_name', [[ @handle_id = ] @handle_id]]  
```  
  
## <a name="arguments"></a>引数  
 *table_name*  
 非トランザクションハンドルを閉じるテーブルの名前。  
  
 *Handle_id*を指定せずに*table_name*を渡して、FileTable のすべての開いている非トランザクションハンドルを閉じることができます。  
  
 *Table_name*の値に NULL を渡すと、現在のデータベース内のすべての filetable に対して開いているすべての非トランザクションハンドルを閉じることができます。 既定値は NULL です。  
  
 *handle_id*  
 閉じる個々のハンドルのオプションの ID です。 *Handle_id*は、 [dm_filestream_non_transacted_handles &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)動的管理ビューから取得できます。 各 ID は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内で一意です。 *Handle_id*を指定する場合は、 *table_name*の値も指定する必要があります。  
  
 *Handle_id*の値に NULL を渡すと、 *table_name*によって指定された FileTable のすべての開いている非トランザクションハンドルを閉じることができます。 既定値は NULL です。  
  
## <a name="return-code-value"></a>リターン コード値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-set"></a>結果セット  
 なし。  
  
## <a name="general-remarks"></a>全般的な解説  
 **Sp_kill_filestream_non_transacted_handles**に必要な*handle_id*は、他の**kill**コマンドで使用されている session_id または作業単位とは関係がありません。  
  
 詳細については、「 [FileTable の管理](../../relational-databases/blob/manage-filetables.md)」を参照してください。  
  
## <a name="metadata"></a>Metadata  
 開いている非トランザクションファイルハンドルの詳細については、動的管理ビューの [dm_filestream_non_transacted_handles &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)を参照してください。  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 **Dm_FILESTREAM_non_transacted_handles**動的管理ビューからファイルハンドルを取得し、 **sp_kill_filestream_non_transacted_handles**を実行するには、 **VIEW DATABASE STATE**権限が必要です。  
  
## <a name="examples"></a>例  
 次の例は、 **sp_kill_filestream_non_transacted_handles** を呼び出して、FileTable データの非トランザクションファイルハンドルを閉じる方法を示しています。  
  
```sql  
-- Close all open handles in the current database.  
sp_kill_filestream_non_transacted_handles  
  
-- Close all open handles in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = 'myFileTable'  
  
-- Close a specific handle in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = 'myFileTable', @handle_id = 0xFFFAAADD  
```  
  
 次の例では、スクリプトを使用して *handle_id* を取得し、それを閉じる方法を示します。  
  
```sql  
DECLARE @handle_id varbinary(16);  
DECLARE @table_name sysname;  
  
SELECT TOP 1 @handle_id = handle_id, @table_name = Object_name(table_id)  
FROM sys.dm_FILESTREAM_non_transacted_handles;  
  
EXEC sp_kill_filestream_non_transacted_handles @dbname, @table_name, @handle_id;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [FileTable の管理](../../relational-databases/blob/manage-filetables.md)  
 [Filestream および FileTable の動的管理ビュー (Transact-sql)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
 <br>[Filestream および FileTable のカタログビュー (Transact-sql)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
 <br>[sp_filestream_force_garbage_collection (Transact-SQL)](filestream-and-filetable-sp-filestream-force-garbage-collection.md)
  
