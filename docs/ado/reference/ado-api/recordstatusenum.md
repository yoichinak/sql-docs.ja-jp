---
description: RecordStatusEnum
title: RecordStatusEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordStatusEnum
helpviewer_keywords:
- RecordStatusEnum enumeration [ADO]
ms.assetid: 506fdd70-4452-4e83-95d5-c94311988dfa
author: rothja
ms.author: jroth
ms.openlocfilehash: e4d2ad74187ef6be146be04f63e634bbdf3de9f5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989673"
---
# <a name="recordstatusenum"></a>RecordStatusEnum
バッチ更新やその他の一括操作に関して、レコードの [状態](./status-property-ado-recordset.md) を指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adRecCanceled**|0x100|操作が取り消されたため、レコードが保存されなかったことを示します。|  
|**adRecCantRelease**|0x400|既存のレコードがロックされていたため、新しいレコードが保存されなかったことを示します。|  
|**adRecConcurrencyViolation**|0x800|オプティミスティック同時実行制御が使用されていたため、レコードが保存されなかったことを示します。|  
|**adRecDBDeleted**|0x40000|レコードが既にデータソースから削除されていることを示します。|  
|**adRecDeleted**|0x4|レコードが削除されたことを示します。|  
|**adRecIntegrityViolation**|0x1000|ユーザーが整合性の制約に違反したため、レコードが保存されなかったことを示します。|  
|**adRecInvalid**|0x10|ブックマークが無効であるため、レコードが保存されなかったことを示します。|  
|**adRecMaxChangesExceeded**|0x2000|保留中の変更が多すぎたため、レコードが保存されなかったことを示します。|  
|**adRecModified**|0x2|レコードが変更されたことを示します。|  
|**adRecMultipleChanges**|0x40|複数のレコードが影響を受ける可能性があるため、レコードが保存されなかったことを示します。|  
|**adRecNew**|0x1|レコードが新規であることを示します。|  
|**adRecObjectOpen**|0x4000|開いているストレージオブジェクトと競合するため、レコードが保存されなかったことを示します。|  
|**adRecOK**|0|レコードが正常に更新されたことを示します。|  
|**adRecOutOfMemory**|0x8000|コンピューターのメモリが不足しているため、レコードが保存されなかったことを示します。|  
|**adRecPendingChanges**|0x80|保留中の挿入を参照しているため、レコードが保存されなかったことを示します。|  
|**adRecPermissionDenied**|0x10000|ユーザーに十分な権限がないため、レコードが保存されなかったことを示します。|  
|**adRecSchemaViolation**|0x20000|基になるデータベースの構造に違反するため、レコードが保存されなかったことを示します。|  
|**adRecUnmodified**|0x8|レコードが変更されていないことを示します。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 AdoEnums。  
  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums.RecordStatus.CANCELED|  
|AdoEnums.RecordStatus.CANTRELEASE|  
|AdoEnums.RecordStatus.CONCURRENCYVIOLATION|  
|AdoEnums.RecordStatus.DBDELETED|  
|AdoEnums.RecordStatus.DELETED|  
|AdoEnums.RecordStatus.INTEGRITYVIOLATION|  
|AdoEnums.RecordStatus.INVALID|  
|AdoEnums.RecordStatus.MAXCHANGESEXCEEDED|  
|AdoEnums.RecordStatus.MODIFIED|  
|AdoEnums.RecordStatus.MULTIPLECHANGES|  
|AdoEnums.RecordStatus.NEW|  
|AdoEnums.RecordStatus.OBJECTOPEN|  
|AdoEnums.RecordStatus.OK|  
|AdoEnums.RecordStatus.OUTOFMEMORY|  
|AdoEnums.RecordStatus.PENDINGCHANGES|  
|AdoEnums.RecordStatus.PERMISSIONDENIED|  
|AdoEnums (スキーマの状態)|  
|AdoEnums.RecordStatus.UNMODIFIED|  
  
## <a name="applies-to"></a>適用対象  
 [Status プロパティ (ADO Recordset)](./status-property-ado-recordset.md)