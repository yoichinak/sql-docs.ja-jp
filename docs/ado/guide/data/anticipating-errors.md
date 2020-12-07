---
description: エラーの予測
title: エラーの予測 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- anticipating errors [ADO]
- errors [ADO], preventing
- preventing errors [ADO]
ms.assetid: ea1d4a97-58c3-476b-a496-cc80db2a90d5
author: rothja
ms.author: jroth
ms.openlocfilehash: f5affe90da5a982a6e01bd5719793581fb3c5f13
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991613"
---
# <a name="anticipating-errors"></a>エラーの予測
エラーの防止は、少なくともエラー処理と同じです。 この最後のセクションでは、エラーが発生する可能性が低くなるようにアプリケーションが実行できる予防措置の一覧を示します。  
  
 オブジェクトの状態を確認するには、そのオブジェクトを使用して操作を実行する前に **state** プロパティの値を確認します。 たとえば、アプリケーションがグローバル**接続**を使用している場合は、 **open**メソッドを呼び出す前に、その**状態**プロパティをチェックして、既に開いているかどうかを確認します。  
  
-   ユーザーからのデータを受け入れるプログラムには、データストアに送信する前にデータを検証するコードを含める必要があります。 データストア、プロバイダー、ADO、またはプログラミング言語に依存して、問題を通知することはできません。 ユーザーが入力したすべてのバイトを確認し、データがフィールドの正しい型であること、および必要なフィールドが空でないことを確認する必要があります。  
  
 データをデータストアに書き込む前に、データを確認してください。 これを行う最も簡単な方法は、WillUpdateRecordset**イベントを**処理すること**WillUpdateRecordset**です。 ADO イベントの処理の詳細については、「 [Ado イベントの処理](./handling-ado-events.md)」を参照してください。  
  
 レコードポインターの移動を試行する前に、レコード **セット** オブジェクトがレコード **セット** の境界を超えていないことを確認してください。 **EOF**が true のとき、または**BOF**が True のときに**MovePrev**を**MoveNext**にしようとすると、エラーが発生します。 **EOF**と**BOF**の両方が True の場合に**Move**メソッドを実行すると、エラーが生成されます。  
  
 また、空の**レコードセット**に対して**Seek**や**Find**などの操作を実行しようとすると、エラーが発生します。