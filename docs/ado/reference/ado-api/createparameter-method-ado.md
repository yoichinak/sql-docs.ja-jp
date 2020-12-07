---
description: CreateParameter メソッド (ADO)
title: CreateParameter メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::raw_CreateParameter
- Command15::CreateParameter
helpviewer_keywords:
- CreateParameter method [RDS]
ms.assetid: 9666fdcc-0544-4ed7-a97b-c415f2a56d7e
author: rothja
ms.author: jroth
ms.openlocfilehash: 8fd075dff5ae67c7965082a9b7d0f75f5c4d47eb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974483"
---
# <a name="createparameter-method-ado"></a>CreateParameter メソッド (ADO)
指定したプロパティを使用して、新しい [Parameter](./parameter-object.md) オブジェクトを作成します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set parameter = command.CreateParameter (Name, Type, Direction, Size, Value)  
```  
  
## <a name="return-value"></a>戻り値  
 **パラメーター**オブジェクトを返します。  
  
#### <a name="parameters"></a>パラメーター  
 *名前*  
 省略可能。 **パラメーター**オブジェクトの名前を含む**文字列**値です。  
  
 *Type*  
 省略可能。 **Parameter**オブジェクトのデータ型を示す[DataTypeEnum](./datatypeenum.md)値です。  
  
 *方向*  
 省略可能。 **パラメーター**オブジェクトの型を指定する[parameterdirection 列挙](./parameterdirectionenum.md)値。  
  
 *[サイズ]*  
 省略可能。 パラメーター値の最大長を文字数またはバイト数で指定する **Long 型** の値。  
  
 *値*  
 省略可能。 **Parameter**オブジェクトの値を指定する**バリアント**です。  
  
## <a name="remarks"></a>解説  
 **Createparameter**メソッドを使用して、指定した名前、型、方向、サイズ、および値を使用して新しい**パラメーター**オブジェクトを作成します。 引数で渡す値は、対応する **パラメーター** プロパティに書き込まれます。  
  
 このメソッドは、 **Parameter**オブジェクトを[Command](./command-object-ado.md)オブジェクトの**Parameters**コレクションに自動的に追加しません。 これにより、 **パラメーター** オブジェクトをコレクションに追加したときに ADO によって検証される値を持つ追加のプロパティを設定できます。  
  
 *型*引数に可変長データ型を指定する場合は、**パラメーター**コレクションに追加する前に、*サイズ*引数を渡すか、**パラメーター**オブジェクトの[size](./size-property-ado-parameter.md)プロパティを設定する必要があります。それ以外の場合は、エラーが発生します。  
  
 *型*引数に数値データ型 (**Adnumeric**または**adDecimal**) を指定する場合は、 [numericscale](./numericscale-property-ado.md)プロパティと[Precision](./precision-property-ado.md)プロパティも設定する必要があります。  
  
## <a name="applies-to"></a>適用対象  
 [Command オブジェクト (ADO)](./command-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Append および CreateParameter メソッドの例 (VB)](./append-and-createparameter-methods-example-vb.md)   
 [Append および CreateParameter メソッドの例 (VC + +)](./append-and-createparameter-methods-example-vc.md)   
 [Append メソッド (ADO)](./append-method-ado.md)   
 [Parameter オブジェクト](./parameter-object.md)   
 [Parameters コレクション (ADO)](./parameters-collection-ado.md)