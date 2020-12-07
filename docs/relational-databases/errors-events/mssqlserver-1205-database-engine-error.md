---
description: MSSQLSERVER_1205
title: MSSQLSERVER_1205 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1205 (Database Engine error)
ms.assetid: 9fe3f67c-df3c-4642-a3a4-ccc0e138b632
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d45f2095a679c8549ebbb42852ab6e2316596852
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88336138"
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
個別のトランザクションで、競合する順序でリソースにアクセスすると、デッドロックが発生します。 次に例を示します。  
  
-   Transaction2 が **Table2.Row2** を更新している間に、Transaction1 が **Table1.Row1** を更新しました。  
  
-   Transaction1 は **Table2.Row2** を更新しようとしましたが、Transaction2 のコミットがまだなので、ブロックされました。  
  
-   今度は Transaction2 が **Table1.Row1** を更新しようとしましたが、Transaction1 のコミットがまだなので、ブロックされました。  
  
-   Transaction1 が Transaction2 の完了を待機していますが、Transaction2 は Transaction1 の完了を待機しているので、デッドロックが生じました。  
  
このメッセージは、このデッドロックが検出され、"被害者" として関与しているトランザクションの 1 つが選択されると発行されます。その被害者のトランザクションはロールバックされます。  
  
## <a name="user-action"></a>ユーザーの操作  
トランザクションを再実行します。 また、デッドロックを回避できるようにアプリケーションを修正します。 デッドロック対象として選択されたトランザクションは、再試行が可能です。同時に実行されている操作によって状況が異なりますが、再試行は成功する可能性があります。  
  
デッドロックを回避するには、すべてのトランザクションから行に対するアクセスが、同じ順序 (**Table1** の次に **Table2** など) で行われるようにすることを検討します。こうすることで、ブロックが発生しても、デッドロックは発生しません。  
  
