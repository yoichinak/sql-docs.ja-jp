---
description: DefinedSize プロパティ
title: 未定義サイズプロパティ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::DefinedSize
helpviewer_keywords:
- DefinedSize property [ADO]
ms.assetid: 3ee27314-a305-4fbc-8433-9ee9a909afd6
author: rothja
ms.author: jroth
ms.openlocfilehash: 35330c6cae4a3450d4a970edddf360296ce33148
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974153"
---
# <a name="definedsize-property"></a>DefinedSize プロパティ
[フィールド](../../../ado/reference/ado-api/field-object.md)オブジェクトのデータ容量を示します。  
  
## <a name="return-value"></a>戻り値  
 フィールドオブジェクトのデータ型に応じて、定義されたフィールドのサイズを反映する **Long 型** の値を返します。詳細については、「 [型](../../../ado/reference/ado-api/type-property-ado.md) 」を参照してください。 固定長データ型を使用するフィールドの場合、戻り値はデータ型のサイズ (バイト単位) になります。 可変長データ型を使用するフィールドの場合は、次のいずれかになります。  
  
1.  フィールドの最大長 ( **adVarChar** と **adVarWChar**の場合)、またはフィールドに長さが定義されている場合は、バイト単位 ( **AdVarBinary**の場合は、 **adVarNumeric**の場合)。 たとえば、 **adVarChar (5)** フィールドの最大長は5です。  
  
2.  フィールドに長さが定義されていない場合、データ型の最大長 ( **Adchar** と **adchar**の場合) またはバイト単位 ( **adchar** と **adchar**の場合)。  
  
3.  ~ 0 (ビットごとの、値が0ではありません。すべてのビットが1に設定されています)、フィールドとデータ型のどちらも定義された最大長を持っていません。  
  
4.  長さが指定されていないデータ型の場合、これは ~ 0 (ビットごとの、値が0ではなく、すべてのビットが1に設定されます) に設定されます。  
  
## <a name="remarks"></a>解説  
 フィールドオブジェクトのデータ容量を確認するには、 **"** 定義済み**サイズ**" プロパティを使用します。  
  
 [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md)プロパティの値**は、それぞれ異なります。** たとえば、 **adVarChar**という宣言された型を持つ**Field**オブジェクトと、1つの文字を含む定義済みの**size**プロパティ値50を考えてみます。 返される **ActualSize** プロパティ値は、1文字の長さ (バイト単位) です。  
  
## <a name="applies-to"></a>適用対象  
 [Field オブジェクト](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>参照  
 [ActualSize とのサイズプロパティの例 (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize とのサイズプロパティの例 (VC + +)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [ActualSize プロパティ (ADO)](../../../ado/reference/ado-api/actualsize-property-ado.md)
