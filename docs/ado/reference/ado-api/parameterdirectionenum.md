---
description: ParameterDirectionEnum
title: Parameterdirection Enum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- ParameterDirectionEnum
helpviewer_keywords:
- ParameterDirectionEnum enumeration [ADO]
ms.assetid: c66aa6e6-d4f0-4f0f-9640-e08ae6cfdef3
author: rothja
ms.author: jroth
ms.openlocfilehash: 960164c8f881c3094493f3bbc828ef7982e75280
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99166884"
---
# <a name="parameterdirectionenum"></a>ParameterDirectionEnum
[パラメーター](./parameter-object.md)が入力パラメーター、出力パラメーター、入力パラメーターと出力パラメーターの両方、またはストアドプロシージャからの戻り値を表すかどうかを指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adParamInput**|1|既定値。 パラメーターが入力パラメーターを表すことを示します。|  
|**adParamInputOutput**|3|パラメーターが入力パラメーターと出力パラメーターの両方を表すことを示します。|  
|**adParamOutput**|2|パラメーターが出力パラメーターを表すことを示します。|  
|**adParamReturnValue**|4|パラメーターが戻り値を表すことを示します。|  
|**adParamUnknown**|0|パラメーターの方向が不明であることを示します。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums ParameterDirection|  
|AdoEnums. ParameterDirection. INPUTOUTPUT|  
|AdoEnums ParameterDirection|  
|AdoEnums ParameterDirection|  
|AdoEnums. ParameterDirection. 不明|  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [CreateParameter メソッド (ADO)](./createparameter-method-ado.md)  
    :::column-end:::
    :::column:::
        [Direction プロパティ](./direction-property.md)  
    :::column-end:::
:::row-end:::