---
description: sp_add_agent_profile (Transact-SQL)
title: sp_add_agent_profile (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_add_agent_profile
- sp_add_agent_profile_TSQL
helpviewer_keywords:
- sp_add_agent_profile
ms.assetid: 5c246a33-2c21-4a77-9c2a-a2c9f0c5dda1
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 379e418cbca4b93fe38bf640f62cd357ef6b5a48
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419396"
---
# <a name="sp_add_agent_profile-transact-sql"></a>sp_add_agent_profile (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  レプリケーション エージェントの新しいプロファイルを作成します。 このストアドプロシージャは、ディストリビューター側で任意のデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_add_agent_profile [ [ @profile_id= ] profile_id OUTPUT ]  
        , [ @profile_name= ] 'profile_name'   
        , [ @agent_type= ] 'agent_type' ]   
    [ , [ @profile_type= ] profile_type ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @default= ] default ]  
```  
  
## <a name="arguments"></a>引数  
`[ @profile_id = ] profile_id` 新しく挿入されたプロファイルに関連付けられている ID を示します。 *profile_id* は **int** で、省略可能な出力パラメーターです。 指定した場合、値は新しいプロファイル ID に設定されます。  
  
`[ @profile_name = ] 'profile_name'` プロファイルの名前を指定します。 *profile_name* は **sysname**であり、既定値はありません。  
  
`[ @agent_type = ] 'agent_type'` レプリケーションエージェントの種類を示します。 *agent_type* は **int**,、既定値はありませんが、これらの値のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|スナップショット エージェント|  
|**2**|ログ リーダー エージェント (Log Reader Agent)|  
|**3**|ディストリビューション エージェント|  
|**4**|[マージ エージェント]|  
|**9**|キュー リーダー エージェント (Queue Reader Agent)|  
  
`[ @profile_type = ] profile_type` プロファイルの種類を示します。*profile_type* は **int**,、既定値は **1**です。  
  
 **0** はシステムプロファイルを示します。 **1** は、カスタムプロファイルを示します。 このストアドプロシージャを使用して作成できるのはカスタムプロファイルだけです。したがって、有効な値は **1**のみです。 は [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システムプロファイルのみを作成します。  
  
`[ @description = ] 'description'` プロファイルの説明を示します。 *説明* は **nvarchar (3000)**,、既定値はありません。  
  
`[ @default = ] default`*Agent_type* **の既定のプロファイルであるかどうかを示します。 *既定値* は **bit**,、既定値は **0**です。 **1** は、追加されるプロファイルが、 *agent_type*によって指定されたエージェントの新しい既定のプロファイルになることを示します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_add_agent_profile** は、スナップショットレプリケーション、トランザクションレプリケーション、およびマージレプリケーションで使用します。  
  
 カスタム エージェント プロファイルは、既定のエージェント パラメーター値を使用して追加されます。 [Sp_change_agent_parameter &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md)を使用してこれらの既定値を変更するか、 [transact-sql &#40;を sp_add_agent_parameter](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)してパラメーターを追加します。  
  
 **Sp_add_agent_profile**が実行されると、 [MSagent_profiles &#40;transact-sql&#41;](../../relational-databases/system-tables/msagent-profiles-transact-sql.md)テーブルの新しいカスタムプロファイルに行が追加され、このプロファイルに関連付けられた既定のパラメーターが MSagent_parameters [&#40;transact-sql&#41;](../../relational-databases/system-tables/msagent-parameters-transact-sql.md)テーブルに追加されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_add_agent_profile**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [レプリケーション エージェント プロファイルの操作](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [レプリケーション エージェント プロファイル](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [sp_add_agent_parameter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_change_agent_parameter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md)   
 [sp_change_agent_profile &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [sp_drop_agent_parameter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [sp_drop_agent_profile &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_parameter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [sp_help_agent_profile &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)  
  
  
