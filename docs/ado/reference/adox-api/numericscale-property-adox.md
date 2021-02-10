---
description: NumericScale プロパティ (ADOX)
title: NumericScale プロパティ (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- _Column::PutNumericScale
- _Column::GetNumericScale
- _Column::NumericScale
- _Column::put_NumericScale
- _Column::get_NumericScale
helpviewer_keywords:
- NumericScale property [ADOX]
ms.assetid: 573ee5d1-57c7-4a27-be79-a0e12944ad9b
author: rothja
ms.author: jroth
ms.openlocfilehash: 8dbf66f202a051740e7d3237f7b52a1fda03b77a
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100053988"
---
# <a name="numericscale-property-adox"></a>NumericScale プロパティ (ADOX)
列の数値の小数点以下桁数を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 [Type](./type-property-column-adox.md)プロパティが **Adnumeric** または **adDecimal** の場合に、列のデータ値の小数点以下桁数を示す **バイト** 値を設定して返します。 他のすべてのデータ型では、 **Numericscale** は無視されます。  
  
## <a name="remarks"></a>解説  
 既定値は 0 です。  
  
 既にコレクションに追加されている [列](./column-object-adox.md)オブジェクトの **numericscale** は読み取り専用です。  
  
## <a name="applies-to"></a>適用対象  
 [Column オブジェクト (ADOX)](./column-object-adox.md)  
  
## <a name="see-also"></a>参照  
 [ADOX のコード例: NumericScale および Precision プロパティの例 (VB)](./adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Type プロパティ (列) (ADOX)](./type-property-column-adox.md)