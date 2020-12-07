---
description: sp_unregister_custom_scripting (Transact-SQL)
title: sp_unregister_custom_scripting (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_unregister_custom_scripting_TSQL
- sp_unregister_custom_scripting
helpviewer_keywords:
- sp_unregister_custom_scripting
ms.assetid: b6e9e0d2-9144-434d-88af-4874f2582399
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1bb9545e4a74fdf6831317ee31f36488e781239d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547299"
---
# <a name="sp_unregister_custom_scripting-transact-sql"></a>sp_unregister_custom_scripting (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  このストアドプロシージャは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] [sp_register_custom_scripting](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)を実行して登録されたユーザー定義のカスタムストアドプロシージャまたはスクリプトファイルを削除します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_unregister_custom_scripting [ @type  = ] 'type'  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @type = ] 'type'` 削除するカスタムストアドプロシージャまたはスクリプトの種類を設定します。 *型* は **varchar (16)**,、既定値はありません、次の値のいずれかを指定することができます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**insert**|登録されたカスタムストアドプロシージャまたはスクリプトは、INSERT ステートメントがレプリケートされるときに実行されます。|  
|**update**|登録済みのカスタムストアドプロシージャまたはスクリプトは、UPDATE ステートメントがレプリケートされるときに実行されます。|  
|**delete**|登録済みのカスタムストアドプロシージャまたはスクリプトは、DELETE ステートメントがレプリケートされるときに実行されます。|  
|**custom_script**|登録済みのカスタムストアドプロシージャまたはスクリプトは、データ定義言語 (DDL) トリガーの最後に実行されます。|  
  
`[ @publication = ] 'publication'` カスタムストアドプロシージャまたはスクリプトを削除するパブリケーションの名前。 *publication* は **sysname**,、既定値は NULL です。  
  
`[ @article = ] 'article'` カスタムストアドプロシージャまたはスクリプトを削除するアーティクルの名前。 *アーティクル* は **sysname**で、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_unregister_custom_scripting** は、スナップショットレプリケーションおよびトランザクションレプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_unregister_custom_scripting**を実行できるのは、 **sysadmin**固定サーバーロール、 **db_owner**固定データベースロール、または**db_ddladmin**固定データベースロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_register_custom_scripting &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)  
  
  
