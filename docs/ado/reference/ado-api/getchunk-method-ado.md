---
description: GetChunk メソッド (ADO)
title: GetChunk メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::raw_GetChunk
- Field20::GetChunk
helpviewer_keywords:
- GetChunk method [ADO]
ms.assetid: fc268e22-205b-44a3-9038-ffed51e23e10
author: rothja
ms.author: jroth
ms.openlocfilehash: 196f41f7828be16c7c38b281edb85774569580a1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88972913"
---
# <a name="getchunk-method-ado"></a>GetChunk メソッド (ADO)
大きいテキストまたはバイナリデータ [フィールド](./field-object.md) オブジェクトの内容のすべて、または一部を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
variable = field.GetChunk(Size)  
```  
  
## <a name="return-value"></a>戻り値  
 **バリアント**を返します。  
  
#### <a name="parameters"></a>パラメーター  
 *[サイズ]*  
 取得するバイト数または文字数と同じ **Long 型** の式。  
  
## <a name="remarks"></a>解説  
 **Field**オブジェクトの**GetChunk**メソッドを使用して、その長いバイナリデータまたは文字データの一部またはすべてを取得します。 システムメモリが制限されている場合は、 **GetChunk** メソッドを使用して、全体ではなく、長い値を部分的に操作することができます。  
  
 **GetChunk**呼び出しによって返されるデータは、*変数*に代入されます。 *Size*が残りのデータよりも大きい場合、 **GetChunk**メソッドは、空のスペースを含む*変数*を埋めずに残りのデータだけを返します。 フィールドが空の場合、 **GetChunk** メソッドは null 値を返します。  
  
 後続の各 **getchunk** 呼び出しは、前の **getchunk** 呼び出しが終了した場所からデータを取得します。 ただし、あるフィールドからデータを取得し、現在のレコードの別のフィールドの値を設定または読み取る場合、ADO では最初のフィールドからのデータの取得が完了したと見なされます。 最初のフィールドに対して **getchunk** メソッドを再度呼び出すと、ADO はその呼び出しを新しい **GetChunk** 操作として解釈し、データの先頭からの読み取りを開始します。 最初の**レコードセット**オブジェクトの複製ではない他の[レコードセット](./recordset-object-ado.md)オブジェクトのフィールドにアクセスしても、 **GetChunk**操作が中断されることはありません。  
  
 **Field**オブジェクトの[Attributes](./attributes-property-ado.md)プロパティの**Adfldlong**ビットが**True**に設定されている場合は、そのフィールドに対して**GetChunk**メソッドを使用できます。  
  
 **Field**オブジェクトで**GetChunk**メソッドを使用しているときに現在のレコードが存在しない場合、エラー 3021 (現在のレコードがありません) が発生します。  
  
> [!NOTE]
>  **GetChunk**メソッドは、 [Record](./record-object-ado.md)オブジェクトの**Field**オブジェクトに対しては機能しません。 操作は一切実行されず、実行時エラーが発生します。  
  
## <a name="applies-to"></a>適用対象  
 [Field オブジェクト](./field-object.md)  
  
## <a name="see-also"></a>参照  
 [AppendChunk および GetChunk メソッドの例 (VB)](./appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk および GetChunk メソッドの例 (VC + +)](./appendchunk-and-getchunk-methods-example-vc.md)   
 [AppendChunk メソッド (ADO)](./appendchunk-method-ado.md)   
 [Attributes プロパティ (ADO)](./attributes-property-ado.md)