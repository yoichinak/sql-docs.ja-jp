---
description: バッチ モード
title: バッチモード |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], batch mode
- batch mode [ADO]
- updating data [ADO], batch mode
ms.assetid: 0cb548e0-fcb4-4c49-98c8-be287911f826
author: rothja
ms.author: jroth
ms.openlocfilehash: a2cda3a14dc51532d52184f8b2101981d4f36cd3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991603"
---
# <a name="batch-mode"></a>バッチ モード
バッチモードは、 **LockType** プロパティが **Adlockbatchoptimistic** に設定され、バッチ更新がプロバイダーによってサポートされている場合に有効になります。 特定のロックの種類の設定は、カーソルの場所によっては使用できません。 たとえば、 **カーソル位置** が **adUseClient**に設定されている場合、ペシミスティックロックの種類は使用できません。 逆に、プロバイダーは、カーソル位置がサーバー上にある場合にバッチオプティミスティックロックをサポートできません。 バッチ更新は、キーセットまたは静的カーソルのいずれかでのみ使用してください。  
  
 **UpdateBatch**メソッドを使用して、コピーバッファーに保持されている**レコードセット**の変更をサーバーに送信し、データソースを更新します。 次のセクションでは、 **レコードセット** をバッチモードで開き、コピーバッファーに変更を加えた後、 **UpdateBatch**の呼び出しを使用して変更をデータソースに送信します。  
  
 このセクションのトピックは次のとおりです。  
  
-   [更新プログラムの送信: UpdateBatch メソッド](./sending-the-updates-updatebatch-method.md)  
  
-   [更新されたレコードのフィルター処理](./filtering-for-updated-records.md)  
  
-   [失敗した更新の処理](./dealing-with-failed-updates.md)  
  
-   [競合の検出および解決](./detecting-and-resolving-conflicts.md)  
  
-   [レコードセットの切断と再接続](./disconnecting-and-reconnecting-the-recordset.md)  
  
-   [JOINed の結果の更新: Unique Table](./updating-joined-results-unique-table.md)