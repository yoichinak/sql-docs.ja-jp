---
description: Requery メソッド
title: Requery メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Recordset15::Requery
- Recordset15::raw_Requery
helpviewer_keywords:
- Requery method [ADO]
ms.assetid: d81ab76f-1aa8-4ccf-92ec-b65254dc3ea1
author: rothja
ms.author: jroth
ms.openlocfilehash: 21056d0e8f8e488bc5b80541ea4c397b3340c453
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99166659"
---
# <a name="requery-method"></a>Requery メソッド
オブジェクトの基になっているクエリを再実行することによって、 [レコードセット](./recordset-object-ado.md) オブジェクトのデータを更新します。  
  
## <a name="syntax"></a>構文  
  
```  
  
recordset.Requery Options  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Options*  
 任意。 この操作に影響を与える [Executeoptionenum](./executeoptionenum.md) 値および [commandtypeenum](./commandtypeenum.md) 値を含むビットマスク。  
  
> [!NOTE]
>  *オプション* が **adasyncexecute** に設定されている場合、この操作は非同期に実行され、終了時に [RecordsetChangeComplete](./willchangerecordset-and-recordsetchangecomplete-events-ado.md)イベントが発行されます。 **AdExecuteNoRecords** または **AdExecuteStream** の **executeopenenum** 値は、 **Requery** と共に使用することはできません。  
  
## <a name="remarks"></a>コメント  
 **Requery** メソッドを使用して、元のコマンドを再実行し、データをもう一度取得して、データソースから **レコードセット** オブジェクトの内容全体を更新します。 このメソッドを呼び出すことは、 [Close](./close-method-ado.md) メソッドと [Open](./open-method-ado-recordset.md) メソッドを連続して呼び出すことと同じです。 現在のレコードを編集している場合、または新しいレコードを追加している場合は、エラーが発生します。  
  
 **Recordset** オブジェクトが開いている間、カーソルの性質を定義するプロパティ ([CursorType](./cursortype-property-ado.md)、 [LockType](./locktype-property-ado.md)、 [MaxRecords](./maxrecords-property-ado.md)など) は読み取り専用です。 したがって、 **Requery** メソッドで更新できるのは現在のカーソルだけです。 カーソルのプロパティを変更して結果を表示するには、 [Close](./close-method-ado.md) メソッドを使用して、プロパティが再度読み取り/書き込み可能になるようにする必要があります。 その後、プロパティの設定を変更し、 [Open](./open-method-ado-recordset.md) メソッドを呼び出してカーソルを再び開くことができます。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Execute、Requery、および Clear メソッドの例 (VB)](./execute-requery-and-clear-methods-example-vb.md)   
 [Execute、Requery、および Clear メソッドの例 (VBScript)](./execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute、Requery、および Clear メソッドの例 (VC + +)](./execute-requery-and-clear-methods-example-vc.md)   
 [CommandText プロパティ (ADO)](./commandtext-property-ado.md)