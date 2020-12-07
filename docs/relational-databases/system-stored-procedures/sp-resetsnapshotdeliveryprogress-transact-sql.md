---
description: sp_resetsnapshotdeliveryprogress (Transact-SQL)
title: sp_resetsnapshotdeliveryprogress (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_resetsnapshotdeliveryprogress
- sp_resetsnapshotdeliveryprogress_TSQL
helpviewer_keywords:
- sp_resetsnapshotdeliveryprogress
ms.assetid: 5df7d86b-d343-4d9b-88b1-74429ed092e6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b4bcee8dfc47a489fc605bcd3bd787a1ed393329
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543085"
---
# <a name="sp_resetsnapshotdeliveryprogress-transact-sql"></a>sp_resetsnapshotdeliveryprogress (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  スナップショットの配信が再起動できるように、プル サブスクリプションのスナップショット配信処理をリセットします。 サブスクライバー側でサブスクリプション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_resetsnapshotdeliveryprogress [ [ @verbose_level = ] verbose_level ]  
    [ , [ @drop_table = ] 'drop_table' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @verbose_level = ] verbose_level` 返される情報の量を指定します。 *verbose_level*は **int**,、既定値は **1**です。 値 **1** は、 **Mssnapshotdeliveryprogress** テーブルで必要なロックを取得できない場合にエラーが返されることを意味し、 **0** はエラーが返されないことを意味します。  
  
`[ @drop_table = ] 'drop_table'` スナップショットの進行状況に関する情報を含むテーブルを削除するか、切り捨てるかを指定します。*drop_table* は **nvarchar (5)**,、既定値は **FALSE**です。 false は、テーブルが切り捨てられることを意味し、true はテーブルが削除されることを意味します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_resetsnapshotdeliveryprogress** は、 **Mssnapshotdeliveryprogress** テーブル内のすべての行を削除します。 これにより、スナップショット配信プロセスで行われた以前の進行状況によって、サブスクリプションデータベースで残されているすべてのメタデータが実質的に削除されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_resetsnapshotdeliveryprogress**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
