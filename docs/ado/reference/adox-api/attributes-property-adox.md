---
description: Attributes プロパティ (ADOX)
title: Attributes プロパティ (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- _Column::put_Attributes
- _Column::Attributes
- _Column::PutAttributes
- _Column::get_Attributes
- _Column::GetAttributes
helpviewer_keywords:
- Attributes property [ADOX]
ms.assetid: e3abb359-79a3-4c22-b3a8-2900817e0d23
author: rothja
ms.author: jroth
ms.openlocfilehash: fd868bc3b2fba2f59a4fa75abc2b2865fe1dd41d
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99169553"
---
# <a name="attributes-property-adox"></a>Attributes プロパティ (ADOX)
列の特性について説明します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 **Long 型** の値を設定または返します。 値は、 [Column](./column-object-adox.md) オブジェクトによって表されるテーブルの特性を指定します。 この値には、 [Columnsystem.enum 列挙](./columnattributesenum.md) 定数の組み合わせを指定できます。 既定値はゼロ (**0**) です。これは、 **Adcolfixed** でも **adcolfixed** でもありません。  
  
## <a name="applies-to"></a>適用対象  
  
- [Column オブジェクト (ADOX)](./column-object-adox.md)  
  
## <a name="see-also"></a>参照  
 [Attributes プロパティの例 (VB)](./attributes-property-example-vb.md)