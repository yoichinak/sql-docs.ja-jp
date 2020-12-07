---
description: CancelBatch メソッド (ADO)
title: CancelBatch メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_CancelBatch
- Recordset15::CancelBatch
helpviewer_keywords:
- CancelBatch method [ADO]
ms.assetid: dbdc2574-e44e-4d95-b03d-4a5d9e9adf3c
author: rothja
ms.author: jroth
ms.openlocfilehash: 0baf8d291bbb45961163dfc80106724c48d71613
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975583"
---
# <a name="cancelbatch-method-ado"></a>CancelBatch メソッド (ADO)
保留中のバッチ更新をキャンセルします。  
  
## <a name="syntax"></a>構文  
  
```  
  
recordset.CancelBatchAffectRecords  
```  
  
#### <a name="parameters"></a>パラメーター  
 *AffectRecords*  
 省略可能。 **CancelBatch**メソッドが影響するレコードの数を示す[AffectEnum](./affectenum.md)値。  
  
## <a name="remarks"></a>解説  
 バッチ更新モードで[レコードセット](./recordset-object-ado.md)内の保留中の更新を取り消すには、 **CancelBatch**メソッドを使用します。 **レコードセット**が即時更新モードである場合、 **AdCancelBatch**が**current**を指定せずにを呼び出すと、エラーが生成されます。  
  
 現在のレコードを編集している場合、または **CancelBatch**を呼び出したときに新しいレコードを追加している場合、ADO は最初に [CancelUpdate](./cancelupdate-method-ado.md) メソッドを呼び出して、キャッシュされた変更を取り消します。 その後、 **レコードセット** 内のすべての保留中の変更が取り消されます。  
  
 **CancelBatch**呼び出しの後に現在のレコードがわからないされている可能性があります。特に、新しいレコードを追加するプロセスを実行していた場合に発生します。 このため、 **CancelBatch**の呼び出し後に、レコード**セット**内の既知の場所に現在のレコードの位置を設定することは賢明です。 たとえば、 [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md) メソッドを呼び出します。  
  
 基になるデータと競合しているために保留中の更新をキャンセルしようとした場合 (たとえば、別のユーザーによってレコードが削除された場合)、プロバイダは [Errors](./errors-collection-ado.md) コレクションに警告を返しますが、プログラムの実行を停止することはありません。 実行時エラーは、要求されたすべてのレコードに競合がある場合にのみ発生します。 [フィルター](./filter-property.md)プロパティ (**AdFilterAffectedRecords**) と[Status](./status-property-ado-recordset.md)プロパティを使用して、競合しているレコードを検索します。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [UpdateBatch および CancelBatch メソッドの例 (VB)](./updatebatch-and-cancelbatch-methods-example-vb.md)   
 [UpdateBatch および CancelBatch メソッドの例 (VC + +)](./updatebatch-and-cancelbatch-methods-example-vc.md)   
 [Cancel メソッド (ADO)](./cancel-method-ado.md)   
 [Cancel メソッド (RDS)](../rds-api/cancel-method-rds.md)   
 [CancelUpdate メソッド (ADO)](./cancelupdate-method-ado.md)   
 [CancelUpdate メソッド (RDS)](../rds-api/cancelupdate-method-rds.md)   
 [Clear メソッド (ADO)](./clear-method-ado.md)   
 [LockType プロパティ (ADO)](./locktype-property-ado.md)   
 [UpdateBatch メソッド](./updatebatch-method.md)