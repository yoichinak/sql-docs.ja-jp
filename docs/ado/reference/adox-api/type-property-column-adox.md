---
description: Type プロパティ (列) (ADOX)
title: Type プロパティ (列) (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- _Column::Type
- _Column::GetType
- _Column::get_Type
- _Column::put_Type
- _Column::PutType
helpviewer_keywords:
- Type property [ADOX]
ms.assetid: 5c6718b6-f728-478a-8afb-5d17b0a91d1f
author: rothja
ms.author: jroth
ms.openlocfilehash: 520087ef5d1afc2024fa5b64fc259cd8ef35439a
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100053463"
---
# <a name="type-property-column-adox"></a>Type プロパティ (列) (ADOX)
列のデータ型を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 [DataTypeEnum](../ado-api/datatypeenum.md)定数のいずれかを指定できる **Long 型** の値を設定または返します。 既定値は **adVarWChar** です。  
  
## <a name="remarks"></a>解説  
 このプロパティは、 [列](./column-object-adox.md) オブジェクトがコレクションまたは別のオブジェクトに追加されるまで、読み取り/書き込みが行われます。その後、読み取り専用になります。  
  
## <a name="applies-to"></a>適用対象  
 [Column オブジェクト (ADOX)](./column-object-adox.md)  
  
## <a name="see-also"></a>参照  
 [ParentCatalog プロパティの例 (VB)](./parentcatalog-property-example-vb.md)   
 [Type プロパティ (キー) (ADOX)](./type-property-key-adox.md)   
 [Type プロパティ (テーブル) (ADOX)](./type-property-table-adox.md)