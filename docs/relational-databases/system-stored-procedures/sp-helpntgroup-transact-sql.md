---
description: sp_helpntgroup (Transact-SQL)
title: sp_helpntgroup (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpntgroup
- sp_helpntgroup_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpntgroup
ms.assetid: 02b4f7c1-480a-436c-8bae-7a2488be45d2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1a88caee8d332a4802f4281360f93392ae29aa2c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535172"
---
# <a name="sp_helpntgroup-transact-sql"></a>sp_helpntgroup (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベースのアカウントを持つ Windows グループに関する情報をレポートします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpntgroup [ [ @ntname= ] 'name' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @ntname = ] 'name'` Windows グループの名前を指定します。 *名前* は **sysname**,、既定値は NULL です。 *名前* は、現在のデータベースへのアクセス権を持つ有効な Windows グループである必要があります。 *名前*が指定されていない場合、現在のデータベースへのアクセス権を持つすべての Windows グループが出力に含まれます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**NTGroupName**|**sysname**|Windows グループの名前。|  
|**NTGroupId**|**smallint**|グループの識別子 (ID)。|  
|**SID**|**varbinary(85)**|**Ntgroupname**のセキュリティ識別子 (SID)。|  
|**HasDbAccess**|**int**|1 = Windows グループには、データベースにアクセスする権限があります。|  
  
## <a name="remarks"></a>解説  
 現在のデータベースのロールの一覧を表示するには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 **sp_helprole**を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、現在のデータベースへのアクセス権を持つ Windows グループの一覧を出力します。  
  
```  
EXEC sp_helpntgroup;  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [sp_helprole &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_revokedbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokedbaccess-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
