---
description: sp_help_agent_profile (Transact-SQL)
title: sp_help_agent_profile (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_help_agent_profile
- sp_help_agent_profile_TSQL
helpviewer_keywords:
- sp_help_agent_profile
ms.assetid: 5637b671-4aa3-497e-9a1c-c99798a1afb4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7bcb9de7480bf0aea92f585cfece47cf09545195
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538858"
---
# <a name="sp_help_agent_profile-transact-sql"></a>sp_help_agent_profile (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  指定されたエージェントのプロファイルを表示します。 このストアドプロシージャは、ディストリビューター側で任意のデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_agent_profile [ [ @agent_type = ] agent_type ]   
    [ , [ @profile_id = ] profile_id ]  
```  
  
## <a name="arguments"></a>引数  
`[ @agent_type = ] agent_type` エージェントの種類を示します。 *agent_type* は **int**,、既定値は **0**,、これらの値のいずれかを指定することができます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|スナップショット エージェント|  
|**2**|ログ リーダー エージェント (Log Reader Agent)|  
|**3**|ディストリビューション エージェント|  
|**4**|[マージ エージェント]|  
|**9**|キュー リーダー エージェント (Queue Reader Agent)|  
  
`[ @profile_id = ] profile_id` 表示するプロファイルの ID を指定します。 *profile_id* は **int**,、既定値は **-1**,、 **MSagent_profiles** テーブル内のすべてのプロファイルを返します。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|プロファイルの ID です。|  
|**profile_name**|**sysname**|エージェントの種類に対して一意です。|  
|**agent_type**|**int**|**1** = スナップショットエージェント<br /><br /> **2** = ログリーダーエージェント<br /><br /> **3** = ディストリビューションエージェント<br /><br /> **4** = マージエージェント<br /><br /> **9** = キューリーダーエージェント|  
|**Type**|**int**|**0** = システム<br /><br /> **1** = カスタム|  
|**description**|**varchar (3000)**|プロファイルの説明です。|  
|**def_profile**|**bit**|このプロファイルがこの種類のエージェントの既定のプロファイルかどうかを指定します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_help_agent_profile** は、すべての種類のレプリケーションで使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_help_agent_profile**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**replmonitor**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [レプリケーション エージェント プロファイルの操作](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [sp_add_agent_profile &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_drop_agent_profile &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)  
  
  
