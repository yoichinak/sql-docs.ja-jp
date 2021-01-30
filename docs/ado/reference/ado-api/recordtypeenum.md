---
description: RecordTypeEnum
title: RecordTypeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- RecordTypeEnum
helpviewer_keywords:
- RecordTypeEnum enumeration [ADO]
ms.assetid: f557e537-015d-4ba7-8a41-a6f00b366a91
author: rothja
ms.author: jroth
ms.openlocfilehash: 8ef671384a552f240930e24a073f979f6e84da8d
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99166678"
---
# <a name="recordtypeenum"></a>RecordTypeEnum
[レコード](./record-object-ado.md)オブジェクトの種類を指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adSimpleRecord**|0|*単純な* レコードを示します (子ノードは含まれません)。|  
|**adCollectionRecord**|1|*コレクション* レコード (子ノードを含む) を示します。|  
|**adRecordUnknown**|-1|この **レコード** の型が不明であることを示します。|  
|**adStructDoc**|2|COM 構造化ドキュメントを表す特別な種類の *コレクション* レコードを示します。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 これらの定数には、対応する ADO/WFC がありません。  
  
## <a name="applies-to"></a>適用対象  
 [RecordType プロパティ (ADO)](./recordtype-property-ado.md)