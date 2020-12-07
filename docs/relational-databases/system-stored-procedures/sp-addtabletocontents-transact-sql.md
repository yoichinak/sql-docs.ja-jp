---
description: sp_addtabletocontents (Transact-sql)
title: sp_addtabletocontents (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addtabletocontents_TSQL
- sp_addtabletocontents
helpviewer_keywords:
- sp_addtabletocontents
ms.assetid: 2ea27001-74f4-463e-bf1b-b6b5a86b9219
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 26b1946d03fe949bd0a2af52ce07d64198dd1bbf
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548350"
---
# <a name="sp_addtabletocontents-transact-sql"></a>sp_addtabletocontents (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在追跡テーブルに含まれていないソース テーブル内の行への参照をマージ追跡テーブルに挿入します。 **Bcp**を使用して大量のデータを一括で読み込む場合は、このオプションを使用します。これにより、マージ追跡トリガーは起動されません。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addtabletocontents [ @table_name = ] 'table_name'  
    [ , [ @owner_name = ] 'owner_name' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @table_name = ] 'table_name'` テーブルの名前を指定します。 *table_name* は **sysname**であり、既定値はありません。  
  
`[ @owner_name = ] 'owner_name'` テーブルの所有者の名前を指定します。 *owner_name* は **sysname**,、既定値は NULL です。  
  
`[ @filter_clause = ] 'filter_clause'` 新しく読み込まれたデータのどの行をマージ追跡テーブルに追加するかを制御するフィルター句を指定します。 *filter_clause* は **nvarchar (4000)**,、既定値は NULL です。 *Filter_clause*が**null**の場合は、一括読み込みされたすべての行が追加されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_addtabletocontents** は、マージレプリケーションでのみ使用されます。  
  
 *Table_name*内の行は**rowguidcol**によって参照され、その参照がマージ追跡テーブルに追加されます。 **sp_addtabletocontents** は、マージレプリケーションを使用してパブリッシュされたテーブルにデータを一括コピーした後に使用する必要があります。 このストアド プロシージャは、コピーされた行のトラッキングを実行し、次の同期処理の際に新しい行を確実に挿入します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_addtabletocontents**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
