---
description: Cancel メソッド (ADO)
title: Cancel メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::Cancel
- _Record::Cancel
- _Connection::Cancel
- Command25::Cancel
- _Stream::Cancel
helpviewer_keywords:
- Cancel method [ADO]
ms.assetid: e0db4e15-6787-41e2-8f13-9e9b524d620a
author: rothja
ms.author: jroth
ms.openlocfilehash: 75829400fbb1beb838b9254acf7db129980046c3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975653"
---
# <a name="cancel-method-ado"></a>Cancel メソッド (ADO)
保留中の非同期メソッド呼び出しの実行を取り消します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.Cancel  
```  
  
## <a name="remarks"></a>解説  
 **Cancel**メソッドを使用して、非同期メソッド呼び出しの実行を終了します。つまり、 **adasyncconnect**、 **adasyncconnect**、または**adasyncconnect**オプションを使用して呼び出されたメソッドです。  
  
 次の表は、特定の種類のオブジェクトに対して **Cancel** メソッドを使用した場合に終了するタスクを示しています。  
  
|*オブジェクト*がである場合|このメソッドへの最後の非同期呼び出しが終了しました|  
|----------------------|-------------------------------------------------------------|  
|[コマンド](./command-object-ado.md)|[実行](./execute-method-ado-command.md)|  
|[接続](./connection-object-ado.md)|[実行](./execute-method-ado-connection.md) または [開く](./open-method-ado-connection.md)|  
|[レコード](./record-object-ado.md)|[Copyrecord](./copyrecord-method-ado.md)、 [DeleteRecord](./deleterecord-method-ado.md)、 [MoveRecord](./moverecord-method-ado.md)、または [Open](./open-method-ado-record.md)|  
|[レコードセット](./recordset-object-ado.md)|[[ファイル]](./open-method-ado-recordset.md)|  
|[Stream](./stream-object-ado.md)|[[ファイル]](./open-method-ado-stream.md)|  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Command オブジェクト (ADO)](./command-object-ado.md)  
        [Connection オブジェクト (ADO)](./connection-object-ado.md)  
    :::column-end:::
    :::column:::
        [Record オブジェクト (ADO)](./record-object-ado.md)  
        [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
    :::column-end:::
    :::column:::
        [Stream オブジェクト (ADO)](./stream-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>参照  
 [Cancel メソッドの例 (VB)](./cancel-method-example-vb.md)   
 [Cancel メソッドの例 (VBScript)](../rds-api/cancel-method-example-vbscript.md)   
 [Cancel メソッドの例 (VC + +)](./cancel-method-example-vc.md)   
 [Cancel メソッド (RDS)](../rds-api/cancel-method-rds.md)   
 [CancelBatch メソッド (ADO)](./cancelbatch-method-ado.md)   
 [CancelUpdate メソッド (ADO)](./cancelupdate-method-ado.md)   
 [CancelUpdate メソッド (RDS)](../rds-api/cancelupdate-method-rds.md)   
 [Execute メソッド (ADO コマンド)](./execute-method-ado-command.md)   
 [Execute メソッド (ADO Connection)](./execute-method-ado-connection.md)   
 [Open メソッド (ADO Connection)](./open-method-ado-connection.md)   
 [Open メソッド (ADO Recordset)](./open-method-ado-recordset.md)