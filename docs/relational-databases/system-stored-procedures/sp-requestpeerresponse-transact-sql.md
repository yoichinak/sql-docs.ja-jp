---
description: sp_requestpeerresponse (Transact-SQL)
title: sp_requestpeerresponse (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_requestpeerresponse_TSQL
- sp_requestpeerresponse
helpviewer_keywords:
- sp_requestpeerresponse
ms.assetid: cbe13c22-4d7d-4a36-b194-7a13ce68ef27
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d07204928403d8ba99aa49688e51239dfdf08804
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543116"
---
# <a name="sp_requestpeerresponse-transact-sql"></a>sp_requestpeerresponse (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  このプロシージャは、ピアツーピアトポロジ内のノードから実行された場合、トポロジ内の他のすべてのノードからの応答を要求します。 この手順を実行し、対応する応答を確認することで、前のすべてのコマンドが応答ノードに配信されたことを保証できます。 このストアドプロシージャは、任意のデータベースの要求元のノードで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_requestpeerresponse [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
    [ , [ @request_id = ] request_id OUTPUT ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` 状態を確認するピアツーピアトポロジ内のパブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。  
  
`[ @description = ] 'description'` 個々の状態要求を識別するために使用できるユーザー定義の情報。 *説明* は **nvarchar (4000)**,、既定値は NULL です。  
  
`[ @request_id = ] request_id` 新しい要求の ID を返します。 *request_id* は **int** で、は出力パラメーターです。 この値は、 [sp_helppeerresponses &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md) を実行して、状態要求に対するすべての応答を表示する場合に使用できます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_requestpeerresponse** は、ピアツーピアトランザクションレプリケーションで使用されます。  
  
 **sp_requestpeerresponse** は、ピアツーピアトポロジでパブリッシュされたデータベースを復元する前に、すべてのコマンドが他のすべてのノードによって受信されたことを確認するために使用されます。 また、ノードがオフラインの間に行われたデータ定義言語 (DDL) の変更をレプリケートするときに、これらの変更が他のノードに到達する時間を推定する場合にも使用できます。  
  
 **sp_requestpeerresponse** は、ユーザー定義のトランザクション内では実行できません。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_requestpeerresponse**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_deletepeerrequesthistory &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerrequests &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)  
  
  
