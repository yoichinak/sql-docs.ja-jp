---
description: MSSQLSERVER_1205
title: MSSQLSERVER_1205 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 1205 (Database Engine error)
ms.assetid: 9fe3f67c-df3c-4642-a3a4-ccc0e138b632
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8ce9d2d99d3db0fc18586b9292876d2e4e6c985b
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99197164"
---
# <a name="mssqlserver_1205"></a>MSSQLSERVER_1205
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|1205|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|LK_VICTIM|  
|メッセージ テキスト|トランザクション (プロセス ID %d) が、%.*ls 個のリソースで他のプロセスとデッドロックして、このトランザクションがそのデッドロックの対象となりました。 トランザクションを再実行してください。|  
  
## <a name="explanation"></a>説明

個別のトランザクションで、競合する順序でリソースにアクセスすると、[デッドロック](../sql-server-transaction-locking-and-row-versioning-guide.md?#deadlocks)が発生します。 次に例を示します。  
  
- Transaction2 によって **Table2.Row2** が更新されている間に、Transaction1 によって **Table1.Row1** が更新されました
- Transaction1 によって **Table2.Row2** の更新が試みられましたが、Transaction2 によるコミットがまだなので、ブロックされました  
- 今度は Transaction2 によって **Table1.Row1** の更新が試みられましたが、Transaction1 によるコミットがまだなので、ブロックされました
- Transaction1 が Transaction2 の完了を待機していますが、Transaction2 は Transaction1 の完了を待機しているので、デッドロックが生じました。  
  
システムによって、このデッドロックが検出され、関係するトランザクションの 1 つが "犠牲者" として選択されます。 次に、このエラー メッセージが発行されて、犠牲者のトランザクションがロールバックされます。  詳細については、「[デッドロック](../sql-server-transaction-locking-and-row-versioning-guide.md?#deadlocks)」を参照してください。

## <a name="user-action"></a>ユーザーの操作  

トランザクションを再実行します。 また、デッドロックを回避できるようにアプリケーションを修正します。 デッドロック対象として選択されたトランザクションは、再試行が可能です。同時に実行されている操作によって状況が異なりますが、再試行は成功する可能性があります。  
  
デッドロックを回避するには、すべてのトランザクションから行に対するアクセスが、同じ順序 (**Table1** の次に **Table2** など) で行われるようにすることを検討します。 こうすることで、ブロックが発生することはあっても、デッドロックは発生しません。  
  
詳細については、「[デッドロックの処理](../sql-server-transaction-locking-and-row-versioning-guide.md?#handling-deadlocks)」および「[デッドロックの最小化](../sql-server-transaction-locking-and-row-versioning-guide.md#deadlock_minimizing)」を参照してください。
