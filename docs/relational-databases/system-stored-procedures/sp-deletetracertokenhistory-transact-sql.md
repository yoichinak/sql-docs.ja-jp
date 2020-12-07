---
description: sp_deletetracertokenhistory (Transact-SQL)
title: sp_deletetracertokenhistory (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_deletetracertokenhistory
- sp_deletetracertokenhistory_TSQL
helpviewer_keywords:
- sp_deletetracertokenhistory
ms.assetid: 9ae1be14-0d2f-40b1-9d6e-22d79726abf4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c08b5373109ab3ea6174aac190ed8fb7b04b2e0e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543540"
---
# <a name="sp_deletetracertokenhistory-transact-sql"></a>sp_deletetracertokenhistory (Transact-SQL)

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

[MStracer_tokens &#40;transact-sql&#41;](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md)からトレーサートークンレコードを削除し、 [transact-sql &#40;システムテーブル&#41;MStracer_history](../../relational-databases/system-tables/mstracer-history-transact-sql.md)します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して、またはディストリビューター側でディストリビューションデータベースに対して実行されます。

![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>構文

```
sp_deletetracertokenhistory [ @publication = ] 'publication'
    [ , [ @tracer_id = ] tracer_id ]
    [ , [ @cutoff_date = ] cutoff_date ]
    [ , [ @publisher = ] 'publisher' ]
    [ , [ @publisher_db = ] 'publisher_db' ]
```

## <a name="arguments"></a>引数

`@publication= 'publication'`  
トレーサートークンが挿入されたパブリケーションの名前を指定します。 データ型は **sysname**です。 このパラメーターは必須です。

`[ @tracer_id= ] tracer_id`  
削除するトレーサートークンの ID を示します。 データ型は **int**です。既定値は *null*です。 *Null*の場合、パブリケーションに属するすべてのトレーサートークンが削除されます。

`[ @cutoff_date= ] cutoff_date`  
この日付が削除される前に、パブリケーションに挿入されたトレーサートークン。 データ型は **datetime**です。 既定値は *null* です。

`[ @publisher= ] 'publisher'`  
パブリッシャーの名前です。 データ型は **sysname**です。 既定値は *null* です。

> [!NOTE]
> このパラメーターは、以外の [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パブリッシャー、またはディストリビューターからストアドプロシージャを実行する場合にのみ指定する必要があります。

`[ @publisher_db= ] 'publisher_db'`  
パブリケーション データベースの名前です。 データ型は **sysname**です。 既定値は NULL です。 ストアドプロシージャがパブリッシャーで実行される場合、このパラメーターは無視されます。

> [!NOTE]
> このパラメーターは、ディストリビューターからストアドプロシージャを実行するときに指定する必要があります。

## <a name="return-code-values"></a>リターン コードの値

**0** (成功) または **1** (失敗)

## <a name="remarks"></a>解説

**sp_deletetracertokenhistory** は、トランザクションレプリケーションで使用します。  

*Tracer_id*と*cutoff_date*の両方のパラメーターを指定すると、エラーが発生します。

トレーサートークンメタデータを削除するために **sp_deletetracertokenhistory** を実行しない場合、定期的にスケジュールされた履歴のクリーンアップが行われるときに、情報が削除されます。

トレーサートークン Id を確認するには [sp_helptracertokens &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md) を実行するか MStracer_tokens、 [transact-sql &#40;](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) システムテーブルに対してクエリを実行します。

## <a name="permissions"></a>アクセス許可

**Sp_deletetracertokenhistory**を実行する権限は、次の担当者にのみ与えられます。

- ディストリビューションデータベース内の **replmonitor** ロールのメンバー
- **Sysadmin**固定サーバーロールのメンバー。
- パブリケーションデータベースの **db_owner** 固定データベースロールのメンバー。
- 固定データベースの **db_owner** 。

## <a name="see-also"></a>参照

[待機時間を計測して Connections for Transactional Replication を検証します。](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)

[sp_helptracertokenhistory &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)
