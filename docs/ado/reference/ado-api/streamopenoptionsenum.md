---
description: StreamOpenOptionsEnum
title: StreamOpenOptionsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamOpenOptionsEnum
helpviewer_keywords:
- StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
author: rothja
ms.author: jroth
ms.openlocfilehash: 8f3865a3b0e550e7e3fe4887fb948bca72eadf1b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988503"
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
[ストリーム](./stream-object-ado.md)オブジェクトを開くためのオプションを指定します。 値は OR 演算と組み合わせることができます。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|非同期モードで **ストリーム** オブジェクトを開きます。|  
|**adOpenStreamFromRecord**|4|*ソース*パラメーターの内容を、既に開いている[レコード](./record-object-ado.md)オブジェクトとして識別します。 既定の動作では、 *ソース* はツリー構造内のノードを直接指す URL として扱われます。 そのノードに関連付けられている既定のストリームが開きます。|  
|**adOpenStreamUnspecified**|-1|既定値。 既定のオプションを使用して **ストリーム** オブジェクトを開くことを指定します。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 これらの定数には、対応する ADO/WFC がありません。  
  
## <a name="applies-to"></a>適用対象  
 [Open メソッド (ADO Stream)](./open-method-ado-stream.md)