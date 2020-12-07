---
description: FieldEnum
title: '|Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldEnum
helpviewer_keywords:
- FieldEnum enumeration [ADO]
ms.assetid: be4eda13-d4e4-4d6b-bb0d-3310b0a96fc2
author: rothja
ms.author: jroth
ms.openlocfilehash: 2bdcec83c211f71803ea64b7b78f3e6f8c76dee6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973133"
---
# <a name="fieldenum"></a>FieldEnum
[レコード](./record-object-ado.md)オブジェクトの[fields](./fields-collection-ado.md)コレクションで参照される特殊なフィールドを指定します。  
  
## <a name="remarks"></a>解説  
 これらの定数は、 **レコード**に関連付けられている特殊なフィールドにアクセスするための "ショートカット" を提供します。 **フィールドコレクションから**[フィールド](./field-object.md)オブジェクトを取得し、**フィールド**オブジェクトの[Value](./value-property-ado.md)プロパティを使用してその内容を取得します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|**レコード**に関連付けられている既定の[ストリーム](./stream-object-ado.md)オブジェクトを格納しているフィールドを参照します。|  
|**adRecordURL**|-2|現在の **レコード**の絶対 URL 文字列を含むフィールドを参照します。|