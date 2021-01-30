---
description: NamedParameters プロパティ (ADO)
title: NamedParameters プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- _Command::NamedParameters
helpviewer_keywords:
- NamedParameters property [ADO]
ms.assetid: 42409387-026c-435f-a9b1-bf4167095875
author: rothja
ms.author: jroth
ms.openlocfilehash: 9ce2c73ec00431f649d24a9effda2a7e9ecb6cfd
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99170778"
---
# <a name="namedparameters-property-ado"></a>NamedParameters プロパティ (ADO)
パラメーター名をプロバイダーに渡す必要があるかどうかを示します。  
  
## <a name="remarks"></a>コメント  
 このプロパティが true の場合、ADO は [コマンドオブジェクト](./command-object-ado.md)の **パラメーター** コレクション内の各パラメーターの **Name** プロパティの値を渡します。 プロバイダーは、パラメーター名を使用して、 **CommandText** または **commandstream** プロパティのパラメーターを照合します。 このプロパティが false (既定値) の場合、パラメーター名は無視され、パラメーターの順序を使用して、 **CommandText** または **commandstream** プロパティのパラメーターに値が一致します。  
  
## <a name="applies-to"></a>適用対象  
 [Command オブジェクト (ADO)](./command-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [CommandText プロパティ (ADO)](./commandtext-property-ado.md)   
 [CommandStream プロパティ (ADO)](./commandstream-property-ado.md)   
 [Parameters コレクション (ADO)](./parameters-collection-ado.md)