---
description: sp_helptracertokenhistory (Transact-SQL)
title: sp_helptracertokenhistory (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helptracertokenhistory_TSQL
- sp_helptracertokenhistory
helpviewer_keywords:
- sp_helptracertokenhistory
ms.assetid: 96910d1c-be76-43eb-9c93-4477e6761749
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4874af1c1defd949f4744a98f9f959995bf1d231
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547941"
---
# <a name="sp_helptracertokenhistory-transact-sql"></a>sp_helptracertokenhistory (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  指定されたトレーサー トークンの詳細な待機時間情報を、各サブスクライバーに対して 1 行ずつ返します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して、またはディストリビューター側でディストリビューションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helptracertokenhistory [ @publication = ] 'publication'   
        , [ @tracer_id = ] tracer_id  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` トレーサートークンが挿入されたパブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。  
  
`[ @tracer_id = ] tracer_id` 履歴情報が返される [MStracer_tokens &#40;transact-sql&#41;](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) テーブル内のトレーサートークンの ID を指定します。 *tracer_id* は **int**,、既定値はありません。  
  
`[ @publisher = ] 'publisher'` パブリッシャーの名前です。 *publisher* は **sysname**で、既定値は NULL です。  
  
> [!NOTE]
>  このパラメーターは、以外のパブリッシャーに対してのみ指定する必要があり [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
`[ @publisher_db = ] 'publisher_db'` パブリケーションデータベースの名前です。 *publisher_db* は **sysname**で、既定値は NULL です。 ストアドプロシージャがパブリッシャーで実行される場合、このパラメーターは無視されます。  
  
## <a name="result-set"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**distributor_latency**|**bigint**|トレーサートークンレコードがパブリッシャーでコミットされてからディストリビューター側でコミットされるまでの秒数。|  
|**サブスクライバ**|**sysname**|トレーサートークンを受け取ったサブスクライバーの名前。|  
|**subscriber_db**|**sysname**|トレーサートークンレコードが挿入されたサブスクリプションデータベースの名前。|  
|**subscriber_latency**|**bigint**|トレーサートークンレコードがディストリビューター側でコミットされてからサブスクライバー側でコミットされるまでの秒数。|  
|**overall_latency**|**bigint**|トレーサートークンレコードがパブリッシャーでコミットされてから、サブスクライバーでトークンレコードがコミットされるまでの秒数。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_helptracertokenhistory** は、トランザクションレプリケーションで使用します。  
  
 [&#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md)を実行 sp_helptracertokens て、パブリケーションのトレーサートークンの一覧を取得します。  
  
 結果セットの値が NULL の場合は、待機時間の統計を計算できないことを意味します。 これは、トレーサートークンがディストリビューターまたはいずれかのサブスクライバーで受信されていないためです。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-helptracertokenhistor_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_helptracertokenhistory**を実行できるのは、 **sysadmin**固定サーバーロールのメンバー、パブリケーションデータベースの固定データベースロール**db_owner** 、またはディストリビューションデータベースの**db_owner**固定データベースロールまたは**replmonitor**ロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [トランザクションレプリケーションの待機時間を計測して接続を検証する](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [sp_deletetracertokenhistory &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)  
  
  
