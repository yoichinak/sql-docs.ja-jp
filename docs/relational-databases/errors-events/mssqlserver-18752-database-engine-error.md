---
description: MSSQLSERVER_18752
title: MSSQLSERVER_18752 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 18752 (Database Engine error)
ms.assetid: 234c58d8-7a1e-4b07-a64b-32a311527980
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 51d1c0e130e0bada6601a9ef10875108da2f233a
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99196492"
---
# <a name="mssqlserver_18752"></a>MSSQLSERVER_18752
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|18752|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|REPL_INUSE|  
|メッセージ テキスト|同時にデータベースに接続できるログ リーダー エージェントまたはログ関連のプロシージャ (sp_repldone、sp_replcmds、および sp_replshowcmds) は 1 つだけです。 ログ関連のプロシージャを実行した場合、そのプロシージャが実行された接続を削除するか、その接続に対して sp_replflush を実行してから、ログ リーダー エージェントを開始するか、別のログ関連のプロシージャを実行してください。|  
  
## <a name="explanation"></a>説明  
同時にデータベースに接続できるログ リーダー エージェントまたはログ関連のプロシージャは 1 つだけです。  
  
## <a name="user-action"></a>ユーザーの操作  
同じパブリッシング データベースに対して他のログ リーダーが実行されていないこと、および sp_replcmds/sp_repltrans/sp_repldone を実行した後に、running sp_replflush を実行していない、または切断していないアクティブな接続が他にないことを確認します。  
  
