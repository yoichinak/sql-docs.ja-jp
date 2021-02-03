---
description: MSSQLSERVER_2593
title: MSSQLSERVER_2593 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 2593 (Database Engine error)
ms.assetid: 2e25bc43-606a-40de-8b87-3b55b96f4a91
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7dd3b350900cb4620f97af2ceb476fdc03f5f4aa
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99190694"
---
# <a name="mssqlserver_2593"></a>MSSQLSERVER_2593
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|2593|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC_OBJECT_ROW_PAGE_SUMMARY|  
|メッセージ テキスト|オブジェクト 'OBJECT' の PAGECOUNT ページには ROWCOUNT 行あります。|  
  
## <a name="explanation"></a>説明  
このメッセージは、DBCC CHECKALLOC を除くすべての DBCC チェックから返される情報出力の一部であり、指定されたオブジェクトの行カウントおよびページ カウントを示しています。  
  
## <a name="user-action"></a>ユーザーの操作  
なし  
  
