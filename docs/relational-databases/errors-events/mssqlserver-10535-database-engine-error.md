---
description: MSSQLSERVER_10535
title: MSSQLSERVER_10535 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 10535 (Database Engine error)
ms.assetid: 478fd978-11d9-4155-8329-f599fdbec14b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 430773e5dcd0d96b8b22359f07fc1ec1a39ffedf
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99197378"
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
  
