---
description: MSSQLSERVER_32042
title: MSSQLSERVER_32042 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 32042 (Database Engine error)
ms.assetid: 53a51c7a-dcd4-4c15-b4d2-6aaa9dce76da
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5be9f2b0ada229fa469baac3e564a87d4ce8ef4c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494504"
---
# <a name="mssqlserver_32042"></a>MSSQLSERVER_32042
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|32042|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SQLErrorNum32042|  
|メッセージ テキスト|'未送信のログ' の警告が発生しました。 現在の値 '%d' はしきい値 '%d' を上回っています。|  
  
## <a name="explanation"></a>説明  
プリンシパル サーバー インスタンスで発生したこのデータベース ミラーリング イベントは、未送信ログの量がユーザー指定のしきい値に達したことを示しています。 通常は、システム パフォーマンスの変化が原因で発生します。 2 つのシステムを接続する帯域幅が縮小したか、負荷が増加しています。  
  
未送信ログの量は、データ損失の可能性を評価する際に役立つパフォーマンス基準であり、送信されていないログが KB 数で示されます。 この基準は、特に高パフォーマンス モードのセッションに関連があります。 ただし、パートナー間の接続が切断され、ミラーリングが中断している場合は、高度な安全性モードのセッションにも関係します。  
  
## <a name="user-action"></a>ユーザーの操作  
プリンシパル サーバー インスタンス、ミラー サーバー インスタンス、および両者のネットワーク接続の負荷が原因になっているかどうかを調査します。  
  
## <a name="see-also"></a>参照  
[データベース ミラーリング &#40;SQL Server&#41;](~/database-engine/database-mirroring/database-mirroring-sql-server.md)  
[ミラーリング パフォーマンス基準の警告しきい値および警告の使用 &#40;SQL Server&#41;](~/database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
