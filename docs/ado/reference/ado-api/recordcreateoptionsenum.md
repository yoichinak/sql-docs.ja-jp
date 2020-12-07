---
description: RecordCreateOptionsEnum
title: RecordCreateOptionsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordCreateOptionsEnum
helpviewer_keywords:
- RecordCreateOptionsEnum enumeration [ADO]
ms.assetid: 6d746670-0850-4065-9cd4-168dea1d3ea9
author: rothja
ms.author: jroth
ms.openlocfilehash: 4393196078b7800e1f1ec324c612918d7b8380e9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989823"
---
# <a name="recordcreateoptionsenum"></a>RecordCreateOptionsEnum
既存の**レコード**を開くか、 [Record](./record-object-ado.md)オブジェクトの[Open](./open-method-ado-record.md)メソッド用に新しい**レコード**を作成するかを指定します。 値は AND 演算子と組み合わせることができます。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adCreateCollection**|0x2000|既存の**レコード**を開く代わりに、 *Source*パラメーターで指定されたノードに新しい**レコード**を作成します。 ソースが既存のノードを指している場合、 **Adcreatecollection** が **Adopenifexists** または **adcreatecollection**と結合されていない限り、実行時エラーが発生します。|  
|**adCreateNonCollection**|0|[Adsimplerecord](./recordtypeenum.md)型の新しい**レコード**を作成します。|  
|**adCreateOverwrite**|0x4000000|作成フラグ **Adcreatecollection**、 **adcreatenoncollection**、および **adCreateStructDoc**を変更します。 またはをこの値と共に使用し、作成フラグの値の1つを使用すると、ソース URL が既存のノードまたは **レコード**を指している場合は、既存のレコードが上書きされ、その代わりに新しい **レコード** が作成されます。 この値は、 **Adopenifexists**と一緒に使用することはできません。|  
|**adCreateStructDoc**|0x80000000|既存の**レコード**を開く代わりに、 [adStructDoc](./recordtypeenum.md)型の新しい**レコード**を作成します。|  
|**adFailIfNotExists**|-1|既定値。 *ソース*が存在しないノードを指している場合、実行時エラーが発生します。|  
|**adOpenIfExists**|0x2000000|作成フラグ **Adcreatecollection**、 **adcreatenoncollection**、および **adCreateStructDoc**を変更します。 またはをこの値と共に使用し、作成フラグの値の1つを使用する場合、ソース URL が既存のノードまたは **レコード** オブジェクトを指している場合、プロバイダーは新しいレコードを作成するのではなく、既存の **レコード** を開く必要があります。 この値は **Adcreateoverwrite**と共に使用することはできません。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 これらの定数には、対応する ADO/WFC がありません。  
  
## <a name="applies-to"></a>適用対象  
 [Open メソッド (ADO Record)](./open-method-ado-record.md)