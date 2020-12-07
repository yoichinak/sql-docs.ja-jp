---
description: sp_script_synctran_commands (Transact-sql)
title: sp_script_synctran_commands (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_script_synctran_commands
- sp_script_synctran_commands_TSQL
helpviewer_keywords:
- sp_script_synctran_commands
ms.assetid: f132694a-dd05-405b-9d84-21acce9e564a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f596a02346748cedcc6b99ada4e0a6122b184673
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541598"
---
# <a name="sp_script_synctran_commands-transact-sql"></a>sp_script_synctran_commands (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  更新可能なサブスクリプションのサブスクライバーで適用される **sp_addsynctrigger** 呼び出しを含むスクリプトを生成します。 パブリケーション内の各アーティクルに対して1つの **sp_addsynctrigger** 呼び出しがあります。 生成されたスクリプトには、キューに置かれたパブリケーションを処理するために必要な**MSsubsciption_articles**テーブルを作成する**sp_addqueued_artinfo**呼び出しも含まれています。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_script_synctran_commands [@publication = ] 'publication'  
    [ , [@article = ] 'article']  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` スクリプトを記述するパブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。  
  
`[ @article = ] 'article'` スクリプトを記述するアーティクルの名前を指定します。 *アーティクル* は **sysname**で、既定値は **all**です。これはすべてのアーティクルをスクリプト化することを指定します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="results-set"></a>結果セット  
 **sp_script_synctran_commands** は、1つの **nvarchar (4000)** 列で構成される結果セットを返します。 結果セットは、サブスクライバーで適用される **sp_addsynctrigger** と **sp_addqueued_artinfo** 呼び出しの両方を作成するために必要なスクリプト全体を形成します。  
  
## <a name="remarks"></a>解説  
 **sp_script_synctran_commands** は、スナップショットレプリケーションおよびトランザクションレプリケーションで使用します。  
  
 キュー更新可能なサブスクリプションには**sp_addqueued_artinfo**が使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_script_synctran_commands**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_addsynctriggers &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsynctriggers-transact-sql.md)   
 [sp_addqueued_artinfo &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addqueued-artinfo-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
