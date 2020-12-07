---
description: RelatedColumn プロパティ (ADOX)
title: "\"関連性列\" プロパティ (ADOX) |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::GetRelatedColumn
- _Column::PutRelatedColumn
- _Column::RelatedColumn
- _Column::put_RelatedColumn
- _Column::get_RelatedColumn
helpviewer_keywords:
- RelatedColumn property [ADOX]
ms.assetid: 2f2ca019-c785-4c08-beb1-3a2d3b47823e
author: rothja
ms.author: jroth
ms.openlocfilehash: ce854ad82338bd6aee43b85b98abfea5adb64646
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983443"
---
# <a name="relatedcolumn-property-adox"></a>RelatedColumn プロパティ (ADOX)
関連するテーブル内の関連する [列オブジェクト (ADOX)](./column-object-adox.md) の名前を示します (キー列のみ)。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 関連するテーブル内の関連する列の名前を表す **文字列** 値を設定して返します。  
  
## <a name="remarks"></a>解説  
 既定値は空の文字列 ("") です。  
  
 このプロパティは、既にコレクションに追加されている [列](./column-object-adox.md) オブジェクトに対しては読み取り専用です。  
  
## <a name="applies-to"></a>適用対象  
 [Column オブジェクト (ADOX)](./column-object-adox.md)  
  
## <a name="see-also"></a>参照  
 [Keys Append メソッド、Key Type、UpdateRule プロパティの例 (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Key オブジェクト (ADOX)](./key-object-adox.md)