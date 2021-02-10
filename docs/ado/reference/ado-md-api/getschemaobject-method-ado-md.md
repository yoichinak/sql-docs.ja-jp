---
description: GetSchemaObject メソッド (ADO MD)
title: GetSchemaObject メソッド (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- GetSchemaObject
- Cellset::GetSchemaObject
helpviewer_keywords:
- GetSchemaObject method [ADO MD]
ms.assetid: 36b754b4-6b17-4dd1-a925-bca46938b7c4
author: rothja
ms.author: jroth
ms.openlocfilehash: 96b0a2b6b8fc0a8d87c51c68701a64c971255ec8
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100054627"
---
# <a name="getschemaobject-method-ado-md"></a>GetSchemaObject メソッド (ADO MD)
[UniqueName](./uniquename-property-ado-md.md)によって ADO MD スキーマオブジェクト ([ディメンション](./dimension-object-ado-md.md)、[階層](./hierarchy-object-ado-md.md)、[レベル](./level-object-ado-md.md)、または[メンバー](./member-object-ado-md.md)) を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set object = CubeDef.GetSchemaObject (ObjType, UniqueName)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *ObjType*  
 取得するスキーマオブジェクト (ディメンション、階層、レベル、またはメンバー) の種類を指定する [Schemaobjecttypeenum](./schemaobjecttypeenum.md) 値。  
  
 *UniqueName*  
 取得するオブジェクトの **UniqueName** プロパティ値を指定する **文字列**。  
  
## <a name="remarks"></a>解説  
 **Getschemaobject** は、 **UniqueName** プロパティで指定されているように、一意の名前を使用してオブジェクトを取得します。 親オブジェクトの名前を把握しておく必要はありません。また、スキーマオブジェクトを取得するために親コレクションを設定する必要もありません。  
  
## <a name="applies-to"></a>適用対象  
 [CubeDef オブジェクト (ADO MD)](./cubedef-object-ado-md.md)  
  
## <a name="see-also"></a>参照  
 [CubeDef オブジェクト (ADO MD)](./cubedef-object-ado-md.md)