---
description: Delete メソッド (ADO Recordset)
title: Delete メソッド (ADO Recordset) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Delete
- Recordset15::Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 1eb9209c-602c-4507-b0c2-6527a599b67d
author: rothja
ms.author: jroth
ms.openlocfilehash: a43aa64d970865b8de706fc4297bba9fd0d18786
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974093"
---
# <a name="delete-method-ado-recordset"></a>Delete メソッド (ADO Recordset)
現在のレコードまたはレコードのグループを削除します。  
  
## <a name="syntax"></a>構文  
  
```  
  
recordset.Delete AffectRecords  
```  
  
#### <a name="parameters"></a>パラメーター  
 *AffectRecords*  
 **Delete**メソッドによって影響を受けるレコードの数を決定する[AffectEnum](../../../ado/reference/ado-api/affectenum.md)値。 既定値は [ **adて、現在**の値です。  
  
> [!NOTE]
>  **adAffectAll** と **AdAffectAllChapters** は、 **削除**する有効な引数ではありません。  
  
## <a name="remarks"></a>解説  
 **Delete**メソッドを使用すると、[レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト内の現在のレコードまたはレコードのグループが削除対象としてマークされます。 レコード **セット** オブジェクトでレコードの削除が許可されていない場合、エラーが発生します。 即時更新モードの場合、削除はすぐにデータベースで発生します。 たとえば、データベースの整合性違反が原因でレコードを正常に削除できない場合、レコードは [更新](../../../ado/reference/ado-api/update-method.md)の呼び出し後も編集モードのままになります。 つまり、現在のレコードから移動する前に、 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) で更新プログラムをキャンセルする必要があります (たとえば、 [Close](../../../ado/reference/ado-api/close-method-ado.md)、 [Move](../../../ado/reference/ado-api/move-method-ado.md)、 [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)など)。  
  
 バッチ更新モードの場合、レコードはキャッシュから削除対象としてマークされ、実際の削除は、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) メソッドを呼び出したときに行われます。 削除されたレコードを表示するには、 [Filter](../../../ado/reference/ado-api/filter-property.md) プロパティを使用します。  
  
 削除されたレコードからフィールド値を取得すると、エラーが発生します。 現在のレコードを削除すると、別のレコードに移動するまで、削除されたレコードは最新の状態のままになります。 削除されたレコードから移動すると、アクセスできなくなります。  
  
 トランザクションで削除を入れ子にすると、 [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) メソッドを使用して削除されたレコードを復元できます。 バッチ更新モードの場合は、 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) メソッドを使用して保留中の削除または保留中の削除のグループを取り消すことができます。  
  
 基になるデータと競合しているためにレコードを削除しようとして失敗した場合 (たとえば、レコードが別のユーザーによって既に削除されている場合)、プロバイダは [Errors](../../../ado/reference/ado-api/errors-collection-ado.md) コレクションに警告を返しますが、プログラムの実行を停止することはありません。 実行時エラーは、要求されたすべてのレコードに競合がある場合にのみ発生します。  
  
 [Unique table](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)動的プロパティが設定されていて、**レコードセット**が複数のテーブルに対して結合操作を実行した結果である場合、 **Delete**メソッドでは、[一意のテーブル](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)プロパティのという名前のテーブルからのみ行が削除されます。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Delete メソッドの例 (VB)](../../../ado/reference/ado-api/delete-method-example-vb.md)   
 [Delete メソッドの例 (VBScript)](../../../ado/reference/ado-api/delete-method-example-vbscript.md)   
 [Delete メソッドの例 (VC + +)](../../../ado/reference/ado-api/delete-method-example-vc.md)   
 [Delete メソッド (ADO Fields コレクション)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete メソッド (ADO Parameters コレクション)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [DeleteRecord メソッド (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
