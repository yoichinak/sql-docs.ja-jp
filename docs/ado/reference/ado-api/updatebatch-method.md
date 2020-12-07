---
description: UpdateBatch メソッド
title: UpdateBatch メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::UpdateBatch
- Recordset15::raw_UpdateBatch
helpviewer_keywords:
- UpdateBatch method [ADO]
ms.assetid: 23f9314c-b027-4a51-aeae-50caa2977740
author: rothja
ms.author: jroth
ms.openlocfilehash: 648e6f8e64d4001851afb3838c901ab2b1172108
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988003"
---
# <a name="updatebatch-method"></a>UpdateBatch メソッド
すべての保留中のバッチ更新をディスクに書き込みます。  
  
## <a name="syntax"></a>構文  
  
```  
  
recordset.UpdateBatch AffectRecords, PreserveStatus  
```  
  
#### <a name="parameters"></a>パラメーター  
 *AffectRecords*  
 省略可能。 **UpdateBatch**メソッドが影響するレコードの数を示す[AffectEnum](./affectenum.md)値です。  
  
 *PreserveStatus*  
 省略可能。 [Status](./status-property-ado-recordset.md)プロパティによって示されるローカルの変更をコミットする必要があるかどうかを指定する**ブール**値です。 この値が **True**に設定されている場合、更新が完了した後も、各レコードの **Status** プロパティは変更されません。  
  
## <a name="remarks"></a>解説  
 バッチ更新モードで**レコードセット**オブジェクトを変更する場合は、 **UpdateBatch**メソッドを使用して、**レコードセット**オブジェクトに加えられたすべての変更を基になるデータベースに転送します。  
  
 **レコードセット**オブジェクトでバッチ更新がサポートされている場合は、 **UpdateBatch**メソッドを呼び出すまで、1つ以上のレコードに対して複数の変更をローカルにキャッシュできます。 現在のレコードを編集している場合、または **UpdateBatch** メソッドを呼び出したときに新しいレコードを追加している場合、ADO は [Update](./update-method.md) メソッドを自動的に呼び出して、保留中の変更を現在のレコードに保存してから、バッチされた変更をプロバイダーに送信します。 バッチ更新は、キーセットまたは静的カーソルのいずれかでのみ使用してください。  
  
> [!NOTE]
>  **Adを**このパラメーターの値として指定すると、現在の**レコードセット**(レコードが一致しないフィルターなど) に表示されているレコードがない場合にエラーが発生します。  
  
 基になるデータとの競合 (たとえば、レコードが別のユーザーによって既に削除されているなど) が原因で、いずれかのレコードまたはすべてのレコードに対して変更を送信しようとして失敗した場合、プロバイダーは [エラー](./errors-collection-ado.md) コレクションに警告を返し、実行時エラーが発生します。 [フィルター](./filter-property.md)プロパティ (**AdFilterAffectedRecords**) と[Status](./status-property-ado-recordset.md)プロパティを使用して、競合しているレコードを検索します。  
  
 保留中のバッチの更新をすべて取り消すには、 [CancelBatch](./cancelbatch-method-ado.md) メソッドを使用します。  
  
 一意の[テーブル](./unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)と更新の再[同期](./update-resync-property-dynamic-ado.md)の動的プロパティが設定されていて、**レコードセット**が複数のテーブルに対して結合操作を実行した結果である場合、更新の再[同期](./update-resync-property-dynamic-ado.md)プロパティの設定に応じて、 **UpdateBatch**メソッドの実行には暗黙的に再[同期](./resync-method.md)メソッドが適用されます。  
  
 バッチの個々の更新がデータソースで実行される順序は、ローカル **レコードセット**で実行された順序と同じである必要はありません。 更新順序はプロバイダに依存します。 Insert または update の foreign key 制約など、相互に関連する更新をコーディングする場合は、このことを考慮してください。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [UpdateBatch および CancelBatch メソッドの例 (VB)](./updatebatch-and-cancelbatch-methods-example-vb.md)   
 [UpdateBatch および CancelBatch メソッドの例 (VC + +)](./updatebatch-and-cancelbatch-methods-example-vc.md)   
 [CancelBatch メソッド (ADO)](./cancelbatch-method-ado.md)   
 [Clear メソッド (ADO)](./clear-method-ado.md)   
 [LockType プロパティ (ADO)](./locktype-property-ado.md)   
 [Update メソッド](./update-method.md)