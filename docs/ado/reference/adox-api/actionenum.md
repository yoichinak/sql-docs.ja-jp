---
description: ActionEnum
title: ActionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- ActionEnum
helpviewer_keywords:
- ActionEnum enumeration [ADOX]
ms.assetid: f948febd-c885-4621-823b-421e116fec4e
author: rothja
ms.author: jroth
ms.openlocfilehash: 35f4ddd60d4056cebbf0383aa0afb240c3ecb722
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99169668"
---
# <a name="actionenum"></a>ActionEnum
[SetPermissions](./setpermissions-method-adox.md)が呼び出されたときに実行されるアクションの種類を指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adAccessDeny**|3|グループまたはユーザーは、指定されたアクセス許可を拒否されます。|  
|**adAccessGrant**|1|グループまたはユーザーには、少なくとも要求されたアクセス許可が付与されます。|  
|**adAccessRevoke**|4|グループまたはユーザーの明示的なアクセス権はすべて取り消されます。|  
|**adAccessSet**|2|グループまたはユーザーには、要求されたアクセス許可だけが付与されます。|