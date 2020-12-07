---
description: sp_create_removable (Transact-SQL)
title: sp_create_removable (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_create_removable
- sp_create_removable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_create_removable
ms.assetid: 06e36ae5-f70d-4a26-9a7f-ee4b9360b355
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8e76256ec08495383d989134c101b54e4a510370
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753960"
---
# <a name="sp_create_removable-transact-sql"></a>sp_create_removable (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  リムーバブル メディア データベースを作成します。 3 つ以上のファイル (システム カタログ テーブルとトランザクション ログに 1 つずつ、データ テーブルに 1 つ以上) を作成し、それらのファイルにデータベースを格納します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md) を使用することをお勧めします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_create_removable   
   [ @dbname = ] 'dbname',   
   [ @syslogical= ] 'syslogical',   
   [ @sysphysical = ] 'sysphysical',   
   [ @syssize = ] syssize,   
   [ @loglogical = ] 'loglogical',   
   [ @logphysical = ] 'logphysical',   
   [ @logsize = ] logsize,   
   [ @datalogical1 = ] 'datalogical1',   
   [ @dataphysical1 = ] 'dataphysical1',   
   [ @datasize1 = ] datasize1 ,   
   [ @datalogical16 = ] 'datalogical16',   
   [ @dataphysical16 = ] 'dataphysical16',   
   [ @datasize16 = ] datasize16 ]  
```  
  
## <a name="arguments"></a>引数  
`[ @dbname = ] 'dbname'` リムーバブルメディアで使用するために作成するデータベースの名前を指定します。 *dbname* は **sysname**です。  
  
`[ @syslogical = ] 'syslogical'` システムカタログテーブルを格納するファイルの論理名を指定します。 *syslogical* は **sysname**です。  
  
`[ @sysphysical = ] 'sysphysical'` 物理名を指定します。 システム カタログ テーブルを格納するファイルの名前をフル パスと共に指定します。 *sysphysical* は **nvarchar (260)** です。  
  
`[ @syssize = ] syssize` システムカタログテーブルを保持するファイルのサイズを mb 単位で示します。 *syssize* は **int**です。 *Syssize* の最小値は1です。  
  
`[ @loglogical = ] 'loglogical'` トランザクションログを格納するファイルの論理名を指定します。 *loglogical* は **sysname**です。  
  
`[ @logphysical = ] 'logphysical'` 物理名を指定します。 これには、トランザクションログを含むファイルの完全修飾パスが含まれます。 *logphysical* は **nvarchar (260)** です。  
  
`[ @logsize = ] logsize` トランザクションログを格納するファイルのサイズを mb 単位で示します。 *logsize* は **int**です。最小 *logsize* は1です。  
  
`[ @datalogical1 = ] 'datalogical'` データテーブルを格納するファイルの論理名を指定します。 *datalogical* は **sysname**です。  
  
 データファイルは 1 ~ 16 である必要があります。 データベースが大きくなり複数のディスクに分散する必要が生じた場合に備えて、通常、複数のデータ ファイルを作成します。  
  
`[ @dataphysical1 = ] 'dataphysical'` 物理名を指定します。 データ テーブルを格納するファイルの名前をフル パスと共に指定します。 *dataphysical* は **nvarchar (260)** です。  
  
`[ @datasize1 = ] 'datasize'` データテーブルを格納するファイルのサイズを mb 単位で示します。 *datasize* は **int**です。最小 *datasize* は1です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 データベースのコピーをコンパクト ディスクなどのリムーバブル メディアに作成し、他のユーザーにデータベースを配布する場合は、このストアド プロシージャを使用します。  
  
## <a name="permissions"></a>アクセス許可  
 CREATE DATABASE、CREATE ANY DATABASE、または ALTER ANY DATABASE の各権限が必要です。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス上のディスク使用量を管理するため、通常、データベースを作成する権限をいくつかのログイン アカウントに制限します。  
  
### <a name="permissions-on-data-and-log-files"></a>データおよびログ ファイルに対する権限  
 特定の操作がデータベースに対して実行されるたびに、対応する権限がそのデータファイルとログファイルに設定されます。 この権限は、開く権限のあるディレクトリにファイルが存在する場合に、そのファイルが誤って書き換えられるのを防ぎます。  
  
|データベースに対する操作|ファイルに対して設定される権限|  
|---------------------------|------------------------------|  
|変更して新しいファイルを追加|作成済み|  
|バックアップ|アタッチ|  
|復元|デタッチ|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、データ ファイルとログ ファイルの権限は設定されません。  
  
## <a name="examples"></a>例  
 次の例では、データベースを `inventory` リムーバブルデータベースとして作成します。  
  
```  
EXEC sp_create_removable 'inventory',   
   'invsys',  
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\invsys.mdf'  
, 2,   
   'invlog',  
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\invlog.ldf', 4,  
   'invdata',  
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\invdata.ndf',   
10;  
```  
  
## <a name="see-also"></a>参照  
 [データベースのデタッチとアタッチ &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_certify_removable &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-certify-removable-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_dbremove &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dbremove-transact-sql.md)   
 [sp_detach_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [sp_helpfile &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sp_helpfilegroup &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
