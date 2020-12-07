---
description: ActionEnum
title: ActionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ActionEnum
helpviewer_keywords:
- ActionEnum enumeration [ADOX]
ms.assetid: f948febd-c885-4621-823b-421e116fec4e
author: rothja
ms.author: jroth
ms.openlocfilehash: 02422de45f3e0ec28901678528468dc72f021549
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985923"
---
# <a name="actionenum"></a>ActionEnum
[SetPermissions](./setpermissions-method-adox.md)が呼び出されたときに実行されるアクションの種類を指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adAccessDeny**|3|グループまたはユーザーは、指定されたアクセス許可を拒否されます。|  
|**adAccessGrant**|1|グループまたはユーザーには、少なくとも要求されたアクセス許可が付与されます。|  
|**adAccessRevoke**|4|グループまたはユーザーの明示的なアクセス権はすべて取り消されます。|  
|**adAccessSet**|2|グループまたはユーザーには、要求されたアクセス許可だけが付与されます。|