---
description: sysmail_help_queue_sp (Transact-SQL)
title: sysmail_help_queue_sp (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_queue_sp
- sysmail_help_queue_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_queue_sp
ms.assetid: 94840482-112c-4654-b480-9b456c4c2bca
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 18e7e8d96a766f628f15dfc747fc3154bc95ea57
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547257"
---
# <a name="sysmail_help_queue_sp-transact-sql"></a>sysmail_help_queue_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベース メールには、メール キューと状態キューの 2 つのキューがあります。 メール キューには、送信待ちのメール アイテムが格納され、 状態キューには、送信済みのアイテムの状態が格納されます。 このストアドプロシージャを使用すると、メールキューまたはステータスキューの状態を表示できます。 パラメーター ** \@ queue_type**が指定されていない場合、ストアドプロシージャは、キューごとに1つの行を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_help_queue_sp  [ @queue_type = ] 'queue_type'  
```  
  
## <a name="arguments"></a>引数  
`[ @queue_type = ] 'queue_type'` 省略可能な引数は、 *queue_type*として指定された種類の電子メールを削除します。 *queue_type* は **nvarchar (6)** で、既定値はありません。 有効なエントリは、 **mail** および **status**です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-set"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**queue_type**|**nvarchar (6)**|キューの種類。 指定できる値は、 **mail** および **status**です。|  
|**length**|**int**|指定したキュー内のメール アイテムの数。|  
|**状態**|**nvarchar (64)**|モニターの状態です。 有効な値は、[ **非** アクティブ] (キューが非アクティブ)、 **通知** された (キューの通知が受信されたことを示す)、 **RECEIVES_OCCURRING** (キューは受信中) です。|  
|**last_empty_rowset_time**|**/**|キューが最後に空だった日付と時刻。 [軍用時刻形式] と [GMT タイムゾーン]。|  
|**last_activated_time**|**/**|キューが最後にアクティブ化された日時。 [軍用時刻形式] と [GMT タイムゾーン]。|  
  
## <a name="remarks"></a>解説  
 データベースメールのトラブルシューティングを行う場合は、 **sysmail_help_queue_sp** を使用して、キューにあるアイテムの数、キューの状態、および最後にアクティブ化された日時を確認します。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、 **sysadmin** 固定サーバーロールのメンバーだけがこのプロシージャにアクセスできます。  
  
## <a name="examples"></a>例  
 次の例では、メール キューと状態キュー両方を返します。  
  
```  
EXECUTE msdb.dbo.sysmail_help_queue_sp ;  
GO  
```  
  
 このサンプルの結果セットは、長さに対して編集されています。  
  
```  
queue_type length      state              last_empty_rowset_time  last_activated_time  
---------- -------- ------------------ ----------------------- -----------------------  
mail       0        RECEIVES_OCCURRING 2005-10-07 21:14:47.010 2005-10-10 20:52:51.517  
status     0        INACTIVE           2005-10-07 21:04:47.003 2005-10-10 21:04:47.003  
  
(2 row(s) affected)  
  
```  
  
## <a name="see-also"></a>参照  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)  
  
  
