---
description: FieldStatusEnum
title: FieldStatusEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldStatusEnum
helpviewer_keywords:
- FieldStatusEnum enumeration [ADO]
ms.assetid: e06da1e2-303f-41b2-a3b0-61e233da152c
author: rothja
ms.author: jroth
ms.openlocfilehash: d30c0bc3508c364b7a0d52f23ccb52d11e06f8d5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973093"
---
# <a name="fieldstatusenum"></a>FieldStatusEnum
[フィールドオブジェクト](./field-object.md)の[状態](./status-property-ado-field.md)を指定します。  
  
 **Adfieldpending \* **値は、状態が設定される原因となった操作を示し、他のステータス値と組み合わせることができます。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**Adfieldexists が既に存在します**|26|指定したフィールドが既に存在することを示します。|  
|**Adの Dbadstatus**|12|無効な状態値が ADO から OLE DB プロバイダーに送信されたことを示します。 原因としては、1.0 または1.1 プロバイダーの OLE DB、または [値](./value-property-ado.md) と [状態](./status-property-ado-field.md)の不適切な組み合わせが考えられます。|  
|**adFieldCannotComplete**|20|は、 [Source](./source-property-ado-record.md) によって指定された URL のサーバーが操作を完了できなかったことを示します。|  
|**adFieldCannotDeleteSource**|23|移動操作中に、ツリーまたはサブツリーが新しい場所に移動されたが、ソースを削除できなかったことを示します。|  
|**adFieldCantConvertValue**|2|データを失うことなく、フィールドを取得または保存できないことを示します。|  
|**adFieldCantCreate**|7|プロバイダーが制限 (許容されるフィールド数など) を超えたため、フィールドを追加できなかったことを示します。|  
|**adFieldDataOverflow**|6|プロバイダーから返されたデータがフィールドのデータ型でオーバーフローしたことを示します。|  
|**adFieldDefault**|13|データを設定するときにフィールドの既定値が使用されたことを示します。|  
|**adFieldDoesNotExist**|16|指定されたフィールドが存在しないことを示します。|  
|**adFieldIgnore**|15|ソースでデータ値を設定するときに、このフィールドがスキップされたことを示します。 プロバイダーに値が設定されていません。|  
|**adFieldIntegrityViolation**|10|計算されたエンティティまたは派生エンティティであるため、フィールドを変更できないことを示します。|  
|**adFieldInvalidURL**|17|データソース URL に無効な文字が含まれていることを示します。|  
|**Adの Disnull**|3|プロバイダーが VT_NULL 型のバリアント値を返し、フィールドが空でないことを示します。|  
|**adFieldOK**|0|既定値。 フィールドが正常に追加または削除されたことを示します。|  
|**adFieldOutOfSpace**|22|移動またはコピー操作を完了するのに十分な記憶域スペースをプロバイダーが取得できないことを示します。|  
|**adFieldPendingChange**|0x40000|フィールドが削除された後、別のデータ型で再追加されたか、以前に **adFieldOK** の状態だったフィールドの値が変更されたことを示します。 フィールドの最終形式では、 [Update](./update-method.md)メソッドが呼び出された後に[フィールド](./fields-collection-ado.md)コレクションが変更されます。|  
|**adFieldPendingDelete**|0x20000|**削除**操作によって状態が設定されたことを示します。 フィールドは、 **Update**メソッドが呼び出された後に、**フィールド**コレクションから削除するようにマークされています。|  
|**adFieldPendingInsert**|0x10000|**追加**操作によって状態が設定されたことを示します。 **フィールド**は、 **Update**メソッドが呼び出された後に**フィールド**コレクションに追加されるようにマークされています。|  
|**adFieldPendingUnknown**|0x80000|フィールドの状態を設定する原因となった操作をプロバイダーが判別できないことを示します。|  
|**adFieldPendingUnknownDelete**|0x100000|プロバイダーが、フィールドの状態を設定する原因となった操作を判別できないこと、および**更新**メソッドが呼び出された後**にフィールドがフィールドコレクションから**削除されることを示します。|  
|**adFieldPermissionDenied**|9|読み取り専用として定義されているため、フィールドを変更できないことを示します。|  
|**adFieldReadOnly**|24|データソース内のフィールドが読み取り専用として定義されていることを示します。|  
|**adFieldResourceExists**|19|オブジェクトが既に送信先 URL に存在し、オブジェクトを上書きできないため、プロバイダーが操作を実行できなかったことを示します。|  
|**adFieldResourceLocked**|18|データソースが1つ以上の他のアプリケーションまたはプロセスによってロックされているため、プロバイダーが操作を実行できなかったことを示します。|  
|**adFieldResourceOutOfScope**|25|送信元または送信先の URL が現在のレコードの範囲外であることを示します。|  
|**adfieldschemaviol**|11|値がフィールドのデータソーススキーマ制約に違反したことを示します。|  
|**adFieldSignMismatch**|5|プロバイダーによって返されたデータ値が署名されているが、ADO フィールド値のデータ型が符号なしであったことを示します。|  
|**adFieldTruncated**|4|データソースからの読み取り時に可変長データが切り捨てられたことを示します。|  
|**adFieldUnavailable 使用できません**|8|プロバイダーが、データソースからの読み取り時に値を特定できなかったことを示します。 たとえば、行は作成されたばかりで、列の既定値は使用できず、新しい値はまだ指定されていません。|  
|**adFieldVolumeNotFound**|21|プロバイダーが URL で指定されたストレージボリュームを見つけることができないことを示します。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 これらの定数には、対応する ADO/WFC がありません。  
  
## <a name="applies-to"></a>適用対象  
 [Status プロパティ (ADO Field)](./status-property-ado-field.md)