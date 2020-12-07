---
description: sp_showpendingchanges (Transact-SQL)
title: sp_showpendingchanges (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_showpendingchanges
- sp_showpendingchanges_TSQL
helpviewer_keywords:
- sp_showpendingchanges
ms.assetid: 8013a792-639d-4550-b262-e65d30f9d291
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 78b4901fc70299373044ce0720403031992e37a4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547402"
---
# <a name="sp_showpendingchanges-transact-sql"></a>sp_showpendingchanges (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  レプリケートを待機している変更を示す結果セットを返します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行され、サブスクライバー側でサブスクリプションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
> [!NOTE]  
>  この手順では、変更の数と、それらの変更に関連する行の概数を指定します。 たとえば、プロシージャは、パブリッシャーまたはサブスクライバーから情報を取得しますが、両方を同時に取得することはありません。 他のノードに格納されている情報は、プロシージャの推定値と比べて、同期する変更のセットが小さくなる場合があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_showpendingchanges [ [ @destination_server = ] 'destination_server' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article']  
    [ , [ @show_rows = ] show_rows]  
```  
  
## <a name="arguments"></a>引数  
`[ @destination_server = ] 'destination_server'` レプリケートされた変更が適用されるサーバーの名前を指定します。 *destination_server* は **sysname**で、既定値は NULL です。  
  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* は **sysname**,、既定値は NULL です。 *パブリケーション*が指定されている場合、結果は指定されたパブリケーションのみに制限されます。  
  
`[ @article = ] 'article'` アーティクルの名前を指定します。 *アーティクル* は **sysname**で、既定値は NULL です。 *Article*が指定されている場合、結果は指定されたアーティクルのみに制限されます。  
  
`[ @show_rows = ] 'show_rows'` 結果セットに保留中の変更に関するより具体的な情報が含まれているかどうかを指定します。既定値は **0**です。 値 **1** を指定した場合、結果セットには is_delete および rowguid という列が含まれます。  
  
## <a name="result-set"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|destination_server|**sysname**|変更がレプリケートされるサーバーの名前。|  
|pub_name|**sysname**|パブリケーションの名前を指定します。|  
|destination_db_name|**sysname**|変更がレプリケートされているデータベースの名前。|  
|is_dest_subscriber|**bit**|変更がサブスクライバーにレプリケートされていることを示します。 値が **1** の場合は、変更がサブスクライバーにレプリケートされていることを示します。 **0** は、変更がパブリッシャーにレプリケートされることを意味します。|  
|article_name|**sysname**|変更が行われたテーブルのアーティクルの名前です。|  
|pending_deletes|**int**|レプリケートを待機している削除の数。|  
|pending_ins_and_upd|**int**|レプリケートを待機している挿入と更新の数。|  
|is_delete|**bit**|保留中の変更が削除かどうかを示します。 値が **1** の場合は、変更が削除であることを示します。 では、に **1** を指定する必要があり @show_rows ます。|  
|rowguid|**uniqueidentifier**|変更された行を識別する GUID です。 では、に **1** を指定する必要があり @show_rows ます。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 sp_showpendingchanges は、マージ レプリケーションで使用します。  
  
 sp_showpendingchanges は、マージレプリケーションのトラブルシューティングを行うときに使用します。  
  
 sp_showpendingchanges の結果には、生成が 0 の行は含まれません。  
  
 *アーティクル*に指定されたアーティクルがパブリケーションに指定されたパブリケーションに属していない場合 *、* pending_deletes と pending_ins_and_upd に対して0のカウントが返されます。  
  
## <a name="permissions"></a>アクセス許可  
 sp_showpendingchanges を実行できるのは、固定サーバー ロール sysadmin または固定データベース ロール db_owner のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
