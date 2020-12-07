---
description: DrilledDown プロパティ (ADO MD)
title: Drilの Down プロパティ (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DrilledDown
- Member::DrilledDown
helpviewer_keywords:
- DrilledDown property [ADO MD]
ms.assetid: bf39dd36-fc7a-4f6e-86c0-fa71430c0d86
author: rothja
ms.author: jroth
ms.openlocfilehash: 3e20e911eefabdf086c805d8b6cbaa87ea7b76b5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986733"
---
# <a name="drilleddown-property-ado-md"></a>DrilledDown プロパティ (ADO MD)
子が軸上の [メンバー](./member-object-ado-md.md) の直後にあるかどうかを示します。  
  
## <a name="return-values"></a>戻り値  
 **ブール**値を返し、読み取り専用です。 **Drilleddown** は、現在のメンバーの子メンバーが軸に存在しない場合に **True** を返します。 現在のメンバーが軸上に1つ以上の子メンバーを持っている場合、 **Drilleddown**は**False**を返します。  
  
## <a name="remarks"></a>解説  
 このメンバーの直後にある軸にこのメンバーの子が少なくとも1つあるかどうかを確認するには、 **Drilの下** のプロパティを使用します。 この情報は、メンバーを表示するときに役立ちます。  
  
 このプロパティは、 [Position](./position-object-ado-md.md)オブジェクトに属する[メンバー](./member-object-ado-md.md)オブジェクトでのみサポートされます。 このプロパティが[Level](./level-object-ado-md.md)オブジェクトに属している**メンバー**オブジェクトから参照されている場合に、エラーが発生します。  
  
## <a name="applies-to"></a>適用対象  
 [Member オブジェクト (ADO MD)](./member-object-ado-md.md)  
  
## <a name="see-also"></a>参照  
 [ParentSameAsPrev プロパティ (ADO MD)](./parentsameasprev-property-ado-md.md)