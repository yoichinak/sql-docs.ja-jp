---
description: MSSQLSERVER_10535
title: MSSQLSERVER_10535 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10535 (Database Engine error)
ms.assetid: 478fd978-11d9-4155-8329-f599fdbec14b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1a5c296aa35899b6e73af77abf979a099678819f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88338288"
---
# <a name="mssqlserver_10535"></a>MSSQLSERVER_10535
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|10535|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|PG_NO_PLAN|  
|メッセージ テキスト|プラン ガイド '%.*ls' を作成できません。指定されたプラン ハンドルに対応するプラン キャッシュでプランが見つかりませんでした。 キャッシュされたプラン ハンドルを指定します。 キャッシュされたプラン ハンドルの一覧を取得するには、sys.dm_exec_query_stats 動的管理ビューに対してクエリを実行します。|  
  
## <a name="explanation"></a>説明  
指定されたプラン ハンドルに対応するプラン キャッシュ内にプランが見つかりませんでした。  
  
## <a name="user-action"></a>ユーザーの操作  
キャッシュされたプラン ハンドルを指定します。 キャッシュされたプラン ハンドルの一覧を取得するには、sys.dm_exec_query_stats 動的管理ビューに対してクエリを実行します。  
  
## <a name="see-also"></a>参照  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
