---
description: StringFormatEnum
title: StringFormatEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StringFormatEnum
helpviewer_keywords:
- StringFormatEnum enumeration [ADO]
ms.assetid: 28f7d1ec-092b-4323-a39d-d3f882c6c81a
author: rothja
ms.author: jroth
ms.openlocfilehash: 7fe580d45d20c65c313cd87b3fb47ef63bb349ca
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988423"
---
# <a name="stringformatenum"></a>StringFormatEnum
[レコードセット](./recordset-object-ado.md)を文字列として取得する場合の形式を指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adClipString**|2|*Rowdelimiter*で行を区切り、 *columndelimiter*で列を区切り、Null 値を*nullexpr*で区切ります。 [GetString](./getstring-method-ado.md)メソッドのこれら3つのパラメーターは、 **Adclipstring**の*StringFormat*でのみ有効です。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums StringFormat|  
  
## <a name="applies-to"></a>適用対象  
 [GetString メソッド (ADO)](./getstring-method-ado.md)