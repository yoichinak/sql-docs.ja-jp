---
description: sp_helpmergearticleconflicts (Transact-SQL)
title: sp_helpmergearticleconflicts (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergearticleconflicts
- sp_helpmergearticleconflicts_TSQL
helpviewer_keywords:
- sp_helpmergearticleconflicts
ms.assetid: 4678a2b9-9a5f-4193-a20d-2e11fc896c3a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 49ca95bebb40c13bf2044bef58e161bb2bacfdd2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535188"
---
# <a name="sp_helpmergearticleconflicts-transact-sql"></a>sp_helpmergearticleconflicts (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  競合しているパブリケーション内のアーティクルを返します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。または、サブスクライバー側でマージ サブスクリプション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpmergearticleconflicts [ [ @publication = ] 'publication' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publsher_db' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` マージパブリケーションの名前を指定します。*publication* のデータ型は **sysname**で、既定値はです **%** 。これにより、データベース内の競合しているすべてのアーティクルが返されます。  
  
`[ @publisher = ] 'publisher'` パブリッシャーの名前を指定します。*publisher* は **sysname**で、既定値は NULL です。  
  
`[ @publisher_db = ] 'publisher_db'` パブリッシャーデータベースの名前を指定します。*publisher_db* は **sysname**,、既定値は NULL です。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**記事**|**sysname**|アーティクルの名前。|  
|**source_owner**|**sysname**|ソース オブジェクトの所有者です。|  
|**source_object**|**nvarchar (386)**|ソース オブジェクトの名前です。|  
|**conflict_table**|**nvarchar(258)**|挿入または更新の競合を格納するテーブルの名前。|  
|**guidcolname**|**sysname**|ソースオブジェクトの RowGuidCol の名前。|  
|**centralized_conflicts**|**int**|指定されたパブリッシャーに競合レコードが格納されているかどうか。|  
  
 アーティクルに削除の競合のみがあり **conflict_table** 行がない場合、結果セットの **conflict_table** の名前は NULL になります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_helpmergearticleconflicts** は、マージレプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_helpmergearticleconflicts**を実行できるのは、 **sysadmin**固定サーバーロールおよび**db_owner**固定データベースロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
