---
description: MSSQLSERVER_5245
title: MSSQLSERVER_5245 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 5245 (Database Engine error)
ms.assetid: 6005c9ec-ccdd-4def-9eb4-37cdb599ddb3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: fa96d1199c33f751dc0e49da396316b21a4f1434
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99198102"
---
# <a name="mssqlserver_5245"></a>MSSQLSERVER_5245
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|5245|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC4_TABLE_LOCK_TIMEOUT_EXCEEDED|  
|メッセージ テキスト|オブジェクト ID O_ID (オブジェクト 'NAME'):DBCC ではこのオブジェクトをロックできませんでした。ロック要求がタイムアウトしました。 このオブジェクトはスキップされたので、処理されません。|  
  
## <a name="explanation"></a>説明  
DBCC が、指定されたオブジェクト用にテーブルのロック獲得を待機している間に、ロック要求のタイムアウトが発生しました。  
  
## <a name="user-action"></a>ユーザーの操作  
DBCC コマンドを再実行します。  
  
