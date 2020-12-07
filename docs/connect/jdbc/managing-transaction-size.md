---
description: トランザクション サイズの管理
title: トランザクション サイズの管理 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 82900342-bc80-445f-98a4-468a303aae1e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1ba88edf4c4c8f1dfb4e8b7cd27db3102be448c4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438374"
---
# <a name="managing-transaction-size"></a>トランザクション サイズの管理
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  トランザクションを扱うときは、トランザクションをできるだけ短くすることが重要です。 [setAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md) メソッドを使用して有効または無効にすることが可能な、既定の自動コミット モードでは、すべてのアクションが自動的にコミットされます。 これは、ほとんどの開発者にとっては最も簡単に扱えるモードです。  
  
 手動トランザクションを使用するときは、トランザクションを可能な限り迅速にコミットする必要があります。 開いているトランザクションを保持していると、他のユーザーがデータにアクセスできなくなります。 たとえば、ロールバックの呼び出しを catch ブロック内に配置し、コミットの呼び出しを finally ブロック内に配置するというプログラミング手法が望ましい場合があります。 ただしこれは、アプリケーションの設計によって異なります。  
  
 トランザクションのサイズを小さくすると、コンカレンシーが向上します。 たとえば、手動トランザクションを開始し、20,000 行のテーブル内の 10,000 行を変更すると、他のすべてのユーザーは、たとえデータを読み取ろうとしているだけであっても、テーブルの半分にはまったくアクセスできなくなります。 変更する行を 2,000 行に減らせば、テーブルの 90% はアクセス可能になります。  
  
 さらに、アプリケーションでブロックの問題が発生する可能性があり、タイムアウトする必要がある場合は、ロック タイムアウトの設定を使用してください。 これを行うには、[setLockTimeout](../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md) メソッドを使用します。 ロック タイムアウトの既定値は -1 です。これは、ロックを待機している間に無期限にブロックすることを意味します。 ロック タイムアウトを 30 秒に設定すると、別の接続によってブロックされている接続が 30 秒でタイムアウトになります。  
  
## <a name="see-also"></a>関連項目  
 [JDBC ドライバーによるパフォーマンスと信頼性の強化](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
