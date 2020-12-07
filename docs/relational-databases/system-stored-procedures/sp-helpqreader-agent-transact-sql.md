---
description: sp_helpqreader_agent (Transact-SQL)
title: sp_helpqreader_agent (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpqreader_agent_TSQL
- sp_helpqreader_agent
helpviewer_keywords:
- sp_helpqreader_agent
ms.assetid: 8e74e1aa-e95b-4183-8017-bf123439b08d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9bdc306ed3622690e97b721f96c99dbc8efe0d1e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89526691"
---
# <a name="sp_helpqreader_agent-transact-sql"></a>sp_helpqreader_agent (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  キューリーダーエージェントのプロパティを返します。 このストアド プロシージャは、ディストリビューター側でディストリビューション データベースについて実行されます。またはパブリッシャー側で任意のデータベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpqreader_agent [ [ @frompublisher = ] frompublisher ]  
```  
  
## <a name="arguments"></a>引数  
`[ @frompublisher = ] frompublisher` ストアドプロシージャをパブリッシャー側とディストリビューター側のどちらで呼び出すかを指定します。 *frompublisher* の部分は bit で、既定値は0です。 **1** は、ストアドプロシージャがパブリッシャーから呼び出されることを示します。 **0** は、ストアドプロシージャがディストリビューターから呼び出されることを示します。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|エージェントの ID。|  
|**name**|**nvarchar (100)**|エージェントの名前。|  
|**job_id**|**uniqueidentifier**|エージェントジョブの一意の ID。|  
|**job_login**|**nvarchar(512)**|ディストリビューションエージェントを実行する Windows アカウントを指定します。このアカウントは、*ドメイン* \\ *ユーザー名*の形式で返されます。|  
|**job_password**|**sysname**|セキュリティ上の理由から、の値 **\*\*\*\*\*\*\*\*\*\*** は常に返されます。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_helpqreader_agent** は、トランザクションレプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 *Frompublisher*の値が**1**の場合、パブリッシャーの**sysadmin**固定サーバーロールのメンバー、またはパブリケーションデータベースの**db_owner**固定データベースロールのメンバーだけが**sp_helpqreader_agent**を実行できます。 それ以外の場合は、ディストリビューター側の固定サーバーロール **sysadmin** のメンバー、またはディストリビューションデータベースの **db_owner** 固定データベースロールのメンバーだけが **sp_helpqreader_agent**を実行できます。  
  
## <a name="see-also"></a>参照  
 [トランザクション パブリケーションの更新可能なサブスクリプションの有効化](../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
  
