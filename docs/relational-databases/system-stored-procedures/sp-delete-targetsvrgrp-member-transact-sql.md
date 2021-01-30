---
description: sp_delete_targetsvrgrp_member (Transact-sql)
title: sp_delete_targetsvrgrp_member (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sp_delete_targetsvrgrp_member_TSQL
- sp_delete_targetsvrgrp_member
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_targetsvrgrp_member
ms.assetid: 178a38d9-9b19-4648-95d7-e1397110d14c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4b363c9be51bb46339bfd6caac4ae389dda0a8b2
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99199124"
---
# <a name="sp_delete_targetsvrgrp_member-transact-sql"></a>sp_delete_targetsvrgrp_member (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ターゲット サーバー グループからターゲット サーバーを削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_delete_targetsvrgrp_member [ @group_name = ] 'group_name' , [ server_name = ] 'server_name'   
```  
  
## <a name="arguments"></a>引数  
`[ @group_name = ] 'group_name'` グループの名前。 *group_name* は **sysname** であり、既定値はありません。  
  
`[ @server_name = ] 'server_name'` 指定したグループから削除するサーバーの名前。 *server_name* は **nvarchar (30)**,、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 このストアドプロシージャを実行するには、 **sysadmin** 固定サーバーロールがユーザーに付与されている必要があります。  
  
## <a name="examples"></a>例  
 次の例では、 `LONDON1` 顧客情報グループを保持しているサーバーからサーバーを削除します。  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_targetsvrgrp_member   
    @group_name = N'Servers Maintaining Customer Information',  
    @server_name = N'LONDON1';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_targetsvrgrp_member &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-targetsvrgrp-member-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
