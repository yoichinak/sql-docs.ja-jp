---
description: sp_helppeerrequests (Transact-SQL)
title: sp_helppeerrequests (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppeerrequests_TSQL
- sp_helppeerrequests
helpviewer_keywords:
- sp_helppeerrequests
ms.assetid: 37bd503e-46c4-47c6-996e-be7ffe636fe8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0ea9dce50e440c9b519032d46340b1b0a495eea0
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535154"
---
# <a name="sp_helppeerrequests-transact-sql"></a>sp_helppeerrequests (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ピアツーピアレプリケーショントポロジ内の参加者が受信したすべてのステータス要求に関する情報を返します。これらの要求は、トポロジ内のパブリッシュされたデータベースで [sp_requestpeerresponse &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) を実行することによって開始されます。 このストアドプロシージャは、ピアツーピアレプリケーショントポロジに参加しているパブリッシャー側のパブリケーションデータベースで実行されます。 詳細については、「[ピア ツー ピア トランザクション レプリケーション](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helppeerrequests [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` 状態要求が送信されたピアツーピアトポロジ内のパブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。  
  
`[ @description = ] 'description'` 個々の状態要求を識別するために使用できる値。これにより、 [transact-sql&#41;&#40;sp_requestpeerresponse ](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)を呼び出すときに指定されたユーザー定義情報に基づいて、返された応答をフィルター処理できます。 *説明* は **nvarchar (4000)**,、既定値は **%** です。 既定では、パブリケーションに対するすべてのステータス要求が返されます。 このパラメーターを使用して、 *description*に指定された値と一致する説明を含むステータス要求だけを返します。この場合、文字列は、 [LIKE &#40;transact-sql&#41;](../../t-sql/language-elements/like-transact-sql.md) 句を使用して照合されます。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|要求を識別します。|  
|**レプリケーション**|**sysname**|ステータス要求が送信されたパブリケーションの名前。|  
|**sent_date**|**datetime**|ステータス要求が送信された日付と時刻。|  
|**description**|**nvarchar (4000)**|個々の状態要求を識別するために使用できるユーザー定義情報。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_helppeerrequests** は、ピアツーピアトランザクションレプリケーションで使用されます。  
  
 **sp_helppeerrequests** は、ピアツーピアトポロジでパブリッシュされたデータベースを復元する場合に使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_helppeerrequests**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_deletepeerrequesthistory &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerresponses &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)  
  
  
