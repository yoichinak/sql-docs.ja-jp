---
description: ADO イベントの処理
title: ADO イベントの処理 |Microsoft Docs
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
- event handlers [ADO]
ms.assetid: e9003457-0762-48b3-942f-0820266b158f
author: rothja
ms.author: jroth
ms.openlocfilehash: ff36542abb462ffc63e8704a5c6c3cdd6670d280
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980703"
---
# <a name="handling-ado-events"></a>ADO イベントの処理
ADO イベントモデルでは、操作の開始前または完了後に *イベント*(通知) を発行する、特定の同期および非同期の ado 操作がサポートされています。 イベントは実際には、アプリケーションで定義するイベントハンドラールーチンの呼び出しです。  
  
 操作が開始される前に発生するイベントのグループに対してハンドラー関数またはプロシージャを指定する場合は、操作に渡されたパラメーターを確認または変更できます。 まだ実行されていないため、操作を取り消すか、または完了を許可することができます。  
  
 ADO を非同期的に使用する場合は、操作の完了後に発生するイベントが特に重要になります。 たとえば、非同期の [レコードセット](../../reference/ado-api/open-method-ado-recordset.md) を起動するアプリケーションは、操作の終了時に実行完了イベントによって通知されます。  
  
 ADO イベントモデルを使用すると、アプリケーションにオーバーヘッドがいくつか追加されますが、ループを使用したオブジェクトの [状態](../../reference/ado-api/state-property-ado.md) プロパティの監視など、非同期操作を処理する他の方法よりもはるかに柔軟性があります。  
  
> [!NOTE]
>  イベントを処理するには、ADO でメッセージポンプを使用するか、シングルスレッドアパートメント (STA) モデルで使用する必要があります。 ADO イベントは、非表示のウィンドウを作成することによって内部的に処理されます。 イベントを発生させる必要がある場合、ADO はこのウィンドウにメッセージを投稿します。 これは、コネクションポイントで **IConnectionPoint:: Advise** を呼び出したスレッドにイベントが確実に送信されるようにするために行われます。 このアーキテクチャでは、通知を受信する必要があるスレッドがウィンドウメッセージをポンプしない場合に問題が発生する可能性があります。 潜在的な問題としては、ADO イベントがスレッドに配信されないことや、グローバルウィンドウのブロードキャストがタイムアウトになり、システム全体の処理速度が低下することがあります。これは、非表示のウィンドウがメッセージを処理しないためです。 STA スレッドでは、通常、メッセージポンプが実行されているので、この問題は STA スレッドではマニフェストを作成しません。 ただし、MTA スレッドには通常、メッセージポンプがないため、問題は通常、MTA スレッドでマニフェストを作成します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ADO イベント ハンドラーの概要](./ado-event-handler-summary.md)  
  
-   [イベントの種類](./types-of-events.md)  
  
-   [イベント パラメーター](./event-parameters.md)  
  
-   [複数のイベント ハンドラーの連携方法](./how-event-handlers-work-together.md)  
  
-   [言語別の ADO イベントのインスタンス化](./ado-event-instantiation-by-language.md)  
  
## <a name="see-also"></a>参照  
 [ADO イベントハンドラーの概要](./ado-event-handler-summary.md)   
 [言語による ADO イベントのインスタンス化](./ado-event-instantiation-by-language.md)   
 [ADO イベント](../../reference/ado-api/ado-events.md)   
 [イベントパラメーター](./event-parameters.md)   
 [イベントの種類](./types-of-events.md)