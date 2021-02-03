---
description: MSSQLSERVER_5231
title: MSSQLSERVER_5231 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 5231 (Database Engine error)
ms.assetid: 6954ae84-ed0b-4f4c-9d0a-e73f3d71476c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8a300734abdc1a175a9601cd7e1049d75b1677ba
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99159579"
---
# <a name="mssqlserver_5231"></a>MSSQLSERVER_5231
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|5231|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC4_DEADLOCK_SKIPPED_OBJECT|  
|メッセージ テキスト|オブジェクト ID O_ID (オブジェクト 'NAME'):このオブジェクトを確認のためにロックしようとして、デッドロックが発生しました。 このオブジェクトはスキップされたので、処理されません。|  
  
## <a name="explanation"></a>説明  
DBCC がオブジェクトをロックしようとしてデッドロックが発生し、DBCC がデッドロック対象として選択されました。 このオブジェクトは処理されません。  
  
## <a name="user-action"></a>ユーザーの操作  
なし  
  
