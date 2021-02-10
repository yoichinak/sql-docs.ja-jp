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
ms.openlocfilehash: b23a6bc4354f4c67c07bcdc1f4b4d463fff072f2
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100056507"
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