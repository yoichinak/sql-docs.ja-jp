---
description: Index プロパティ
title: Index プロパティ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Recordset21::Index
helpviewer_keywords:
- Index property
ms.assetid: 1c79e271-21ec-41a8-8163-c5e89f0001a7
author: rothja
ms.author: jroth
ms.openlocfilehash: 9e8c346ac48092d7a5dcaf09068bb64d63316a38
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99170954"
---
# <a name="index-property"></a>Index プロパティ
[レコードセット](./recordset-object-ado.md)オブジェクトに現在適用されているインデックスの名前を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 インデックスの名前を設定するか、 **文字列** 値を返します。  
  
## <a name="remarks"></a>コメント  
 **Index** プロパティによって指定されたインデックスは、**レコードセット** オブジェクトの基になるベーステーブルで既に宣言されている必要があります。 つまり、インデックスは、ADOX [index](../adox-api/index-object-adox.md) オブジェクトとして、またはベーステーブルが作成されたときに、プログラムによって宣言されている必要があります。  
  
 インデックスを設定できない場合は、実行時エラーが発生します。 **Index** プロパティは、次の条件下では設定できません。  
  
-   [WillChangeRecordset](./willchangerecordset-and-recordsetchangecomplete-events-ado.md)または **RecordsetChangeComplete** イベントハンドラー内。  
  
-   **レコードセット** がまだ操作を実行している ( [State](./state-property-ado.md)プロパティによって決定できる) 場合はです。  
  
-   [フィルタープロパティを](./filter-property.md)使用して **レコードセット** にフィルターが設定されている場合は。  
  
 **レコード** セットが閉じられていても、**レコード** セットが正常に開かれない場合、または基になるプロバイダーがインデックスをサポートしていない場合にインデックスを使用できない場合は、**インデックス** プロパティをいつでも正常に設定できます。  
  
 インデックスを設定できる場合は、現在の行の位置が変更される可能性があります。 これにより、 [AbsolutePosition](./absoluteposition-property-ado.md)プロパティが更新され、 **WillChangeRecordset**、 **RecordsetChangeComplete**、 [MoveComplete](./willmove-and-movecomplete-events-ado.md) [の各](./willmove-and-movecomplete-events-ado.md)イベントが起動されます。  
  
 インデックスを設定でき、 [LockType](./locktype-property-ado.md) プロパティが **adlockpessimistic** または **adlockpessimistic** の場合、暗黙的な [UpdateBatch](./updatebatch-method.md) 操作が実行されます。 これにより、現在のグループと影響を受けるグループが解放されます。 既存のフィルターがすべて解放され、現在の行の位置が、並べ替えられた **レコードセット** の最初の行に変更されます。  
  
 **Index** プロパティは、 [Seek](./seek-method.md)メソッドと組み合わせて使用されます。 基になるプロバイダーが **Index** プロパティをサポートしていないため、 **Seek** メソッドを使用する場合は、代わりに [Find](./find-method-ado.md) メソッドを使用することを検討してください。 **レコードセット** オブジェクトが [サポート](./supports-method.md)**(adindex)** メソッドを使用したインデックスをサポートしているかどうかを判断します。  
  
 組み込みの **インデックス** プロパティは、動的 [最適化](./optimize-property-dynamic-ado.md) プロパティに関連付けられていませんが、両方ともインデックスを処理します。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Seek メソッドと Index プロパティの例 (VB)](./seek-method-and-index-property-example-vb.md)   
 [Index オブジェクト (ADOX)](../adox-api/index-object-adox.md)   
 [Seek メソッド](./seek-method.md)