---
description: sp_helpfilegroup (Transact-SQL)
title: sp_helpfilegroup (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpfilegroup_TSQL
- sp_helpfilegroup
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpfilegroup
ms.assetid: 619716b5-95dc-4538-82ae-4b90b9da8ebc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 253118a01b4044d752c16e570e16b1f46f21ede2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549621"
---
# <a name="sp_helpfilegroup-transact-sql"></a>sp_helpfilegroup (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベースに関連付けられたファイル グループの名前と属性を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpfilegroup [ [ @filegroupname = ] 'name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @filegroupname = ] 'name'` 現在のデータベース内のファイルグループの論理名を指定します。 *名前* は **sysname**,、既定値は NULL です。 *名前*が指定されていない場合は、現在のデータベース内のすべてのファイルグループが一覧表示され、結果セットセクションに表示される最初の結果セットのみが表示されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**groupname**|**sysname**|ファイルグループの名前。|  
|**groupid**|**smallint**|数値ファイル グループ識別子です。|  
|**filecount**|**int**|ファイルグループ内のファイルの数。|  
  
 *Name*を指定した場合は、ファイルグループ内のファイルごとに1つの行が返されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**file_in_group**|**sysname**|ファイルグループ内のファイルの論理名。|  
|**fileid**|**smallint**|数値ファイル識別子。|  
|**ファイル名**|**nchar (260)**|ディレクトリパスを含むファイルの物理名。|  
|**size**|**nvarchar (15)**|ファイル サイズ (KB 単位) です。|  
|**maxsize**|**nvarchar (15)**|ファイルの最大サイズ。<br /><br /> この値は、ファイルのサイズの上限です。 このフィールドの値が UNLIMITED である場合、ディスクがいっぱいになるまでファイルを拡張できることを示します。|  
|**成長**|**nvarchar (15)**|ファイルの拡張増分値。 これは、新しい領域が必要になるたびにファイルに追加される領域の量を示します。<br /><br /> 0 = ファイルのサイズは固定されており、容量を追加することはできません。|  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-returning-all-filegroups-in-a-database"></a>A. データベース内のすべてのファイルグループを返す  
 次の例は、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースのファイル グループに関する情報を返します。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfilegroup;  
GO  
```  
  
### <a name="b-returning-all-files-in-a-filegroup"></a>B. ファイルグループ内のすべてのファイルを返す  
 次の例は、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースの `PRIMARY` ファイル グループにあるすべてのファイルの情報を返します。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfilegroup 'PRIMARY';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_helpfile &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [master_files &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [データベース ファイルとファイル グループ](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
