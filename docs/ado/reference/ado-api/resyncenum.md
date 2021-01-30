---
description: ResyncEnum
title: ResyncEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- ResyncEnum
helpviewer_keywords:
- ResyncEnum enumeration [ADO]
ms.assetid: d3df2c90-e570-4c40-a79a-25b3448a009c
author: rothja
ms.author: jroth
ms.openlocfilehash: c20965a348227583580bb75a807e792f74a9e967
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99166627"
---
# <a name="resyncenum"></a>ResyncEnum
再 [同期](./resync-method.md)の呼び出しによって基になる値を上書きするかどうかを指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adResyncAllValues**|2|既定値。 データを上書きします。保留中の更新は取り消されます。|  
|**adResyncUnderlyingValues**|1|はデータを上書きしません。保留中の更新は取り消されません。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums. ALLVALUES|  
|AdoEnums. UNDERLYINGVALUES|  
  
## <a name="applies-to"></a>適用対象  
 [Resync メソッド](./resync-method.md)