---
description: Clear メソッド (ADO)
title: Clear メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Errors::raw_Clear
- Errors::Clear
helpviewer_keywords:
- Clear method [ADO]
ms.assetid: 0a61ba7a-20b8-426a-91a0-9040e7c5a98a
author: rothja
ms.author: jroth
ms.openlocfilehash: d78980c1baee5aed1280f69c0d5224622a217ea0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975473"
---
# <a name="clear-method-ado"></a>Clear メソッド (ADO)
[エラーコレクションから](./errors-collection-ado.md)すべての[エラー](./error-object.md)オブジェクトを削除します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>解説  
 コレクションから既存の[エラー](./error-object.md)オブジェクトをすべて削除するには、 [Errors](./errors-collection-ado.md)コレクションに対して**Clear**メソッドを使用します。 エラーが発生すると、ADO によってエラーコレクションが自動的にクリア **され、** 新しいエラーに基づいて **エラー** オブジェクトに格納されます。  
  
 一部のプロパティおよびメソッドは、**エラーコレクションに****エラー**オブジェクトとして表示されるが、プログラムの実行を停止しない警告を返します。 [レコードセット](./recordset-object-ado.md)オブジェクトの[Resync](./resync-method.md)、 [UpdateBatch](./updatebatch-method.md)、または[CancelBatch](./cancelbatch-method-ado.md)メソッドを呼び出す前に、[接続](./connection-object-ado.md)オブジェクトの[Open](./open-method-ado-connection.md)メソッド。または、**レコードセット**オブジェクトの[Filter](./filter-property.md)プロパティを設定し、 **Errors**コレクションに対して**Clear**メソッドを呼び出します。 これにより、 **Errors**コレクションの[Count](./count-property-ado.md)プロパティを読み取って、返された警告をテストできます。  
  
## <a name="applies-to"></a>適用対象  
 [Errors コレクション (ADO)](./errors-collection-ado.md)  
  
## <a name="see-also"></a>参照  
 [Execute、Requery、および Clear メソッドの例 (VB)](./execute-requery-and-clear-methods-example-vb.md)   
 [Execute、Requery、および Clear メソッドの例 (VBScript)](./execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute、Requery、および Clear メソッドの例 (VC + +)](./execute-requery-and-clear-methods-example-vc.md)   
 [CancelBatch メソッド (ADO)](./cancelbatch-method-ado.md)   
 [Delete メソッド (ADO Fields コレクション)](./delete-method-ado-fields-collection.md)   
 [Delete メソッド (ADO Parameters コレクション)](./delete-method-ado-parameters-collection.md)   
 [Delete メソッド (ADO Recordset)](./delete-method-ado-recordset.md)   
 [Filter プロパティ](./filter-property.md)   
 [Resync メソッド](./resync-method.md)   
 [UpdateBatch メソッド](./updatebatch-method.md)