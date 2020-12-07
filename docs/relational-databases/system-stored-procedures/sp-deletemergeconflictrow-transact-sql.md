---
description: sp_deletemergeconflictrow (Transact-sql)
title: sp_deletemergeconflictrow (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_deletemergeconflictrow
- sp_deletemergeconflictrow_TSQL
helpviewer_keywords:
- sp_deletemergeconflictrow
ms.assetid: 64cf1186-28b8-4cd9-88f1-a7808a9c8d60
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4b2fae5fad15490fee5c239a26e8e0b5e0a25832
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543537"
---
# <a name="sp_deletemergeconflictrow-transact-sql"></a>sp_deletemergeconflictrow (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  競合テーブルまたは [MSmerge_conflicts_info &#40;transact-sql&#41;](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md) テーブルから行を削除します。 このストアド プロシージャは、競合テーブルが格納されているコンピューターの、任意のデータベース上で実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_deletemergeconflictrow [ [ @conflict_table = ] 'conflict_table' ]  
    [ , [ @source_object = ] 'source_object' ]  
    { , [ @rowguid = ] 'rowguid'  
        , [ @origin_datasource = ] 'origin_datasource' ] }  
    [ , [ @drop_table_if_empty = ] 'drop_table_if_empty' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @conflict_table = ] 'conflict_table'` 競合テーブルの名前を指定します。 *conflict_table* は **sysname**で、既定値は **%** です。 *Conflict_table*が NULL またはとして指定されている場合、 **%** 競合は削除競合であると見なされ、 *rowguid*と*origin_datasource*と*Source_object*に一致する行が[MSmerge_conflicts_info &#40;transact-sql&#41;](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md)テーブルから削除されます。  
  
`[ @source_object = ] 'source_object'` ソーステーブルの名前を指定します。 *source_object* は **nvarchar (386)**,、既定値は NULL です。  
  
`[ @rowguid = ] 'rowguid'` 削除競合の行識別子を示します。 *rowguid* は **uniqueidentifier**,、既定値はありません。  
  
`[ @origin_datasource = ] 'origin_datasource'` 競合の発生元を示します。 *origin_datasource* は **varchar (255)**,、既定値はありません。  
  
`[ @drop_table_if_empty = ] 'drop_table_if_empty'` が空の場合に *conflict_table* を削除することを示すフラグです。 *drop_table_if_empty* は **varchar (10)**,、既定値は FALSE です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_deletemergeconflictrow** は、マージレプリケーションで使用します。  
  
 [MSmerge_conflicts_info &#40;transact-sql&#41;](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md) テーブルはシステムテーブルであり、空の場合でも、データベースからは削除されません。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_deletemergeconflictrow**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
