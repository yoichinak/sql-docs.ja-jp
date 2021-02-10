---
description: GetString メソッド (ADO)
title: GetString メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Recordset20::raw_GetString
- Recordset20::GetString
helpviewer_keywords:
- GetString method [ADO]
ms.assetid: 92452940-b2a7-456e-94fc-3780c71da33c
author: rothja
ms.author: jroth
ms.openlocfilehash: b1cfaa8b75f7e8d1dfb5fc0cecf7e5d99634960a
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100020815"
---
# <a name="getstring-method-ado"></a>GetString メソッド (ADO)
[レコードセット](./recordset-object-ado.md)を文字列として返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Variant = recordset.GetString(StringFormat, NumRows, ColumnDelimiter, RowDelimiter, NullExpr)  
```  
  
## <a name="return-value"></a>戻り値  
 **レコードセット** を文字列値 **バリアント**(BSTR) として返します。  
  
#### <a name="parameters"></a>パラメーター  
 *StringFormat*  
 **レコードセット** を文字列に変換する方法を指定する [stringformatenum](./stringformatenum.md)値。 *Rowdelimiter*、 *Columndelimiter*、 *nullexpr* の各パラメーターは、 **adclipstring** の *StringFormat* でのみ使用されます。  
  
 *NumRows*  
 任意。 **レコードセット** 内で変換される行の数。 *Numrows* が指定されていない場合、または **レコードセット** 内の行の合計数よりも大きい場合は、**レコードセット** 内のすべての行が変換されます。  
  
 *[列区切り記号]*  
 任意。 指定されている場合は列の間で使用される区切り記号。それ以外の場合はタブ文字。  
  
 *[RowDelimiter]*  
 任意。 指定されている場合は、行の間で使用される区切り記号。それ以外の場合は復帰文字。  
  
 *NullExpr*  
 任意。 Null 値の代わりに使用される式 (指定されている場合)。それ以外の場合は空の文字列。  
  
## <a name="remarks"></a>解説  
 行データは文字列に保存されますが、スキーマデータは保存されません。 このため、この文字列を使用して **レコードセット** を再度開くことはできません。  
  
 このメソッドは、RDO **Getclipstring** メソッドに相当します。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [GetString メソッドの例 (VB)](./getstring-method-example-vb.md)