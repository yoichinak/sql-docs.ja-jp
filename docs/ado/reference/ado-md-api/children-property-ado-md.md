---
description: Children プロパティ (ADO MD)
title: Children プロパティ (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Member::Children
- Children
helpviewer_keywords:
- Children property [ADO MD]
ms.assetid: 61d36468-1ccd-467a-9cb5-17d0bfacc766
author: rothja
ms.author: jroth
ms.openlocfilehash: 7fae1b50b219abc4e5841bb537d0befaf35a4b3e
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100055676"
---
# <a name="children-property-ado-md"></a>Children プロパティ (ADO MD)
現在の[メンバー](./member-object-ado-md.md)が階層内の親である[メンバー](./members-collection-ado-md.md)コレクションを返します。  
  
## <a name="return-values"></a>戻り値  
 **メンバー** コレクションを返し、読み取り専用です。  
  
## <a name="remarks"></a>解説  
 **Children** プロパティには、現在の **メンバー** が階層構造の親である **Members** コレクションが含まれています。 リーフレベルの **メンバー** オブジェクトには、 **members** コレクションに子メンバーがありません。 このプロパティは、 [Level](./level-object-ado-md.md)オブジェクトに属している **メンバー** オブジェクトでのみサポートされます。 このプロパティが、 [Position](./position-object-ado-md.md)オブジェクトに属する **メンバー** オブジェクトから参照されている場合に、エラーが発生します。  
  
## <a name="applies-to"></a>適用対象  
 [Member オブジェクト (ADO MD)](./member-object-ado-md.md)  
  
## <a name="see-also"></a>参照  
 [ChildCount プロパティ (ADO MD)](./childcount-property-ado-md.md)