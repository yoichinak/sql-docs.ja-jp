---
description: WillExecute イベント (ADO)
title: イベント実行 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillExecute
- Connection::WillExecute
helpviewer_keywords:
- WillExecute event [ADO]
ms.assetid: dd755e46-f589-48a3-93a9-51ff998d44b5
author: rothja
ms.author: jroth
ms.openlocfilehash: f56e864efd37b927ae657edc2ef2e8307d839104
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987773"
---
# <a name="willexecute-event-ado"></a>WillExecute イベント (ADO)
この **イベントは、接続** で保留中のコマンドが実行される直前に呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
WillExecute Source, CursorType, LockType, Options, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>パラメーター  
 *ソース*  
 SQL コマンドまたはストアドプロシージャ名を含む **文字列** 。  
  
 *CursorType*  
 開かれる**レコードセット**のカーソルの種類が格納されている[cursor typeenum](./cursortypeenum.md) 。 このパラメーターを使用すると、**レコードセット**の[OPEN メソッド (ADO recordset)](./open-method-ado-recordset.md)操作中に、カーソルを任意の型に変更できます。 *CursorType* は、他の操作では無視されます。  
  
 *LockType*  
 開かれる**レコードセット**のロックの種類を格納する[locktypeenum](./locktypeenum.md) 。 このパラメーターを使用すると、 **RecordsetOpen** 操作中に任意の型にロックを変更できます。 他の操作では、 *LockType*は無視されます。  
  
 *Options*  
 コマンドを実行したり、**レコードセット**を開いたりするために使用できるオプションを示す**Long 型**の値です。  
  
 *adStatus*  
 このイベントが呼び出されたときに**Adstatuscantdeny**または**Adstatusok**となる[eventstatusenum](./eventstatusenum.md)ステータス値。 **Adstatuscantdeny**の場合、このイベントは保留中の操作の取り消しを要求しない可能性があります。  
  
 *pCommand*  
 このイベント通知を適用する対象の [コマンドオブジェクト (ADO)](./command-object-ado.md) オブジェクト。  
  
 *pRecordset*  
 このイベント通知を適用する [ADO (Recordset オブジェクト](./recordset-object-ado.md) ) オブジェクト。  
  
 *pConnection*  
 このイベント通知を適用する [接続オブジェクト (ADO)](./connection-object-ado.md) オブジェクト。  
  
## <a name="remarks"></a>解説  
 接続によっ **てイベントが発生する可能性** があります。  [Execute メソッド (Ado Connection)](./execute-method-ado-connection.md)、 [EXECUTE メソッド (ado Command)](./execute-method-ado-command.md)、または [Open method (Ado Recordset)](./open-method-ado-recordset.md) メソッド。 *Pconnection* パラメーターには、常に **接続** オブジェクトへの有効な参照を含める必要があります。 イベントが **Connection.Exeかわいらしい**のために発生した場合、 *Precordset* パラメーターと *precordset* パラメーターは **Nothing**に設定されます。 イベントが **レコードセット**によって発生した場合、 *Precordset* パラメーターは **レコードセット** オブジェクトを参照し、 *precordset* パラメーターは **Nothing**に設定されます。 イベントが **Command.Exeかわいらしい**のために発生した場合、 *Pcommand* パラメーターは **コマンド** オブジェクトを参照し、 *pcommand* パラメーターは **Nothing**に設定されます。  
  
 を**実行**すると、保留中の実行パラメーターを確認および変更できます。 このイベントは、保留中のコマンドがキャンセルされたことを示す要求を返す場合があります。  
  
> [!NOTE]
>  **コマンド**の元のソースが[COMMANDSTREAM プロパティ (ADO)](./commandstream-property-ado.md)プロパティによって指定されたストリームである場合は、新しい文字列をに渡し**て、****コマンド**_のソースを_変更します。 **Commandstream**プロパティがクリアされ、 [COMMANDTEXT プロパティ (ADO)](./commandtext-property-ado.md)プロパティが新しいソースで更新されます。 **Commandstream**によって指定された元のストリームは解放され、アクセスできなくなります。  
  
 新しいソース文字列の言語が、 [Dialect プロパティ](./dialect-property.md)プロパティ ( **commandstream**にこれ) の元の設定と異なる場合は、 *pcommand*によって参照されるコマンドオブジェクトの**dialect**プロパティを設定して、正しい言語を指定する必要があります。  
  
## <a name="see-also"></a>参照  
 [ADO Events モデルの例 (VC + +)](./ado-events-model-example-vc.md)   
 [ADO イベントハンドラーの概要](../../guide/data/ado-event-handler-summary.md)   
 [Connection オブジェクト (ADO)](./connection-object-ado.md)