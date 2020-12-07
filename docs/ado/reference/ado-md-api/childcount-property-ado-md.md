---
description: ChildCount プロパティ (ADO MD)
title: ChildCount プロパティ (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ChildCount
- Member::ChildCount
helpviewer_keywords:
- ChildCount property [ADO MD]
ms.assetid: 5463be22-ca50-43ea-9c92-468fc8eda280
author: rothja
ms.author: jroth
ms.openlocfilehash: a5c3668a115de8137cd96f489f3e11483cb50045
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987133"
---
# <a name="childcount-property-ado-md"></a>ChildCount プロパティ (ADO MD)
現在の [メンバー](./member-object-ado-md.md) オブジェクトが階層内の親であるメンバーの数を示します。  
  
## <a name="return-values"></a>戻り値  
 **長**整数を返し、読み取り専用です。  
  
## <a name="remarks"></a>解説  
 **Childcount**プロパティを使用して、**メンバー**が持つ子の数の推定値を返します。 **メンバー**の実際の子は、 [children](./children-property-ado-md.md)プロパティで返すことができます。  
  
 [Position](./position-object-ado-md.md)オブジェクトの**メンバー**オブジェクトの場合、返される最大値は65536です。 実際の子の数が65536を超えた場合、返される値は依然として65536になります。 このため、アプリケーションで65536は、 **Childcount** が65536の子以上であることを解釈する必要があります。  
  
 [Level](./level-object-ado-md.md)オブジェクトの**メンバー**オブジェクトの場合は、 **Children**コレクションの ADO collection [Count](../ado-api/count-property-ado.md)プロパティを使用して、子の正確な数を決定します。 コレクション内の子の数が多い場合、子の正確な数を判断するには時間がかかることがあります。  
  
## <a name="applies-to"></a>適用対象  
 [Member オブジェクト (ADO MD)](./member-object-ado-md.md)  
  
## <a name="see-also"></a>参照  
 [Children プロパティ (ADO MD)](./children-property-ado-md.md)   
 [Count プロパティ (ADO)](../ado-api/count-property-ado.md)   
 [Members コレクション (ADO MD)](./members-collection-ado-md.md)