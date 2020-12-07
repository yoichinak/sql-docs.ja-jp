---
description: sp_register_custom_scripting (Transact-SQL)
title: sp_register_custom_scripting (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_register_custom_scripting
- sp_register_custom_scripting_TSQL
helpviewer_keywords:
- sp_register_custom_scripting
ms.assetid: a8159282-de3b-4b9e-bdc9-3d3fce485c7f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4f73353cc5d2e0e9be02be5a0e6dc59eaf2f909f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547507"
---
# <a name="sp_register_custom_scripting-transact-sql"></a>sp_register_custom_scripting (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  レプリケーションでは、トランザクションレプリケーションで使用される1つ以上の既定のプロシージャを、ユーザー定義のカスタムストアドプロシージャで置き換えることができます。 レプリケートされたテーブルにスキーマ変更が行われると、これらのストアド プロシージャは再作成されます。 **sp_register_custom_scripting** は、 [!INCLUDE[tsql](../../includes/tsql-md.md)] 新しいユーザー定義カスタムストアドプロシージャの定義をスクリプト化するためにスキーマ変更が発生したときに実行されるストアドプロシージャまたはスクリプトファイルを登録します。 この新しいユーザー定義カスタム ストアド プロシージャには、テーブルに対する新しいスキーマを反映する必要があります。 パブリッシャー側のパブリケーションデータベースに対して**sp_register_custom_scripting**が実行されます。登録されているスクリプトファイルまたはストアドプロシージャは、スキーマの変更が発生したときにサブスクライバー側で実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_register_custom_scripting [ @type  = ] 'type'  
    [ @value = ] 'value'   
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @type = ] 'type'` 登録するカスタムストアドプロシージャまたはスクリプトの種類を設定します。 *型* は **varchar (16)**,、既定値はありません、次の値のいずれかを指定することができます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**insert**|登録されたカスタムストアドプロシージャは、INSERT ステートメントがレプリケートされるときに実行されます。|  
|**update**|登録したカスタム ストアド プロシージャを、UPDATE ステートメントがレプリケートされるときに実行。|  
|**delete**|登録したカスタム ストアド プロシージャを、DELETE ステートメントがレプリケートされるときに実行。|  
|**custom_script**|スクリプトは、データ定義言語 (DDL) トリガーの最後に実行されます。|  
  
`[ @value = ] 'value'` ストアドプロシージャの名前、または登録するスクリプトファイルの完全修飾パス名 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。 *値* は **nvarchar (1024)**,、既定値はありません。  
  
> [!NOTE]  
>  *値*パラメーターに NULL を指定すると、以前に登録したスクリプトの登録が解除されます。これは[sp_unregister_custom_scripting](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)を実行した場合と同じです。  
  
 *型*の値が**custom_script**の場合、スクリプトファイルの名前と完全パス [!INCLUDE[tsql](../../includes/tsql-md.md)] が必要です。 それ以外の場合、 *値* は登録されたストアドプロシージャの名前である必要があります。  
  
`[ @publication = ] 'publication'` カスタムストアドプロシージャまたはスクリプトを登録するパブリケーションの名前。 *publication* は **sysname**,、既定値は **NULL**です。  
  
`[ @article = ] 'article'` カスタムストアドプロシージャまたはスクリプトを登録するアーティクルの名前。 *アーティクル* は **sysname**で、既定値は **NULL**です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_register_custom_scripting** は、スナップショットレプリケーションおよびトランザクションレプリケーションで使用します。  
  
 レプリケートされたテーブルにスキーマを変更する前に、このストアドプロシージャを実行する必要があります。 このストアドプロシージャの使用方法の詳細については、「 [カスタムトランザクションプロシージャの再生成によるスキーマ変更の反映](../../relational-databases/replication/transactional/transactional-articles-regenerate-to-reflect-schema-changes.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_register_custom_scripting**を実行できるのは、 **sysadmin**固定サーバーロール、 **db_owner**固定データベースロール、または**db_ddladmin**固定データベースロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_unregister_custom_scripting &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)  
  
  
