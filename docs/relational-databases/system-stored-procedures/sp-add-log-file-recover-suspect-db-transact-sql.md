---
description: sp_add_log_file_recover_suspect_db (Transact-SQL)
title: sp_add_log_file_recover_suspect_db (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_log_file_recover_suspect_db_TSQL
- sp_add_log_file_recover_suspect_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_file_recover_suspect_db
ms.assetid: b41ca3a5-7222-4c22-a012-e66a577a82f6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b67ebd25d3418392e4a6aa7986e3305ee6eae0ba
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474597"
---
# <a name="sp_add_log_file_recover_suspect_db-transact-sql"></a>sp_add_log_file_recover_suspect_db (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ログ領域が不足しているため (エラー 9002)、データベースで復旧を完了できない場合に、ログファイルをファイルグループに追加します。 ファイルが追加されると、 **sp_add_log_file_recover_suspect_db** 問題のある設定がオフになり、データベースの復旧が完了します。 パラメーターは、ALTER DATABASE の *DATABASE_NAME* ログファイルの追加と同じです。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_add_log_file_recover_suspect_db [ @dbName= ] 'database' ,   
    [ @name = ] 'logical_file_name' ,   
    [ @filename= ] 'os_file_name' ,   
    [ @size = ] 'size' ,   
    [ @maxsize = ] 'max_size' ,   
    [ @filegrowth = ] 'growth_increment'  
```  
  
## <a name="arguments"></a>引数  
`[ @dbName = ] 'database'` データベースの名前を指定します。 *データベースのデータ* 型は **sysname**で、既定値はありません。  
  
`[ @name = ] 'logical_file_name'` ファイルを参照するときにで使用される名前を指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 サーバー内で一意な名前を指定する必要があります。 *logical_file_name* は **nvarchar (260)**,、既定値はありません。  
  
`[ @filename = ] 'os_file_name'` は、ファイルのオペレーティングシステムによって使用されるパスとファイル名です。 ファイルは、がインストールされているサーバーに存在している必要があり [!INCLUDE[ssDE](../../includes/ssde-md.md)] ます。 *os_file_name* は **nvarchar (260)**,、既定値はありません。  
  
`[ @size = ] 'size_ '` ファイルの初期サイズです。 *サイズ* は **nvarchar (20)**,、既定値は NULL です。 整数を指定します。小数を含めないでください。 サフィックス MB、KB を使用してメガバイト、キロバイトを指定できます。 既定値は MB です。 最小値は 512 KB です。 *Size*が指定されていない場合の既定値は 1 MB です。  
  
`[ @maxsize = ] 'max_size_ '` ファイルの拡張可能な最大サイズを指定します。 *max_size* は **nvarchar (20)**,、既定値は NULL です。 整数を指定します。小数を含めないでください。 サフィックス MB、KB を使用してメガバイト、キロバイトを指定できます。 既定値は MB です。  
  
 *Max_size*が指定されていない場合、ファイルはディスクがいっぱいになるまで拡張されます。 ディスク容量の上限まで近づくと、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アプリケーション ログが管理者に対して警告を発します。  
  
`[ @filegrowth = ] 'growth_increment_ '` 新しい領域が必要になるたびにファイルに追加される領域のサイズです。 *growth_increment* は **nvarchar (20)**,、既定値は NULL です。 値0は、増加していないことを示します。 整数を指定します。小数を含めないでください。 値は MB、KB、またはパーセント (%) の単位で指定できます。 % が指定されている場合、増加率は、増分が発生した時点でのファイルのサイズに対して指定された割合になります。 サフィックス MB、KB、または % を付けないで数値を指定した場合の既定値は MB です。  
  
 *Growth_increment*が NULL の場合、既定値は10% で、最小サイズの値は 64 KB です。 指定されたサイズは、最も近い 64 KB 単位の値に切り上げられます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 実行権限は、既定では **sysadmin** 固定サーバーロールのメンバーに与えています。 これらのアクセス許可は転送できません。  
  
## <a name="examples"></a>例  
 次の例では、 `db1` ログ領域が不足しているため、復旧中にデータベースが問題ありとマークされています (エラー 9002)。  
  
```  
USE master;  
GO  
EXEC sp_add_log_file_recover_suspect_db db1, logfile2,  
'C:\Program Files\Microsoft SQL  
    Server\MSSQL13.MSSQLSERVER\MSSQL\Data\db1_logfile2.ldf',   
    '1MB';  
```  
  
## <a name="see-also"></a>参照  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_add_data_file_recover_suspect_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-data-file-recover-suspect-db-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
