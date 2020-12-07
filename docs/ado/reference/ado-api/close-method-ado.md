---
description: Close メソッド (ADO)
title: Close メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Close
- _Stream::Close
- _Record::Close
helpviewer_keywords:
- Close method [ADO]
ms.assetid: 3cdf27d1-a180-4cff-8e42-95dec5fb1b55
author: rothja
ms.author: jroth
ms.openlocfilehash: 7843642c38a30d854cb6729fd5a418de8c91f2c7
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975393"
---
# <a name="close-method-ado"></a>Close メソッド (ADO)
開いているオブジェクトとすべての依存オブジェクトを閉じます。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.Close  
```  
  
## <a name="remarks"></a>解説  
 **Close**メソッドを使用して、[接続](./connection-object-ado.md)、[レコード](./record-object-ado.md)、[レコードセット](./recordset-object-ado.md)、または[ストリーム](./stream-object-ado.md)オブジェクトを閉じて、関連付けられているシステムリソースを解放します。 オブジェクトを閉じると、メモリから削除されません。プロパティの設定を変更し、後でもう一度開くことができます。 オブジェクトをメモリから完全に削除するには、オブジェクトを閉じて、オブジェクト変数を *Nothing* (Visual Basic) に設定します。  
  
## <a name="connection"></a>接続  
 **Close**メソッドを使用して**connection**オブジェクトを閉じると、接続に関連付けられているアクティブな**レコードセット**オブジェクトも閉じられます。 閉じようとしている**接続**オブジェクトに関連付けられている[Command](./command-object-ado.md)オブジェクトは永続化されますが、**接続**オブジェクトに関連付けられなくなります。つまり、 [ActiveConnection](./activeconnection-property-ado.md)プロパティは**Nothing**に設定されます。 また、 **コマンド** オブジェクトの [parameters](./parameters-collection-ado.md) コレクションは、プロバイダーによって定義されたパラメーターに対して消去されます。  
  
 後で [Open](./open-method-ado-connection.md) メソッドを呼び出して、同じまたは別のデータソースへの接続を再確立することができます。 **接続**オブジェクトが閉じられている間に、データソースへの接続を開いているメソッドを呼び出すと、エラーが生成されます。  
  
 接続に開いている**レコードセット**オブジェクトがあるときに**接続**オブジェクトを閉じると、すべての**レコードセット**オブジェクトの保留中の変更がロールバックされます。 トランザクションの進行中に ( **Close**メソッドを呼び出すことによって)**接続**オブジェクトを明示的に終了すると、エラーが生成されます。 トランザクションの進行中に **接続** オブジェクトがスコープ外になると、ADO によってトランザクションが自動的にロールバックされます。  
  
## <a name="recordset-record-stream"></a>レコードセット、レコード、ストリーム  
 **Close**メソッドを使用して**レコードセット**、**レコード**、または**ストリーム**オブジェクトを閉じると、関連付けられているデータと、この特定のオブジェクトを介してデータに対して持っていた排他アクセスが解放されます。 後で [Open](./open-method-ado-recordset.md) メソッドを呼び出して、同じ、または変更された属性を持つオブジェクトを再び開くことができます。  
  
 **レコードセット**オブジェクトが閉じられている間に、ライブカーソルを必要とするメソッドを呼び出すと、エラーが発生します。  
  
 即時更新モードで編集が進行中の場合、 **Close** メソッドを呼び出すとエラーが発生します。代わりに、 [Update](./update-method.md) または [CancelUpdate](./cancelupdate-method-ado.md) メソッドを最初に呼び出します。 バッチ更新モードで **レコードセット** オブジェクトを閉じた場合、最後の [UpdateBatch](./updatebatch-method.md) 呼び出し以降のすべての変更は失われます。  
  
 [Clone](./clone-method-ado.md)メソッドを使用して、開いている**レコードセット**オブジェクトのコピーを作成する場合、元のまたは複製を閉じると、他のコピーには影響しません。  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Connection オブジェクト (ADO)](./connection-object-ado.md)  
        [Record オブジェクト (ADO)](./record-object-ado.md)  
    :::column-end:::
    :::column:::
        [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
        [Stream オブジェクト (ADO)](./stream-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>参照  
 [Open および Close メソッドの例 (VB)](./open-and-close-methods-example-vb.md)   
 [Open および Close メソッドの例 (VBScript)](./open-and-close-methods-example-vbscript.md)   
 [Open および Close メソッドの例 (VC + +)](./open-and-close-methods-example-vc.md)   
 [Open メソッド (ADO Connection)](./open-method-ado-connection.md)   
 [Open メソッド (ADO Recordset)](./open-method-ado-recordset.md)   
 [Save メソッド](./save-method.md)