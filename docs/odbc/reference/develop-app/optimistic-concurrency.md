---
description: オプティミスティック コンカレンシー
title: オプティミスティック同時実行制御 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
- optimistic concurrency [ODBC]
ms.assetid: 9d71e09e-bc68-4c1f-9229-ed2a7be7d324
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dce1982edbb8f5a417404c6e24e8a40d25b58e0b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429134"
---
# <a name="optimistic-concurrency"></a>オプティミスティック コンカレンシー
*オプティミスティック同時実行制御* は、トランザクション間の競合が発生することはほとんどないというオプティミスティックな前提から名前を取得します。競合は、別のトランザクションによってデータ行が更新または削除されるときに、現在のトランザクションによって読み取られた時点と更新または削除された時間の間に発生したと言われます。 これは、アプリケーション開発者がこのような衝突が一般的であると考えている *ペシミスティック同時実行制御* (ロック) とは逆です。  
  
 オプティミスティック同時実行制御では、行が更新または削除されるまで、ロックが解除されたままになります。 その時点で、行は再読み込みされ、最後に読み取られてから変更されたかどうかが確認されます。 行が変更された場合、更新または削除は失敗し、再試行する必要があります。  
  
 行が変更されたかどうかを判断するために、行のキャッシュされたバージョンに対して新しいバージョンがチェックされます。 このチェックは、行のバージョン (SQL Server のタイムスタンプ列、行の各列の値など) に基づいて行うことができます。 多くの Dbms では、行バージョンはサポートされていません。  
  
 オプティミスティック同時実行制御は、データソースまたはアプリケーションによって実装できます。 どちらの場合も、アプリケーションでは Read Committed などの低トランザクション分離レベルを使用する必要があります。高いレベルを使用すると、オプティミスティック同時実行制御を使用した場合に得られる同時実行の増加が否定されます。  
  
 オプティミスティック同時実行制御がデータソースによって実装されている場合、アプリケーションは、SQL_ATTR_CONCURRENCY statement 属性を SQL_CONCUR_ROWVER または SQL_CONCUR_VALUES に設定します。 行を更新または削除するには、位置指定の update または delete ステートメントを実行するか、ペシミスティック同時実行の場合と同じように **SQLSetPos** を呼び出します。競合によって更新または削除が失敗した場合、ドライバーまたはデータソースから SQLSTATE 01001 (カーソル操作の競合) が返されます。  
  
 アプリケーション自体でオプティミスティック同時実行制御が実装されている場合は、SQL_ATTR_CONCURRENCY ステートメントの属性を SQL_CONCUR_READ_ONLY に設定して行を読み取ります。 行バージョンを比較し、行バージョン列がわからない場合は、この列の名前を決定するために、SQL_ROWVER オプションを使用して **Sqlの列** を呼び出します。  
  
 アプリケーションで行を更新または削除するには、同時実行を SQL_CONCUR_LOCK に (行への書き込みアクセスを取得) し、アプリケーションが読み取るときに行で保持されていたバージョンまたは値を指定する**where**句を使用して**UPDATE**ステートメントまたは**DELETE**ステートメントを実行します。 その後、行が変更された場合、ステートメントは失敗します。 **WHERE**句によって行が一意に識別されない場合は、ステートメントによって他の行が更新または削除されることもあります。行バージョンは常に行を一意に識別しますが、行の値は、主キーが含まれている場合にのみ行を一意に識別します。
