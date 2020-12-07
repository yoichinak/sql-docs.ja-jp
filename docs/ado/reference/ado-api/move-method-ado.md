---
description: Move メソッド (ADO)
title: Move メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Move
- Recordset15::raw_Move
helpviewer_keywords:
- Move method [ADO]
ms.assetid: 13fe9381-d00b-4f4a-9162-83c3f21b3837
author: rothja
ms.author: jroth
ms.openlocfilehash: 6b394d64a9d1b1f403137e9875db83fdd82c2ac1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990593"
---
# <a name="move-method-ado"></a>Move メソッド (ADO)
[レコードセット](./recordset-object-ado.md)オブジェクト内の現在のレコードの位置を移動します。  
  
## <a name="syntax"></a>構文  
  
```  
  
recordset.Move NumRecords, Start  
```  
  
#### <a name="parameters"></a>パラメーター  
 *NumRecords*  
 現在のレコード位置が移動するレコードの数を指定する、符号付き **Long** 式。  
  
 *Start*  
 省略可能。 ブックマークに評価される **文字列** 値または **バリアント** 。 [BookmarkEnum](./bookmarkenum.md)値を使用することもできます。  
  
## <a name="remarks"></a>解説  
 **Move**メソッドは、すべての**レコードセット**オブジェクトでサポートされています。  
  
 *NumRecords*引数が0より大きい場合、現在のレコードの位置は (**レコードセット**の末尾に向かって) 前方に移動します。 *NumRecords*が0未満の場合、現在のレコードの位置は後方 (**レコードセット**の先頭に向かって) に移動します。  
  
 **移動**呼び出しによって、現在のレコード位置が最初のレコードの前のポイントに移動された場合、ADO では、レコードセット内の最初のレコード ([BOF](./bof-eof-properties-ado.md)が**True**) の前の位置に現在のレコードが設定されます。 **BOF**プロパティが既に**True**の場合に後方に移動しようとすると、エラーが生成されます。  
  
 **移動**呼び出しによって、現在のレコード位置が最後のレコードの後のポイントに移動された場合、ADO は現在のレコードをレコードセットの最後のレコード ([EOF](./bof-eof-properties-ado.md)が**True**) の後の位置に設定します。 **EOF**プロパティが既に**True**になっているときに先に進むと、エラーが発生します。  
  
 空の**レコードセット**オブジェクトから**Move**メソッドを呼び出すと、エラーが生成されます。  
  
 Start 引数を渡すと、**レコードセット**オブジェクトがブックマークをサポートしていると仮定した場合、このブックマークを持つレコードに対する移動が*実行*されます。 指定しない場合、移動は現在のレコードを基準にして行われます。  
  
 プロバイダーからローカルにレコードをキャッシュするために [CacheSize](./cachesize-property-ado.md) プロパティを使用している場合は、現在のレコードの位置をキャッシュされたレコードの現在のグループの外側に移動する *NumRecords* 引数を渡すと、変換先レコードから始まる新しいレコードのグループが ADO によって強制的に取得されます。 **CacheSize**プロパティは、新しく取得したグループのサイズを決定し、宛先レコードは最初に取得されたレコードになります。  
  
 **Recordset**オブジェクトが順方向専用の場合でも、出力先がキャッシュされたレコードの現在のセット内にある場合、ユーザーは*NumRecords*引数を0未満に渡すことができます。 **移動**呼び出しによって、最初にキャッシュされたレコードの前のレコードに現在のレコード位置が移動された場合は、エラーが発生します。 そのため、前方スクロールのみをサポートするプロバイダーに対するフルスクロールをサポートするレコードキャッシュを使用できます。 キャッシュされたレコードはメモリに読み込まれるため、必要以上に多くのレコードをキャッシュしないようにしてください。 前方参照専用の**レコードセット**オブジェクトがこのように後方移動をサポートしている場合でも、前方参照専用の**レコードセット**オブジェクトに対して[MovePrevious](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)メソッドを呼び出すとエラーが発生します。  
  
> [!NOTE]
>  前方参照専用 **レコードセット** での後方移動のサポートは、プロバイダーによっては予測できません。 現在のレコードが **レコードセット**内の最後のレコードの後に配置されている場合は、後方に **移動** すると、正しい現在位置が得られないことがあります。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Move メソッドの例 (VB)](./move-method-example-vb.md)   
 [Move メソッドの例 (VBScript)](./move-method-example-vbscript.md)   
 [Move メソッドの例 (VC + +)](./move-method-example-vc.md)   
 [MoveFirst、MoveLast、MoveNext、および MovePrevious メソッド (ADO)](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst、MoveLast、MoveNext、および MovePrevious メソッド (RDS)](../rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord メソッド (ADO)](./moverecord-method-ado.md)