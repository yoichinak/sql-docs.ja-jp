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
ms.openlocfilehash: fd2104a3b334da02e9bceee3ef191baac1d66cab
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100050793"
---
# <a name="actionenum"></a>ActionEnum
[SetPermissions](./setpermissions-method-adox.md)が呼び出されたときに実行されるアクションの種類を指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adAccessDeny**|3|グループまたはユーザーは、指定されたアクセス許可を拒否されます。|  
|**adAccessGrant**|1|グループまたはユーザーには、少なくとも要求されたアクセス許可が付与されます。|  
|**adAccessRevoke**|4|グループまたはユーザーの明示的なアクセス権はすべて取り消されます。|  
|**adAccessSet**|2|グループまたはユーザーには、要求されたアクセス許可だけが付与されます。|