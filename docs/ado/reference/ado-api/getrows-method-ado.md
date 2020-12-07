---
description: GetRows メソッド (ADO)
title: GetRows メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::GetRows
- Recordset15::raw_GetRows
helpviewer_keywords:
- Getrows method [ADO]
ms.assetid: 14b92860-4171-47d9-a413-dd60dd6a8880
author: rothja
ms.author: jroth
ms.openlocfilehash: 666eabf1a375c6a86826bc94600846bd10a0ecfe
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990913"
---
# <a name="getrows-method-ado"></a>GetRows メソッド (ADO)
[レコードセット](./recordset-object-ado.md)オブジェクトの複数のレコードを配列に取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
array = recordset.GetRows(Rows, Start, Fields )  
```  
  
## <a name="return-value"></a>戻り値  
 値が2次元配列である **バリアント** を返します。  
  
#### <a name="parameters"></a>パラメーター  
 *行数*  
 省略可能。 取得するレコードの数を示す [GetRowsOptionEnum](./getrowsoptionenum.md) 値です。 既定値は **adGetRowsRest**です。  
  
 *Start*  
 省略可能。 **GetRows**操作の開始位置となるレコードのブックマークに評価される**文字列**値または**バリアント**。 [BookmarkEnum](./bookmarkenum.md)値を使用することもできます。  
  
 *フィールド*  
 省略可能。 1つのフィールド名または序数位置、またはフィールド名または序数位置の配列を表す **バリアント** 。 ADO は、これらのフィールド内のデータのみを返します。  
  
## <a name="remarks"></a>解説  
 **GetRows**メソッドを使用して、レコード**セット**から2次元配列にレコードをコピーします。 最初の添字はフィールドを識別し、2番目のインデックスはレコード番号を識別します。 **GetRows**メソッドがデータを返すと、*配列*変数は自動的に正しいサイズに設定されます。  
  
 *Rows*引数の値を指定しない場合、 **GetRows**メソッドは**Recordset**オブジェクト内のすべてのレコードを自動的に取得します。 使用可能な数より多くのレコードを要求した場合、 **GetRows** は使用できるレコードの数のみを返します。  
  
 レコード**セット**オブジェクトがブックマークをサポートしている場合は、 **GetRows**メソッドが*開始*引数でそのレコードの[Bookmark](./bookmark-property-ado.md)プロパティの値を渡すことによって、データの取得を開始するレコードを指定できます。  
  
 **GetRows**呼び出しによって返されるフィールドを制限する場合*は、フィールド引数に*1 つのフィールド名と数値、またはフィールド名/数値の配列を渡すことができます。  
  
 **GetRows**を呼び出した後、次に未読のレコードが現在のレコードになります。レコードがなくなった場合は、 [EOF](./bof-eof-properties-ado.md)プロパティが**True**に設定されます。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [GetRows メソッドの例 (VB)](./getrows-method-example-vb.md)   
 [GetRows メソッドの例 (VC++)](./getrows-method-example-vc.md)