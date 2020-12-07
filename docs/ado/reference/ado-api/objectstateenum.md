---
description: ObjectStateEnum
title: ObjectStateEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ObjectStateEnum
helpviewer_keywords:
- ObjectStateEnum enumeration [ADO]
ms.assetid: 32746558-097b-4749-989e-519aadf7e3f4
author: rothja
ms.author: jroth
ms.openlocfilehash: f89b433ae7e44b3b90c3a7ef1f8eca4bcd62f5ec
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990383"
---
# <a name="objectstateenum"></a>ObjectStateEnum
オブジェクトが開いているか閉じられているか、データソースに接続しているか、コマンドを実行しているか、データを取得しているかを指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|オブジェクトが閉じていることを示します。|  
|**adStateOpen**|1|オブジェクトが開いていることを示します。|  
|**adStateConnecting**|2|オブジェクトが接続していることを示します。|  
|**adStateExecuting**|4|オブジェクトがコマンドを実行していることを示します。|  
|**adStateFetching**|8|オブジェクトの行が取得されていることを示します。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums を終了しました。|  
|AdoEnums を開きます。|  
|AdoEnums。接続しています。|  
|AdoEnums.ObjectState.EXE|  
|AdoEnums を取得します。|  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [State プロパティ (ADO)](./state-property-ado.md)  
    :::column-end:::
    :::column:::
        [State プロパティ (ADO MD)](../ado-md-api/state-property-ado-md.md)  
    :::column-end:::
:::row-end:::