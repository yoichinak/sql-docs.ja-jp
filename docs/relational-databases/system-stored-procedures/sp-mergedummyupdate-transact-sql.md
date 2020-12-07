---
description: sp_mergedummyupdate (Transact-sql)
title: sp_mergedummyupdate (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergedummyupdate_TSQL
- sp_mergedummyupdate
helpviewer_keywords:
- sp_mergedummyupdate
ms.assetid: b834f7f6-9588-4d59-a3e2-83d8e8e722e1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 39558295ad31cfccd1f4df70e89580e2615fea56
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545972"
---
# <a name="sp_mergedummyupdate-transact-sql"></a>sp_mergedummyupdate (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定した行でダミーを更新し、その更新が次のマージで再送されるようにします。 このストアドプロシージャは、パブリッシャー、パブリケーションデータベース、またはサブスクライバー側でサブスクリプションデータベースに対して実行できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_mergedummyupdate [ @source_object =] 'source_object', [ @rowguid =] 'rowguid'  
```  
  
## <a name="arguments"></a>引数  
`[ @source_object = ] 'source_object'` ソースオブジェクトの名前を指定します。 *source_object*は **nvarchar (386)**,、既定値はありません。  
  
`[ @rowguid = ] 'rowguid'` 行識別子を示します。 *rowguid* は **uniqueidentifier**,、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_mergedummyupdate** は、マージレプリケーションで使用します。  
  
 **sp_mergedummyupdate** は、レプリケーション競合表示モジュール (Wzcnflct.exe) に独自の代替手段を記述する場合に便利です。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_mergedummyupdate**を実行できるのは、 **db_owner**固定データベースロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
