---
description: StreamWriteEnum
title: StreamWriteEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- StreamWriteEnum
helpviewer_keywords:
- StreamWriteEnum enumeration [ADO]
ms.assetid: bdbf3405-a0bd-4f02-85d4-e3fe8da3f3f7
author: rothja
ms.author: jroth
ms.openlocfilehash: 5be021aab95fb9fa2c0571deba176f30836a7f4e
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99170110"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
[ストリーム](./stream-object-ado.md)オブジェクトに書き込まれる文字列に行の区切り記号を追加するかどうかを指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|既定値。 指定された ( *データ* パラメーターによって指定された) テキスト文字列を **ストリーム** オブジェクトに書き込みます。|  
|**adWriteLine**|1|**ストリーム** オブジェクトにテキスト文字列と行区切り記号を書き込みます。 [Lineseparator](./lineseparator-property-ado.md)プロパティが定義されていない場合は、実行時エラーが返されます。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 これらの定数には、対応する ADO/WFC がありません。  
  
## <a name="applies-to"></a>適用対象  
 [WriteText メソッド](./writetext-method.md)