---
description: AllowNullsEnum
title: AllowNullsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- AllowNullsEnum
helpviewer_keywords:
- AllowNullsEnum enumeration [ADOX]
ms.assetid: 6acf3689-1a7f-4379-9d7f-df452ccbac27
author: rothja
ms.author: jroth
ms.openlocfilehash: c2d21b4a7e4de67e45210f11598a7cf3a2a99b9e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985543"
---
# <a name="allownullsenum"></a>AllowNullsEnum
Null 値を持つレコードのインデックスを作成するかどうかを指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|インデックスでは、キー列が null であるエントリが許可されます。 キー列に null 値を入力すると、エントリがインデックスに挿入されます。|  
|**adIndexNullsDisallow**|1|既定値。 インデックスでは、キー列が null であるエントリは許可されません。 キー列に null 値が入力されると、エラーが発生します。|  
|**adIndexNullsIgnore**|2|インデックスでは、null キーを含むエントリは挿入されません。 キー列に null 値を入力した場合、エントリは無視され、エラーは発生しません。|  
|**adIndexNullsIgnoreAny**|4|インデックスでは、一部のキー列が null 値を持つエントリは挿入されません。 複数列のキーを持つインデックスの場合、ある列に null 値を入力すると、エントリは無視され、エラーは発生しません。|  
  
## <a name="applies-to"></a>適用対象  
 [IndexNulls プロパティ (ADOX)](./indexnulls-property-adox.md)