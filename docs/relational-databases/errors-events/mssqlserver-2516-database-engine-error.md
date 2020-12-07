---
description: MSSQLSERVER_2516
title: MSSQLSERVER_2516 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2516 (Database Engine error)
ms.assetid: 79ed14b5-f53c-40c6-8334-8a083f732207
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b62b3d0fcf702b25882c0dee3d312d5339e879f6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428784"
---
# <a name="mssqlserver_2516"></a>MSSQLSERVER_2516
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|2516|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC_REPAIR_DIFF_MAP_INVALIDATED|  
|メッセージ テキスト|修復により、データベース NAME の差分ビットマップが無効になりました。 差分バックアップ チェーンが壊れています。 データベース全体をバックアップしてから、差分バックアップを実行できます。|  
  
## <a name="explanation"></a>説明  
この情報メッセージは、エラー MSSQLEngine_2515 の修復時に返されます。  
  
## <a name="user-action"></a>ユーザーの操作  
データベースの完全バックアップを実行します。  
  
## <a name="see-also"></a>参照  
[データベースの完全バックアップの作成 &#40;SQL Server&#41;](~/relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
