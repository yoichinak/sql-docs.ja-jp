---
description: ResyncEnum
title: ResyncEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ResyncEnum
helpviewer_keywords:
- ResyncEnum enumeration [ADO]
ms.assetid: d3df2c90-e570-4c40-a79a-25b3448a009c
author: rothja
ms.author: jroth
ms.openlocfilehash: 0c98c0b0bae307f57e5a77c7ca4ac6b473f4d149
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989463"
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