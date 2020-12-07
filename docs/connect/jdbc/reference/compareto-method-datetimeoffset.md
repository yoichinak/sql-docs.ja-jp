---
description: compareTo (DateTimeOffset) メソッド
title: compareTo メソッド (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e4cf2ea4-0fe9-40ce-ba79-f2a2b616997e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2d4673597255819521bc5becf48a92908ea1330a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438004"
---
# <a name="compareto-method-datetimeoffset"></a>compareTo (DateTimeOffset) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  GMT での時間に基づいて、この **DateTimeOffset** オブジェクトを別の **DateTimeOffset** オブジェクトと比較します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int compareTo(DateTimeOffset other)  
```  
  
#### <a name="parameters"></a>パラメーター  
 現在のインスタンスと比較する [DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) 値です。  
  
## <a name="return-value"></a>戻り値  
 次の表で、このメソッドの戻り値について説明します。  
  
|戻り値|説明|  
|------------------|-----------------|  
|0|両方の **DateTimeOffset** オブジェクトは、同じ特定の時点を表します。|  
|負の数|この **DateTimeOffset** オブジェクトは、*other* より前の特定の時点を表します。|  
|正の数|この **DateTimeOffset** オブジェクトは、*other* より後の特定の時点を表します。|  
  
## <a name="remarks"></a>解説  
 2 つの **DateTimeOffset** オブジェクトが GMT で同じ時間を表している場合は、オフセットに基づいたオブジェクトの追加の順序はありません。  
  
## <a name="see-also"></a>参照  
 [DateTimeOffset クラス](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset のメンバー](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
