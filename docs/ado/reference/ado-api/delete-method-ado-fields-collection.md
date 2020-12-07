---
description: Delete メソッド (ADO Fields コレクション)
title: Delete メソッド (ADO Fields コレクション) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Fields20::Delete
- Fields20::raw_Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 25bedc25-c51c-4cab-96ce-930b959965d9
author: rothja
ms.author: jroth
ms.openlocfilehash: 11499e3483af13ce5fc9edea8fd69694d36be9c7
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974133"
---
# <a name="delete-method-ado-fields-collection"></a>Delete メソッド (ADO Fields コレクション)
[フィールド](../../../ado/reference/ado-api/fields-collection-ado.md)コレクションからオブジェクトを削除します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Fields.Delete Field  
```  
  
#### <a name="parameters"></a>パラメーター  
 *フィールド*  
 削除する[フィールド](../../../ado/reference/ado-api/field-object.md)オブジェクトを指定する**バリアント**です。 このパラメーターには、 **フィールド** オブジェクトの名前、または **フィールド** オブジェクト自体の序数位置を指定できます。  
  
## <a name="remarks"></a>解説  
 開いている[レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md)で**Fields. Delete**メソッドを呼び出すと、実行時エラーが発生します。  
  
## <a name="applies-to"></a>適用対象  
 [Fields コレクション (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
  
## <a name="see-also"></a>参照  
 [Delete メソッド (ADO Parameters コレクション)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete メソッド (ADO Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord メソッド (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
