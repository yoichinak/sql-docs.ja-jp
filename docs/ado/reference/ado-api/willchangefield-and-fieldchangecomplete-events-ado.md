---
description: WillChangeField および FieldChangeComplete イベント (ADO)
title: Changefield および FieldChangeComplete イベント (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldChangeComplete
- Recordset::WillChangeField
- Recordset::FieldChangeComplete
- WillChangeField
helpviewer_keywords:
- WillChangeField event [ADO]
- fieldchangecomplete event [ADO]
ms.assetid: 3e49fb89-c45b-4d39-823e-3cc887c59b37
author: rothja
ms.author: jroth
ms.openlocfilehash: 836228d0741cdf4fd75db5d9c9e0c3d523848b50
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987883"
---
# <a name="willchangefield-and-fieldchangecomplete-events-ado"></a>WillChangeField および FieldChangeComplete イベント (ADO)
イベントは、保留**中の操作**によって[レコードセット](./recordset-object-ado.md)内の1つまたは複数の[フィールド](./field-object.md)オブジェクトの値が変更される前に呼び出されます。 **FieldChangeComplete**イベントは、1つまたは複数の**フィールド**オブジェクトの値が変更された後に呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
WillChangeField cFields, Fields, adStatus, pRecordset  
FieldChangeComplete cFields, Fields, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>パラメーター  
 *cFields*  
 *フィールド*内の**フィールド**オブジェクトの数を示す**Long**です。  
  
 *フィールド*  
 が**Changefield**の場合、 *Fields*パラメーターは、元の値を持つ**Field**オブジェクトを含む**variant**の配列です。 **FieldChangeComplete**の場合、 *Fields*パラメーターは、値が変更された**フィールド**オブジェクトを含む**variant**の配列です。  
  
 *pError*  
 [エラー](./error-object.md)オブジェクトです。 *Adstatus*の値が**adstatuserrorて**いる場合に発生したエラーについて説明します。それ以外の場合は設定されません。  
  
 *adStatus*  
 [Eventstatusenum](./eventstatusenum.md)状態の値です。  
  
 が **呼び出されたときに** 、イベントを発生させた操作が成功した場合、このパラメーターは **adstatusok** に設定されます。 このイベントが保留中の操作の取り消しを要求できない場合は、 **Adstatuscantdeny** に設定されます。  
  
 **FieldChangeComplete**が呼び出されると、このパラメーターは、イベントの原因となった操作が成功した場合は**adstatusok**に、操作が失敗した場合は**Adstatuserror curred**に設定されます。  
  
 **Changefield**が返される前に、このパラメーターを**adstatuscancel**に設定して、保留中の操作の取り消しを要求します。  
  
 **FieldChangeComplete**が返される前に、このパラメーターを**adStatusUnwantedEvent**に設定して、後続の通知が行われないようにします。  
  
 *pRecordset*  
 **レコードセット**オブジェクトです。 このイベントが発生した **レコードセット** 。  
  
## <a name="remarks"></a>解説  
 [Value](./value-property-ado.md)プロパティを設定し**FieldChangeComplete** 、フィールドと値の配列パラメーターを使用して[Update](./update-method.md)メソッドを呼び出す**と、が**発生する可能性があります。  
  
## <a name="see-also"></a>参照  
 [ADO Events モデルの例 (VC + +)](./ado-events-model-example-vc.md)   
 [ADO イベント ハンドラーの概要](../../guide/data/ado-event-handler-summary.md)