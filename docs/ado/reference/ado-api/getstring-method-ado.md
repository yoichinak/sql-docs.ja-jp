---
description: GetString メソッド (ADO)
title: GetString メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::raw_GetString
- Recordset20::GetString
helpviewer_keywords:
- GetString method [ADO]
ms.assetid: 92452940-b2a7-456e-94fc-3780c71da33c
author: rothja
ms.author: jroth
ms.openlocfilehash: 15a3ffc6252f1caf56ea1d47006cb84d7f3df201
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990863"
---
# <a name="getstring-method-ado"></a>GetString メソッド (ADO)
[レコードセット](./recordset-object-ado.md)を文字列として返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Variant = recordset.GetString(StringFormat, NumRows, ColumnDelimiter, RowDelimiter, NullExpr)  
```  
  
## <a name="return-value"></a>戻り値  
 **レコードセット**を文字列値**バリアント**(BSTR) として返します。  
  
#### <a name="parameters"></a>パラメーター  
 *StringFormat*  
 **レコードセット**を文字列に変換する方法を指定する[stringformatenum](./stringformatenum.md)値。 *Rowdelimiter*、 *Columndelimiter*、 *nullexpr*の各パラメーターは、 **adclipstring**の*StringFormat*でのみ使用されます。  
  
 *NumRows*  
 省略可能。 **レコードセット**内で変換される行の数。 *Numrows*が指定されていない場合、または**レコードセット**内の行の合計数よりも大きい場合は、**レコードセット**内のすべての行が変換されます。  
  
 *[列区切り記号]*  
 省略可能。 指定されている場合は列の間で使用される区切り記号。それ以外の場合はタブ文字。  
  
 *[RowDelimiter]*  
 省略可能。 指定されている場合は、行の間で使用される区切り記号。それ以外の場合は復帰文字。  
  
 *NullExpr*  
 省略可能。 Null 値の代わりに使用される式 (指定されている場合)。それ以外の場合は空の文字列。  
  
## <a name="remarks"></a>解説  
 行データは文字列に保存されますが、スキーマデータは保存されません。 このため、この文字列を使用して **レコードセット** を再度開くことはできません。  
  
 このメソッドは、RDO **Getclipstring** メソッドに相当します。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [GetString メソッドの例 (VB)](./getstring-method-example-vb.md)