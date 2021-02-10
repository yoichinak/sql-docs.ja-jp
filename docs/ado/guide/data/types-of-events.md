---
description: イベントの種類
title: イベントの種類 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- EventComplete event [ADO]
- events [ADO], types
- Will events [ADO]
- complete events [ADO]
- WillEvent event [ADO]
ms.assetid: f3327ea0-635a-43d4-bd78-c1674f62f1a2
author: rothja
ms.author: jroth
ms.openlocfilehash: 9da4e5cefa1c33a2a1b4b5002dc9030550265ca3
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100032344"
---
# <a name="types-of-events"></a>イベントの種類
イベントには、次の2つの基本的な種類があります。 "は、操作が開始される前に呼び出されるイベントです。通常は、名前に" **WillChangeRecordset** "が含まれます。たとえば、「」と **接続** します。 イベントの完了後に呼び出されるイベントには、通常、名前に "Complete" が含まれます。たとえば、 **RecordChangeComplete** や **connectcomplete** などです。 **Infomessage** などの例外が存在しますが、関連付けられた操作が完了した後に発生します。  
  
## <a name="will-events"></a>イベントを発生させる  
 操作が開始される前に呼び出されるイベントハンドラーによって、操作パラメーターを確認または変更し、操作をキャンセルするか、または完了を許可することができます。 これらのイベントハンドラールーチンには、通常、<strong>という</strong>形式の名前が付いています。  
  
## <a name="complete-events"></a>完了イベント  
 操作の完了後に呼び出されるイベントハンドラーは、操作が終了したことをアプリケーションに通知できます。 このようなイベントハンドラーは、がイベントハンドラーによって保留中の操作をキャンセルしたときにも通知されます。 これらのイベントハンドラールーチンには、通常、フォーム <strong>*イベント*</strong>の名前があります。  
  
 通常、と完了イベントはペアで使用されます。  
  
## <a name="other-events"></a>その他のイベント  
 その他のイベントハンドラー (名前がフォームに含まれていないイベントは、 <strong>*イベント*</strong>または <strong>*イベント* が完了</strong>します) は、操作が完了した後にのみ呼び出されます。 これらのイベントは、 **Disconnect**、 **Endofrecordset**、および **infomessage** です。  
  
## <a name="see-also"></a>参照  
 [ADO イベントハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [言語による ADO イベントのインスタンス化](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [イベントパラメーター](../../../ado/guide/data/event-parameters.md)   
 [複数のイベント ハンドラーの連携方法](../../../ado/guide/data/how-event-handlers-work-together.md)
