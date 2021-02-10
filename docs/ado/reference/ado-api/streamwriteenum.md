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
ms.openlocfilehash: f0f102ec1457b0cb327ab563ee348cf4112c749a
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100056547"
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