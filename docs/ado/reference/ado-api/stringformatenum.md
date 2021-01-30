---
description: StringFormatEnum
title: StringFormatEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- StringFormatEnum
helpviewer_keywords:
- StringFormatEnum enumeration [ADO]
ms.assetid: 28f7d1ec-092b-4323-a39d-d3f882c6c81a
author: rothja
ms.author: jroth
ms.openlocfilehash: 199aaab9215165e06598ca0c1be783b0a123a1c5
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99166393"
---
# <a name="stringformatenum"></a>StringFormatEnum
[レコードセット](./recordset-object-ado.md)を文字列として取得する場合の形式を指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adClipString**|2|*Rowdelimiter* で行を区切り、 *columndelimiter* で列を区切り、Null 値を *nullexpr* で区切ります。 [GetString](./getstring-method-ado.md)メソッドのこれら3つのパラメーターは、 **Adclipstring** の *StringFormat* でのみ有効です。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums StringFormat|  
  
## <a name="applies-to"></a>適用対象  
 [GetString メソッド (ADO)](./getstring-method-ado.md)