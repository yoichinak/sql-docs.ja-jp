---
description: SortOrder プロパティ (ADOX)
title: 順序のプロパティ (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- _Column::SortOrder
- _Column::PutSortOrder
- _Column::put_SortOrder
- _Column::get_SortOrder
- _Column::GetSortOrder
helpviewer_keywords:
- SortOrder property [ADOX]
ms.assetid: 04510b19-9cb2-4895-b23b-f7790123eb04
author: rothja
ms.author: jroth
ms.openlocfilehash: 939630bea7346d1c4602fb04a6d9ed21a7b3fef7
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100053513"
---
# <a name="sortorder-property-adox"></a>SortOrder プロパティ (ADOX)
列の並べ替え順序を示します (インデックス列のみ)。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 は、 [Sortorderenum](./sortorderenum.md)定数のいずれかを指定できる **Long 型** の値を設定して返します。 既定値は **adSortAscending** です。  
  
## <a name="remarks"></a>解説  
 このプロパティは、[インデックス](./index-object-adox.md)の[Columns](./columns-collection-adox.md)コレクション内の[Column](./column-object-adox.md)オブジェクトにのみ適用されます。  
  
## <a name="applies-to"></a>適用対象  
 [Column オブジェクト (ADOX)](./column-object-adox.md)  
  
## <a name="see-also"></a>参照  
 [順序のプロパティの例 (VB)](./sortorder-property-example-vb.md)   
 [Columns コレクション (ADOX)](./columns-collection-adox.md)   
 [Index オブジェクト (ADOX)](./index-object-adox.md)