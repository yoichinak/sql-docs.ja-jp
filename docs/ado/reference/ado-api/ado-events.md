---
description: ADO のイベント
title: ADO Events |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO]
- ADO, events
ms.assetid: 0ded5ad9-8f83-4224-95af-38512783b972
author: rothja
ms.author: jroth
ms.openlocfilehash: c2925a2c0a25bb919b5cfaae7a6b245f1175b9bb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976453"
---
# <a name="ado-events"></a>ADO のイベント

|Event|説明|  
|-|-|  
|[BeginTransComplete](./begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**BeginTrans**操作の後に呼び出されます。|  
|[CommitTransComplete](./begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**CommitTrans**操作の後に呼び出されます。|  
|[ConnectComplete](./connectcomplete-and-disconnect-events-ado.md)|接続の開始後に呼び出されます。|  
|[Disconnect (切断)](./connectcomplete-and-disconnect-events-ado.md)|接続の終了後に呼び出されます。|  
|[EndOfRecordset](./endofrecordset-event-ado.md)|**レコードセット**の末尾を越えて行を移動しようとしたときに呼び出されます。|  
|[ExecuteComplete](./executecomplete-event-ado.md)|コマンドの実行が完了した後に呼び出されます。|  
|[FetchComplete](./fetchcomplete-event-ado.md)|長い非同期操作内のすべてのレコードが **レコードセット**に取得された後に呼び出されます。|  
|[FetchProgress](./fetchprogress-event-ado.md)|長い非同期操作中に、 **レコードセット**に現在取得されている行の数を報告するために定期的に呼び出されます。|  
|[FieldChangeComplete](./willchangefield-and-fieldchangecomplete-events-ado.md)|1つまたは複数の **フィールド** オブジェクトの値が変更された後に呼び出されます。|  
|[InfoMessage](./infomessage-event-ado.md)|**Connectionevent**操作中に警告が発生するたびに呼び出されます。|  
|[MoveComplete](./willmove-and-movecomplete-events-ado.md)|**レコードセット**内の現在位置が変更された後に呼び出されます。|  
|[RecordChangeComplete](./willchangerecord-and-recordchangecomplete-events-ado.md)|1つ以上のレコードが変更した後に呼び出されます。|  
|[RecordsetChangeComplete](./willchangerecordset-and-recordsetchangecomplete-events-ado.md)|**レコードセット**が変更された後に呼び出されます。|  
|[RollbackTransComplete](./begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**RollbackTrans**操作の後に呼び出されます。|  
|[Changefield](./willchangefield-and-fieldchangecomplete-events-ado.md)|保留中の操作が**レコードセット**内の1つまたは複数の**フィールド**オブジェクトの値を変更する前に呼び出されます。|  
|[Changerecord](./willchangerecord-and-recordchangecomplete-events-ado.md)|**レコードセット**内の1つ以上のレコード (行) が変更される前に呼び出されます。|  
|[WillChangeRecordset](./willchangerecordset-and-recordsetchangecomplete-events-ado.md)|保留中の操作によって **レコードセット**が変更される前に呼び出されます。|  
|[接続](./willconnect-event-ado.md)|接続が開始される前に呼び出されます。|  
|[実行する](./willexecute-event-ado.md)|保留中のコマンドがこの接続で実行される直前に呼び出され、保留中の実行パラメーターを確認および変更する機会をユーザーに与えます。|  
|[移動](./willmove-and-movecomplete-events-ado.md)|"イベントの**移動**" は、保留中の操作が**レコードセット**内の現在の位置を変更*する前に*呼び出されます。|  
  
## <a name="see-also"></a>参照  
 [ADO API リファレンス](./ado-api-reference.md)   
 [ADO コレクション](./ado-collections.md)   
 [ADO の動的プロパティ](./ado-dynamic-properties.md)   
 [ADO 列挙定数](./ado-enumerated-constants.md)   
 [付録 B: ADO エラー](../../guide/appendixes/appendix-b-ado-errors.md)   
 [ADO イベントの処理](../../guide/data/handling-ado-events.md)   
 [ADO メソッド](./ado-methods.md)   
 [ADO オブジェクトモデル](./ado-object-model.md)   
 [ADO オブジェクトとインターフェイス](./ado-objects-and-interfaces.md)   
 [ADO のプロパティ](./ado-properties.md)