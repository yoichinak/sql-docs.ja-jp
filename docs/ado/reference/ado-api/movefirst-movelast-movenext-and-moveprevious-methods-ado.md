---
description: MoveFirst、MoveLast、MoveNext、および MovePrevious メソッド (ADO)
title: MoveFirst、MoveLast、MoveNext、および MovePrevious メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MoveLast
- Recordset15::MoveNext
- Recordset15::raw_MoveNext
- Recordset15::raw_MovePrevious
- Recordset15::MoveFirst
- Recordset15::raw_MoveLast
- Recordset15::MovePrevious
- Recordset15::raw_MoveFirst
helpviewer_keywords:
- MoveNext method [ADO]
- MoveLast method [ADO]
- MoveFirst method [ADO]
- MovePrevious method [ADO]
ms.assetid: a61a01a7-5b33-4150-9126-21dfa63654cb
author: rothja
ms.author: jroth
ms.openlocfilehash: dd050c775c706b3cafe2586eed05d93f9079fe27
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990553"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-ado"></a>MoveFirst、MoveLast、MoveNext、および MovePrevious メソッド (ADO)
指定したレコード [セット](./recordset-object-ado.md) オブジェクト内の最初、最後、次、または前のレコードに移動し、そのレコードを現在のレコードにします。  
  
## <a name="syntax"></a>構文  
  
```  
  
recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
## <a name="remarks"></a>解説  
 **MoveFirst**メソッドを使用して、現在のレコードの位置を**レコードセット**内の最初のレコードに移動します。  
  
 現在のレコードの位置を**レコードセット**内の最後のレコードに移動するには、 **MoveLast**メソッドを使用します。 **レコードセット**オブジェクトは、ブックマークまたは後方カーソル移動をサポートしている必要があります。それ以外の場合、メソッドの呼び出しでエラーが発生します。  
  
 **レコードセット**が空のときに**MoveFirst**または**MoveLast**を呼び出すと ( **BOF**と**EOF**の両方が True の場合)、エラーが生成されます。  
  
 **MoveNext**メソッドを使用して、現在のレコードの位置を (**レコードセット**の一番下に) 1 つずつ前方に移動します。 最後のレコードが現在のレコードで、 **MoveNext** メソッドを呼び出すと、ADO は現在のレコードを **レコードセット** 内の最後のレコード ([EOF](./bof-eof-properties-ado.md) が **True**) の後の位置に設定します。 **EOF**プロパティが既に**True**になっているときに先に進むと、エラーが発生します。  
  
 ADO 2.5 以降では、 **レコードセット** がフィルター処理または並べ替えられ、現在のレコードのデータが変更されると、 **MoveNext** メソッドを呼び出すと、カーソルが現在のレコードから前方に2つのレコードに移動します。 これは、現在のレコードが変更されたときに、次のレコードが新しい現在のレコードになるためです。 変更後に **MoveNext** を呼び出して、カーソルを新しい現在のレコードから1つ前のレコードに移動します。 これは、ADO 2.1 以前の動作とは異なります。 これらの以前のバージョンでは、並べ替えまたはフィルター選択されたレコード **セット** 内の現在のレコードのデータを変更しても、現在のレコードの位置は変更されず、 **MoveNext** はカーソルを現在のレコードの直後の次のレコードに移動します。  
  
 **MovePrevious**メソッドを使用して、現在のレコードの位置をレコード**セット**の先頭に向かって後方に移動します。 **レコードセット**オブジェクトは、ブックマークまたは後方カーソル移動をサポートしている必要があります。それ以外の場合、メソッドの呼び出しでエラーが発生します。 最初のレコードが現在のレコードで、 **MovePrevious** メソッドを呼び出すと、ADO によって、レコード **セット** 内の最初のレコード ([BOF](./bof-eof-properties-ado.md) が **True**) の前の位置に現在のレコードが設定されます。 **BOF**プロパティが既に**True**の場合に後方に移動しようとすると、エラーが生成されます。 **Recordset**オブジェクトがブックマークまたは後方カーソルの移動をサポートしていない場合は、 **MovePrevious**メソッドによってエラーが生成されます。  
  
 **レコードセット**が転送のみ可能で、前方スクロールと後方スクロールの両方をサポートする場合は、 [CacheSize](./cachesize-property-ado.md)プロパティを使用して、 [Move](./move-method-ado.md)メソッドを使用した後方カーソルの移動をサポートするレコードキャッシュを作成できます。 キャッシュされたレコードはメモリに読み込まれるため、必要以上に多くのレコードをキャッシュしないようにしてください。 前方参照専用の**レコードセット**オブジェクトでは、 **MoveFirst**メソッドを呼び出すことができます。この操作を行うと、**レコードセット**オブジェクトを生成したコマンドがプロバイダーによって再実行される可能性があります。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [MoveFirst、MoveLast、MoveNext、および MovePrevious メソッドの例 (VB)](./movefirst-movelast-movenext-and-moveprevious-methods-example-vb.md)   
 [MoveFirst、MoveLast、MoveNext、および MovePrevious メソッドの例 (VBScript)](./movefirst-movelast-movenext-and-moveprevious-methods-example-vbscript.md)   
 [MoveFirst、MoveLast、MoveNext、および MovePrevious メソッドの例 (VC + +)](./movefirst-movelast-movenext-and-moveprevious-methods-example-vc.md)   
 [Move メソッド (ADO)](./move-method-ado.md)   
 [MoveFirst、MoveLast、MoveNext、および MovePrevious メソッド (RDS)](../rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord メソッド (ADO)](./moverecord-method-ado.md)