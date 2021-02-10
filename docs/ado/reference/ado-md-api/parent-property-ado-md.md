---
description: Parent プロパティ (ADO MD)
title: Parent プロパティ (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Parent
- Member::Parent
helpviewer_keywords:
- Parent property [ADO MD]
ms.assetid: 32c278c1-d8e1-4bb7-9ecd-2fbfdffee34b
author: rothja
ms.author: jroth
ms.openlocfilehash: 0674b3455611e8700e8859d4ced5d4052c51135c
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100050953"
---
# <a name="parent-property-ado-md"></a>Parent プロパティ (ADO MD)
階層内の現在の [メンバー](./member-object-ado-md.md) の親であるメンバーを示します。  
  
## <a name="return-values"></a>戻り値  
 [メンバー](./member-object-ado-md.md)オブジェクトを返し、読み取り専用です。  
  
## <a name="remarks"></a>解説  
 階層の最上位レベル (ルート) にあるメンバーには親がありません。 このプロパティは、 [Level](./level-object-ado-md.md)オブジェクトに属する **メンバー** オブジェクトでのみサポートされます。 このプロパティが、 [Position](./position-object-ado-md.md)オブジェクトに属する **メンバー** オブジェクトから参照されている場合に、エラーが発生します。  
  
## <a name="applies-to"></a>適用対象  
 [Member オブジェクト (ADO MD)](./member-object-ado-md.md)  
  
## <a name="see-also"></a>参照  
 [Children プロパティ (ADO MD)](./children-property-ado-md.md)