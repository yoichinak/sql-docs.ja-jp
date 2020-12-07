---
description: login_token (Transact-sql)
title: login_token (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- login_token_TSQL
- sys.login_token_TSQL
- sys.login_token
- login_token
dev_langs:
- TSQL
helpviewer_keywords:
- sys.login_token catalog view
- logins [SQL Server], security tokens
- tokens [SQL Server]
ms.assetid: 86e06938-9d0a-44e5-99e2-55c8ef5f2f84
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 339964a859d5e95d88853781a8b2b43f341f23be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88377808"
---
# <a name="syslogin_token-transact-sql"></a>login_token (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ログイン トークンの一部であるサーバー プリンシパルすべてに 1 行を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**principal_id**|**int**|プリンシパルの ID です。 この値は、サーバー内で一意です。|  
|**sid**|**varbinary (85)**|プリンシパルのセキュリティ識別子です。 Windows プリンシパルの場合は、 **sid** = windows sid です。 ログインが証明書にマップされている場合は、証明書の **sid** = GUID になります。|  
|**name**|**nvarchar(128)**|プリンシパルの名前。 この値は、サーバー内で一意です。|  
|**type**|**nvarchar(128)**|プリンシパルの種類の説明。 すべての型が **sid**にマップされます。 値は次のいずれかになります。<br /><br /> SQL ログイン<br /><br /> WINDOWS ログイン<br /><br /> WINDOWS GROUP<br /><br /> SERVER ROLE<br /><br /> 証明書にマップされたログイン<br /><br /> LOGIN MAPPED TO ASYMMETRIC KEY<br /><br /> CERTIFICATE<br /><br /> ASYMMETRIC KEY|  
|**ユーセジリンク**|**nvarchar(128)**|GRANT または DENY 権限の評価にプリンシパルが参加するかどうか、または認証子としての役割を果たすかどうかを示します。<br /><br /> この値は、次のいずれかです。<br /><br /> GRANT または DENY<br /><br /> 拒否のみ<br /><br /> アプリ|  
  
## <a name="see-also"></a>参照  
 [user_token &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-user-token-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
