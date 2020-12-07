---
description: ロックの種類
title: ロックの種類 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AdLockBatchOptimistic [ADO]
- AdLockReadOnly [ADO]
- AdLockUnspecified [ADO]
- locks [ADO], types
- AdLockOptimistic [ADO]
- AdLockPessimistic [ADO]
ms.assetid: 12a978c0-b8a0-4ef0-87f0-a43c13659272
author: rothja
ms.author: jroth
ms.openlocfilehash: 55087e96c0855f24153dee9bc279d9abf58d3f04
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979263"
---
# <a name="types-of-locks"></a>ロックの種類
## <a name="adlockbatchoptimistic"></a>adLockBatchOptimistic  
 オプティミスティックバッチ更新を示します。 バッチ更新モードでは必須です。  
  
 多くのアプリケーションは、一度に多数の行をフェッチし、挿入、更新、または削除する行セット全体を含む、調整された更新を行う必要があります。 バッチカーソルを使用すると、サーバーへのラウンドトリップが1回だけ必要になります。これにより、更新のパフォーマンスが向上し、ネットワークトラフィックが減少します。 バッチカーソルライブラリを使用して、静的カーソルを作成し、データソースから切断することができます。 この時点で、行に変更を加え、その後再接続して、変更内容をバッチ内のデータソースにポストすることができます。  
  
## <a name="adlockoptimistic"></a>adLockOptimistic  
 **更新**メソッドを呼び出した場合にのみ、プロバイダーがオプティミスティックロックロックのレコードを使用することを示します。 つまり、レコードを編集してから **Update**を呼び出すと、競合が発生する別のユーザーがデータを変更する可能性があります。 このロックの種類は、衝突の可能性が低い場合や、衝突がすぐに解決される場合に使用します。  
  
## <a name="adlockpessimistic"></a>adLockPessimistic  
 ペシミスティックロック、レコードごとのレコードを示します。 プロバイダーは、レコードを正常に編集するために必要な処理を実行します。通常は、データソースのレコードを編集する直前にロックします。 もちろん、これは、Update を呼び出すことによってロックが解除されるまで、他のユーザーが編集を開始した後にレコードを使用できないことを意味し **ます。** 予約システムなど、データに対する同時変更を行うことができないシステムでは、このタイプのロックを使用します。  
  
## <a name="adlockreadonly"></a>adLockReadOnly  
 読み取り専用レコードを示します。 データを変更することはできません。 読み取り専用ロックは、"最速" のロックの種類です。これは、サーバーがレコードのロックを維持する必要がないためです。  
  
## <a name="adlockunspecified"></a>adLockUnspecified  
 はロックの種類を指定していません。
