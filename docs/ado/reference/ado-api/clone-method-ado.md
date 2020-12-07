---
description: Clone メソッド (ADO)
title: Clone メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::Clone
- Recordset20::raw_Clone
helpviewer_keywords:
- Clone method [ADO]
ms.assetid: ad49265f-1c05-4271-9bbf-7c00010ac18c
author: rothja
ms.author: jroth
ms.openlocfilehash: cc7bab8106ba0d9b023999f80ce77935ae30cc8d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975433"
---
# <a name="clone-method-ado"></a>Clone メソッド (ADO)
既存の**レコード**セットオブジェクトから、重複する[レコードセット](./recordset-object-ado.md)オブジェクトを作成します。 必要に応じて、複製が読み取り専用であることを指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set rstDuplicate = rstOriginal.Clone (LockType)  
```  
  
## <a name="return-value"></a>戻り値  
 **レコードセット**オブジェクト参照を返します。  
  
#### <a name="parameters"></a>パラメーター  
 *rstDuplicate*  
 作成される重複した **レコードセット** オブジェクトを識別するオブジェクト変数です。  
  
 *rstOriginal*  
 複製する **レコードセット** オブジェクトを識別するオブジェクト変数です。  
  
 *LockType*  
 省略可能。 元の**レコードセット**のロックの種類または読み取り専用の**レコードセット**を指定する[locktypeenum](./locktypeenum.md)値。 有効な値は、 **Adlockunspecified** または **adlockunspecified**です。  
  
## <a name="remarks"></a>解説  
 複数の重複したレコード**セット**オブジェクトを作成するには、 **Clone**メソッドを使用します。特に、特定のレコードのセットに複数の現在のレコードを保持する場合に使用します。 **Clone**メソッドを使用する方が、元のと同じ定義を使用する新しい**レコードセット**オブジェクトを作成して開くよりも効率的です。  
  
 元の**レコードセット**(存在する場合) の[Filter](./filter-property.md)プロパティは、複製には適用されません。 新しい**レコードセット**の**filter**プロパティを設定して、結果をフィルター処理します。 既存の **フィルター** 値をコピーする最も簡単な方法は、次のように、それを直接割り当てることです。  
  
```  
rsNew.Filter = rsOriginal.Filter  
```  
  
 新しく作成された複製の現在のレコードは、最初のレコードに設定されます。  
  
 1つの **レコードセット** オブジェクトに対して行った変更は、カーソルの種類に関係なく、すべての複製に表示されます。 ただし、元の**レコードセット**に対して再[クエリ](./requery-method.md)を実行すると、複製は元のレコードと同期されなくなります。  
  
 元の **レコードセット** を閉じると、コピーが閉じられることはなく、コピーを終了しても、元のコピーまたは他のコピーを閉じることはできません。  
  
 複製できるのは、ブックマークをサポートする **レコードセット** オブジェクトだけです。 ブックマーク値は交換可能です。つまり、1つの **レコードセット** オブジェクトからのブックマーク参照は、その複製内の同じレコードを参照します。  
  
 トリガーされる一部の **レコードセット** イベントは、すべての **レコードセット** の複製でも発生します。 ただし、複製されたレコード **セット**間で現在のレコードが異なる場合があるため、そのイベントは複製に対して有効ではない可能性があります。 たとえば、フィールドの値を変更すると、変更された**レコードセット**とすべての複製でが[changefield](./willchangefield-and-fieldchangecomplete-events-ado.md)イベントが発生します。 複製された**レコードセット**(変更が行われていない) の **"** *フィールド*" パラメーターは、複製の現在のレコードのフィールドを参照します。これは、変更が発生した元のレコード**セット**の現在のレコードとは異なるレコードである可能性があります。  
  
 次の表に、すべての **レコードセット** イベントの完全な一覧を示します。 **Clone**メソッドを使用して生成されたレコードセット複製に対して有効でトリガーされるかどうかを示します。  
  
|Event|複製でトリガーされますか?|  
|-----------|--------------------------|  
|[EndOfRecordset](./endofrecordset-event-ado.md)|いいえ|  
|[FetchComplete](./fetchcomplete-event-ado.md)|いいえ|  
|[FetchProgress](./fetchprogress-event-ado.md)|いいえ|  
|[FieldChangeComplete](./willchangefield-and-fieldchangecomplete-events-ado.md)|はい|  
|[MoveComplete](./willmove-and-movecomplete-events-ado.md)|いいえ|  
|[RecordChangeComplete](./willchangerecord-and-recordchangecomplete-events-ado.md)|はい|  
|[RecordsetChangeComplete](./willchangerecordset-and-recordsetchangecomplete-events-ado.md)|いいえ|  
|[Changefield](./willchangefield-and-fieldchangecomplete-events-ado.md)|はい|  
|[Changerecord](./willchangerecord-and-recordchangecomplete-events-ado.md)|はい|  
|[WillChangeRecordset](./willchangerecordset-and-recordsetchangecomplete-events-ado.md)|いいえ|  
|[移動](./willmove-and-movecomplete-events-ado.md)|いいえ|  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Clone メソッドの例 (VB)](./clone-method-example-vb.md)   
 [Clone メソッドの例 (VBScript)](./clone-method-example-vbscript.md)   
 [Clone メソッドの例 (VC++)](./clone-method-example-vc.md)