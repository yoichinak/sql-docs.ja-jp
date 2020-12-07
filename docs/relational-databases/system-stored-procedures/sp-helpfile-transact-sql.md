---
description: sp_helpfile (Transact-sql)
title: sp_helpfile (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpfile
- sp_helpfile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpfile
ms.assetid: 1546e0ae-5a99-4e01-9eb9-d147fa65884c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7bb8c6ff5fe18393db1c08bae888d1479a7f2594
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549654"
---
# <a name="sp_helpfile-transact-sql"></a>sp_helpfile (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベースに関連付けられたファイルの物理名と属性を返します。 このストアドプロシージャを使用して、サーバーにアタッチまたはデタッチするファイルの名前を決定します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpfile [ [ @filename= ] 'name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @filename = ] 'name'` 現在のデータベース内のすべてのファイルの論理名を指定します。 *名前* は **sysname**,、既定値は NULL です。 場合 *名前* が指定されていない、現在のデータベース内のすべてのファイルの属性が返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|論理ファイル名です。|  
|**fileid**|**smallint**|ファイルの数値識別子。 *Name*が指定されている場合、は返されません *。*|  
|**ファイル名**|**nchar (260)**|物理ファイル名。|  
|**グループ**|**sysname**|ファイルが属するファイルグループ。<br /><br /> NULL = ファイルはログファイルです。 これは、ファイルグループの一部ではありません。|  
|**size**|**nvarchar (15)**|ファイル サイズ (KB 単位) です。|  
|**maxsize**|**nvarchar (15)**|ファイルの最大拡張サイズです。 このフィールドの値が UNLIMITED である場合、ディスクがいっぱいになるまでファイルを拡張できることを示します。|  
|**成長**|**nvarchar (15)**|ファイルの拡張増分値。 これは、新しい領域が必要になるたびにファイルに追加される領域の量を示します。<br /><br /> 0 = ファイルのサイズは固定されており、容量を追加することはできません。|  
|**ユーセジリンク**|**varchar (9)**|データファイルの場合、値は **' data only '** で、ログファイルの値は **' log only '** です。|  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、内のファイルに関する情報を返し [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ます。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfile;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_helpfilegroup &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [master_files &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [データベース ファイルとファイル グループ](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
