---
description: ParameterDirectionEnum
title: Parameterdirection Enum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ParameterDirectionEnum
helpviewer_keywords:
- ParameterDirectionEnum enumeration [ADO]
ms.assetid: c66aa6e6-d4f0-4f0f-9640-e08ae6cfdef3
author: rothja
ms.author: jroth
ms.openlocfilehash: b7422bf0037adc8d756c20c82404a7f3b06ae9e3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990133"
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