---
description: Optimize プロパティ - 動的 (ADO)
title: Optimize プロパティ-動的 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Optimize property [ADO]
ms.assetid: a491c4ce-2b04-4c84-be83-3846bde8d16b
author: rothja
ms.author: jroth
ms.openlocfilehash: 3393bbfbfbaeb50c6a608db92dae42bb29fb3b1d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990263"
---
# <a name="optimize-property-dynamic-ado"></a>Optimize プロパティ - 動的 (ADO)
[フィールド](./field-object.md)にインデックスを作成するかどうかを指定します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 インデックスを作成する必要があるかどうかを示す **ブール** 値を設定または返します。  
  
## <a name="remarks"></a>解説  
 インデックスを使用すると、 [レコードセット](./recordset-object-ado.md)内の値を検索したり並べ替えたりする操作のパフォーマンスを向上させることができます。 インデックスは ADO の内部にあります。アプリケーションで明示的にアクセスしたり、使用したりすることはできません。  
  
 フィールドにインデックスを作成するには、 **Optimize** プロパティを **True**に設定します。 インデックスを削除するには、このプロパティを **False**に設定します。  
  
 **[最適化**] は、[[カーソルの場所](./cursorlocation-property-ado.md)] プロパティが**adUseClient**に設定されている場合に、[フィールド](./field-object.md)オブジェクトの[プロパティ](./properties-collection-ado.md)のコレクションに追加される動的プロパティです。  
  
## <a name="usage"></a>使用法  
  
```  
Dim rs As New Recordset  
Dim fld As Field  
rs.CursorLocation = adUseClient      'Enable index creation  
rs.Fields.Append "Field1", adChar, 35, adFldIsNullable  
rs.Open  
Set fld = rs.Fields(0)  
fld.Properties("Optimize") = True    'Create an index  
fld.Properties("Optimize") = False   'Delete an index  
```  
  
## <a name="applies-to"></a>適用対象  
 [Field オブジェクト](./field-object.md)  
  
## <a name="see-also"></a>参照  
 [Optimize プロパティの例 (VB)](./optimize-property-example-vb.md)   
 [Optimize プロパティの例 (VC + +)](./optimize-property-example-vc.md)   
 [Filter プロパティ](./filter-property.md)   
 [Find メソッド (ADO)](./find-method-ado.md)   
 [Sort プロパティ](./sort-property.md)