---
description: dbo.sysプロキシ (Transact-sql)
title: dbo.sysプロキシ (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- dbo.sysproxies_TSQL
- sysproxies_TSQL
- dbo.sysproxies
- sysproxies
dev_langs:
- TSQL
helpviewer_keywords:
- sysproxies system table
ms.assetid: a73da875-be22-45fc-b5e2-ea7ebd48e2d6
author: cawrites
ms.author: chadam
ms.openlocfilehash: fb3f9c479086650752b550588bf8abe6c7f0e220
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99184674"
---
# <a name="dbosysproxies-transact-sql"></a>dbo.sysプロキシ (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  エージェントプロキシアカウントの属性を定義 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。 このテーブルは、 **msdb** データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|プロキシアカウントの ID。|  
|**name**|**sysname**|プロキシアカウントの名前。|  
|**credential_id**|**int**|プロキシアカウントが使用する資格情報の ID。|  
|**有効**|**tinyint**|プロキシ アカウントの状態。<br /><br /> **0** = 無効です。 **1** = 有効。|  
|**description**|**nvarchar(512)**|プロキシアカウントの作成時にユーザーが入力した説明。|  
|**user_sid**|**varbinary(85)**|プロキシ資格情報に関連付けられているユーザーまたはグループの Microsoft Windows *security_identifier* 。|  
|**credential_date_created**|**datetime**|資格情報が作成された日付と時刻。|  
  
## <a name="remarks"></a>コメント  
 **Sysproxies** テーブルにアクセスできるのは、 **sysadmin** 固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [dbo.sysproxylogin &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysproxylogin-transact-sql.md)   
 [dbo.sysproxysubsystem &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.sysサブシステム &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-syssubsystems-transact-sql.md)  
  
  
