---
description: sp_help_category (Transact-SQL)
title: sp_help_category (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_category
- sp_help_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_category
ms.assetid: 8cad1dcc-b43e-43bd-bea0-cb0055c84169
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d500bad167bda9085d4caf40bdaa9e442cb26efb
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549708"
---
# <a name="sp_help_category-transact-sql"></a>sp_help_category (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ジョブ、警告、またはオペレーターについて、指定されたクラスの情報を提供します。  
   
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_category [ [ @class = ] 'class' ]   
     [ , [ @type = ] 'type' ]   
     [ , [ @name = ] 'name' ]   
     [ , [ @suffix = ] suffix ]   
```  
  
## <a name="arguments"></a>引数  
`[ @class = ] 'class'` 要求する情報に関するクラス。 *クラス* は **varchar (8)**,、既定値は **JOB**です。 *クラス* には、次のいずれかの値を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**補足**|ジョブカテゴリに関する情報を提供します。|  
|**アラート**|アラートカテゴリに関する情報を提供します。|  
|**OPERATOR**|オペレーター カテゴリに関する情報|  
  
`[ @type = ] 'type'` 情報を要求するカテゴリの種類。 *型* は **varchar (12)**,、既定値は NULL の場合、これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**LOCAL**|ローカルジョブカテゴリ。|  
|**MULTI -SERVER**|マルチサーバージョブカテゴリ。|  
|**NONE**|**JOB**以外のクラスのカテゴリ。|  
  
`[ @name = ] 'name'` 情報が要求されるカテゴリの名前。 *名前* は **sysname**,、既定値は NULL です。  
  
`[ @suffix = ] suffix` 結果セットの **category_type** 列が ID と名前のどちらであるかを指定します。 *サフィックス* は **ビット**,、既定値は **0**です。 **1** は **category_type** を名前として示し、 **0** は ID として表示します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 ** \@ サフィックス**が**0**の場合、 **sp_help_category**は次の結果セットを返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|カテゴリ ID。|  
|**category_type**|**tinyint**|カテゴリの種類:<br /><br /> **1** = ローカル<br /><br /> **2** = マルチサーバー<br /><br /> **3** = なし|  
|**name**|**sysname**|カテゴリ名|  
  
 ** \@ サフィックス**が**1**の場合、 **sp_help_category**は次の結果セットを返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|カテゴリ ID。|  
|**category_type**|**sysname**|カテゴリの種類。 **LOCAL**、 **MULTI SERVER**、または**NONE**のいずれか|  
|**name**|**sysname**|カテゴリ名|  
  
## <a name="remarks"></a>解説  
 **sp_help_category** は、 **msdb** データベースから実行する必要があります。  
  
 パラメーターを指定しない場合、結果セットではすべてのジョブ カテゴリに関する情報が提供されます。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、 **sysadmin** 固定サーバーロールのメンバーは、このストアドプロシージャを実行できます。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
## <a name="examples"></a>例  
  
### <a name="a-returning-local-job-information"></a>A. ローカルジョブ情報を返す  
 次の例では、ローカルで管理されるジョブに関する情報を返します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_category  
    @type = N'LOCAL' ;  
GO  
```  
  
### <a name="b-returning-alert-information"></a>B. アラート情報を返す  
 次の例では、レプリケーションの警告カテゴリに関する情報を返します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_category  
    @class = N'ALERT',  
    @name = N'Replication' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_category &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md)   
 [sp_delete_category &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [sp_update_category &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
