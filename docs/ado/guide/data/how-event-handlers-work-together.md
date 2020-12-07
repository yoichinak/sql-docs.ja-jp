---
description: 複数のイベント ハンドラーの連携方法
title: イベントハンドラーの連携方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO], about event handlers
- unpaired event handlers [ADO]
- paired event handlers [ADO]
- single event handlers [ADO]
- event handlers [ADO]
- multiple object event handlers [ADO]
ms.assetid: a86c8a02-dd69-420d-8a47-0188b339858d
author: rothja
ms.author: jroth
ms.openlocfilehash: 37e1c5d081ccbcacaf50aa385a87afa9555ad2ca
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980523"
---
# <a name="how-event-handlers-work-together"></a>複数のイベント ハンドラーの連携方法
Visual Basic でプログラミングする場合を除き、すべてのイベントを実際に処理するかどうかに関係なく、 **接続** イベントと **レコードセット** イベントのすべてのイベントハンドラーを実装する必要があります。 実行する必要のある実装作業の量は、プログラミング言語によって異なります。 詳細については、「 [言語別の ADO イベントのインスタンス化](./ado-event-instantiation-by-language.md)」を参照してください。  
  
## <a name="paired-event-handlers"></a>ペアのイベントハンドラー  
 各イベントハンドラーには、関連付けられた **完全な** イベントハンドラーがあります。 たとえば、アプリケーションでフィールドの値が変更された場合、 **「」というイベントハンドラー** が呼び出されます。 変更が許容される場合、アプリケーションは **Adstatus** パラメーターを変更せずにそのまま使用し、操作を実行します。 操作が完了すると、 **FieldChangeComplete** イベントによって、操作が完了したことがアプリケーションに通知されます。 正常に完了した場合、 **Adstatus** は **adstatusok**を含みます。それ以外の場合、 **Adstatus** に **Adstatuserrorの curred** が含まれています。エラーの原因を特定するには、 **error** オブジェクトを確認する必要があります。  
  
 が呼び出されたときに、変更を行わないことを決定 **する場合が** あります。 その場合は、 **Adstatus**を**adstatuscancel**に設定します。 操作は取り消され、 **FieldChangeComplete**イベントは**Adstatuserror Curred**の**adstatus**値を受け取ります。 **エラー**オブジェクトには、操作が取り消されたことを**FieldChangeComplete**ハンドラーが認識するように、 **adErrOperationCancelled**が含まれています。 ただし、パラメーターを変更する前に**adstatus**パラメーターの値を確認する必要があります。 Adstatuscancel**に設定**した場合、パラメーターが**adStatusCancel** **adstatuscantdeny**に設定されていると、プロシージャには影響しません。  
  
 場合によっては、1つの操作で複数のイベントを発生させることができます。 たとえば、 **レコードセット** オブジェクトには、 **フィールド** の変更や **レコード** の変更に関するイベントがペアで含まれています。 アプリケーションが **フィールド**の値を変更すると、" **イベントハンドラー** " が呼び出されます。 操作を続行できると判断された場合 **は、発生したイベントハンドラー** も発生します。 また、このハンドラーによってイベントが続行される場合は、変更が行われ、 **FieldChangeComplete** イベントハンドラーと **RecordChangeComplete** イベントハンドラーが呼び出されます。 特定の操作のイベントハンドラーが呼び出される順序は定義されていないため、特定のシーケンスの呼び出しハンドラーに依存するコードを記述しないようにする必要があります。  
  
 複数のイベントが発生した場合、イベントの1つによって保留中の操作が取り消されることがあります。 たとえば、アプリケーションが **フィールド**の値を変更した場合、通常は、両方の **Changefield** とが **changerecord** イベントハンドラーが呼び出されます。 ただし、操作が最初のイベントハンドラーで取り消された場合、その操作に関連付けられた **完全な** ハンドラーは、 **adstatusoperationcancelled**ですぐに呼び出されます。 2番目のハンドラーは呼び出されません。 ただし、最初のイベントハンドラーによってイベントが続行される場合は、他のイベントハンドラーが呼び出されます。 その後、操作をキャンセルすると、前の例のように **完了** した両方のイベントが呼び出されます。  
  
## <a name="unpaired-event-handlers"></a>対になっていないイベントハンドラー  
 イベントに渡される状態が**Adstatuscantdeny**でない限り、 *Status*パラメーターで**adStatusUnwantedEvent**を返すことによって、イベントのイベント通知を無効にすることができます。 たとえば、 **完全な** イベントハンドラーが初めて呼び出されたときに、 **adStatusUnwantedEvent**を返すことができます。 その後 **、イベントのみが表示** されます。 ただし、一部のイベントは複数の理由でトリガーされることがあります。 この場合、イベントには *Reason* パラメーターがあります。 **AdStatusUnwantedEvent**を返すと、その特定の理由で発生した場合にのみ、そのイベントの通知を受信しなくなります。 つまり、イベントがトリガーされる可能性がある原因ごとに通知を受け取る可能性があります。  
  
 単一のイベントハンドラー **は** 、操作で使用されるパラメーターを調べるときに便利です。 これらの操作パラメーターを変更するか、操作を取り消すことができます。  
  
 または、 **完全な** イベント通知を有効にしたままにします。 最初のイベントハンドラーが呼び出されたときに、 **adStatusUnwantedEvent**を返します。 その後、 **完全な** イベントのみを受信します。  
  
 単一の **完全な** イベントハンドラーは、非同期操作の管理に役立ちます。 各非同期操作には、適切な **完全** なイベントがあります。  
  
 たとえば、大きな [レコードセット](../../reference/ado-api/recordset-object-ado.md) オブジェクトを設定するには、長い時間がかかることがあります。 アプリケーションが適切に記述されている場合は、操作を開始 `Recordset.Open(...,adAsyncExecute)` して他の処理を続行できます。 **レコードセット**に**ExecuteComplete**イベントが設定されると、最終的に通知が表示されます。  
  
## <a name="single-event-handlers-and-multiple-objects"></a>単一のイベントハンドラーと複数のオブジェクト  
 Microsoft Visual C++®のようなプログラミング言語の柔軟性により、複数のオブジェクトのイベントを1つのイベントハンドラーで処理できます。 たとえば、1つの **Disconnect** イベントハンドラーで複数の **接続** オブジェクトからイベントを処理することができます。 接続のいずれかが終了した場合、 **切断** イベントハンドラーが呼び出されます。 イベントハンドラーオブジェクトのパラメーターが対応する **接続** オブジェクトに設定されるため、イベントが発生した接続を特定できます。  
  
> [!NOTE]
>  この言語では、1つのオブジェクトのみをイベントハンドラーに関連付けることができるため、この手法を Visual Basic で使用することはできません。  
  
## <a name="see-also"></a>参照  
 [ADO イベントハンドラーの概要](./ado-event-handler-summary.md)   
 [言語による ADO イベントのインスタンス化](./ado-event-instantiation-by-language.md)   
 [イベントパラメーター](./event-parameters.md)   
 [イベントの種類](./types-of-events.md)