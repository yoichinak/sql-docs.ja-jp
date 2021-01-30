---
description: xp_enumgroups (Transact-sql)
title: xp_enumgroups (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- xp_enumgroups_TSQL
- xp_enumgroups
dev_langs:
- TSQL
helpviewer_keywords:
- xp_enumgroups
ms.assetid: 0bd3ed36-e260-469c-a5ff-b033fb9ea59d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a0319158b7e2627bac7cd67a8f15e10dc4694b51
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99124072"
---
# <a name="xp_enumgroups-transact-sql"></a>xp_enumgroups (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ローカルの Microsoft Windows グループの一覧、または指定された Windows ドメインで定義されているグローバルグループの一覧が表示されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
xp_enumgroups [ 'domain_name' ]  
```  
  
## <a name="arguments"></a>引数  
 **'** *domain_name* **'**  
 グローバル グループの一覧を列挙する Windows ドメインの名前を指定します。 *domain_name* は **sysname**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**group**|**sysname**|Windows グループの名前|  
|**comment**|**sysname**|Windows によって提供される Windows グループの説明|  
  
## <a name="remarks"></a>コメント  
 *Domain_name* が、のインスタンスが実行されている Windows ベースのコンピューターの名前である場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] またはドメイン名が指定されていない場合 **xp_enumgroups** は、を実行しているコンピューターからローカルグループを列挙し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
 のインスタンス [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が Windows 98 で実行されている場合、xp_enumgroups は使用できません。  
  
## <a name="permissions"></a>アクセス許可  
 **Master** データベースの **db_owner** 固定データベースロールのメンバーシップ、または **sysadmin** 固定サーバーロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、ドメイン内のグループを一覧表示し `sales` ます。  
  
```  
EXEC xp_enumgroups 'sales';  
```  
  
## <a name="see-also"></a>参照  
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;の一般的な拡張ストアドプロシージャ ](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_loginconfig &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [xp_logininfo &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
