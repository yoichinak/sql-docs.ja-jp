---
description: MSSQLSERVER_3413
title: MSSQLSERVER_3413 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 3413 (Database Engine error)
ms.assetid: 3fa07637-ba93-4633-aaf2-ade7d18bc487
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 14420a895991a4ea9ed1cc7dc259ac16ad55dead
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99197772"
---
# <a name="mssqlserver_3413"></a>MSSQLSERVER_3413
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|3413|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|MARKDB|  
|メッセージ テキスト|データベース ID %d。 データベースを問題ありに設定できませんでした。 sys.databases.database_id での Getnext NC スキャンが失敗しました。 エラー ログで以前のエラーを参照して原因を特定し、関連している問題をすべて修正してください。|  
  
## <a name="explanation"></a>説明  
カタログ内で、ユーザー データベースを SUSPECT に設定しようとして、予期しないエラーが発生しました。 SUSPECT 状態は保存されません。  
  
## <a name="user-action"></a>ユーザーの操作  
これより前に発生したエラーを調べて、問題を修正します。  
  
