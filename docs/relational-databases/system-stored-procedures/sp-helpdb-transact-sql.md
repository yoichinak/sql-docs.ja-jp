---
description: sp_helpdb (Transact-sql)
title: sp_helpdb (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpdb
- sp_helpdb_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpdb
ms.assetid: 4c3e3302-6cf1-4b2b-8682-004049b578c3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b1b2055f810be69949f72dd97364ccfb47bfa22f
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809166"
---
# <a name="sp_helpdb-transact-sql"></a>sp_helpdb (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定されたデータベースまたはすべてのデータベースに関する情報をレポートします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpdb [ [ @dbname= ] 'name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @dbname = ] 'name'` 情報を報告するデータベースの名前を指定します。 *名前* は **sysname**,、既定値はありません。 *名前*が指定されていない場合は、 **sp_helpdb** 、**データベースカタログビュー**内のすべてのデータベースについてレポートします。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|データベース名。|  
|**db_size**|**nvarchar (13)**|データベースの合計サイズ。|  
|**責任**|**sysname**|**Sa**などのデータベース所有者。|  
|**dbid**|**smallint**|データベース ID。|  
|**created**|**nvarchar(11)**|データベースの作成日です。|  
|**status**|**nvarchar (600)**|データベースで現在設定されているデータベースオプションの値のコンマ区切りの一覧です。<br /><br /> ブール値を持つオプションは、有効になっている場合にのみリストに追加されます。 ブール型以外のオプションは、 *option_name*値の形式で対応する値と共に一覧表示され = *value*ます。<br /><br /> 詳細については、「[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)」を参照してください。|  
|**compatibility_level**|**tinyint**|データベースの互換性レベル (60、65、70、80、および 90) です。|  
  
 *Name*を指定した場合は、指定されたデータベースのファイル割り当てを示す追加の結果セットが存在します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**nchar(128)**|論理ファイル名です。|  
|**fileid**|**smallint**|ファイル ID。|  
|**filename**|**nchar (260)**|オペレーティングシステムのファイル名 (物理ファイル名)。|  
|**グループ**|**nvarchar(128)**|ファイルが属するファイルグループ。<br /><br /> NULL = ファイルはログファイルです。 これは、ファイルグループの一部ではありません。|  
|**size**|**nvarchar (18)**|ファイルサイズ (mb)。|  
|**maxsize**|**nvarchar (18)**|ファイルの最大拡張サイズです。 このフィールドの値が UNLIMITED である場合、ディスクがいっぱいになるまでファイルを拡張できることを示します。|  
|**成長**|**nvarchar (18)**|ファイルの拡張増分値。 これは、新しい領域が必要になるたびにファイルに追加される領域の量を示します。|  
|**ユーセジリンク**|**varchar (9)**|ファイルの使用方法。 データファイルの場合、値は **' data only '** で、ログファイルの値は **' log only '** です。|  
  
## <a name="remarks"></a>注釈  
 結果セットの **status** 列は、データベースで ON に設定されているオプションを報告します。 [ **状態** ] 列には、すべてのデータベースオプションがレポートされません。 現在のデータベースオプションの設定の完全な一覧を表示するに **は、データベースカタログビュー** を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 1つのデータベースを指定する場合は、データベース内の **public** ロールのメンバーシップが必要です。 データベースが指定されていない場合は、 **master**データベースの**public**ロールのメンバーシップが必要です。  
  
 データベースにアクセスできない場合は、エラーメッセージ15622とデータベースに関する情報が **sp_helpdb** 表示されます。  
  
## <a name="examples"></a>例  
  
### <a name="a-returning-information-about-a-single-database"></a>A. 1つのデータベースに関する情報を返す  
 次の例では、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースに関する情報を表示します。  
  
```sql  
EXEC sp_helpdb N'AdventureWorks2012';  
```  
  
### <a name="b-returning-information-about-all-databases"></a>B. すべてのデータベースに関する情報を返す  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行するサーバー上のすべてのデータベースに関する情報を表示します。  
  
```sql  
EXEC sp_helpdb;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.master_files &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
