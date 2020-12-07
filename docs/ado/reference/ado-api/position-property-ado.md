---
description: Position プロパティ (ADO)
title: Position プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Position
helpviewer_keywords:
- Position property [ADO]
ms.assetid: daa8319a-49aa-4c1c-9af6-0b01e9ab2f9d
author: rothja
ms.author: jroth
ms.openlocfilehash: 55ae275db06b8b0c73598977e78954bac0fd22be
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990063"
---
# <a name="position-property-ado"></a>Position プロパティ (ADO)
[ストリーム](./stream-object-ado.md)オブジェクト内の現在の位置を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 ストリームの先頭からの現在位置のオフセットをバイト数で指定する **Long 型** の値を設定または返します。 既定値は0で、ストリームの最初のバイトを表します。  
  
## <a name="remarks"></a>解説  
 現在の位置は、ストリームの末尾の後の点に移動できます。 ストリームの末尾を越えて現在位置を指定すると、**ストリーム**オブジェクトの[サイズ](./size-property-ado-stream.md)がそれに応じて大きくなります。 この方法で追加された新しいバイトは null になります。  
  
> [!NOTE]
>  **Position** は常にバイトを測定します。 マルチバイト文字セットを使用したテキストストリームの場合、文字数を決定するために文字サイズで位置を乗算します。 たとえば、2バイト文字セットの場合、最初の文字は0の位置、2番目の文字の位置は2、3番目の文字は4の位置になります。  
  
> [!NOTE]
>  負の値を使用して、 **ストリーム**内の現在位置を変更することはできません。 **位置**には正の数値のみ使用できます。  
  
> [!NOTE]
>  読み取り専用の**ストリーム**オブジェクトの場合、**位置**が**ストリーム**の**サイズ**より大きい値に設定されていると、ADO はエラーを返しません。 **ストリーム**のサイズを変更したり、**ストリーム**の内容を変更したりすることはできません。 ただし、これは無意味な **位置**の値になるため、回避する必要があります。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Charset プロパティ (ADO)](./charset-property-ado.md)