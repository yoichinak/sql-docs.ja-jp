---
description: MSSQLSERVER_8712
title: MSSQLSERVER_8712 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 8712 (Database Engine error)
ms.assetid: 292fb3bc-062e-41e4-a566-b5d3d0b21977
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6a443dddc9eadbaa0a032a77d18e5b6dbcaa525b
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99194064"
---
# <a name="mssqlserver_8712"></a>MSSQLSERVER_8712
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|8712|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|USEPLAN_ERR_NO_INDEX|  
|メッセージ テキスト|USE PLAN ヒントで指定したインデックス '%.*ls' が存在しません。 既存のインデックスを指定するか、指定した名前を持つインデックスを作成してください。|  
  
## <a name="explanation"></a>説明  
USE PLAN ヒントで指定したインデックスが存在しません。  
  
## <a name="user-action"></a>ユーザーの操作  
USE PLAN ヒントで指定したすべてのインデックスが存在することを確認します。  
  
## <a name="see-also"></a>参照  
[クエリ ヒント &#40;Transact-SQL&#41;](~/t-sql/queries/hints-transact-sql-query.md)  
[プラン ガイド](~/relational-databases/performance/plan-guides.md)  
  
