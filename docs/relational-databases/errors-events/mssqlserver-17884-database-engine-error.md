---
description: MSSQLSERVER_17884
title: MSSQLSERVER_17884 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 17884 (Database Engine error)
ms.assetid: 8d05ba05-3f71-4dc3-bd81-2ea5ac9fe843
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5e81871694060414d0f3fdf24fde05b01d0b13d8
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99196596"
---
# <a name="mssqlserver_17884"></a>MSSQLSERVER_17884
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|17884|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SRV_SCHEDULER_DEADLOCK|  
|メッセージ テキスト|ノード %d のプロセスに割り当てられた新しいクエリが、この %d 秒間ワーカー スレッドで選択されませんでした。 クエリのブロックまたは長時間実行をこの条件に含めることができますが、クライアントの応答時間が低下する可能性があります。 "max worker threads" 構成オプションを使用して使用可能なスレッド数を増やすか、現在実行中のクエリを最適化してください。  SQL プロセス使用率: %d%%。 システムのアイドル状態: %d%%。|  
  
## <a name="explanation"></a>説明  
各スケジューラで処理の進行が示されません。デッドロックが原因である可能性があり、その場合、スレッドは進行せず、新しい作業は選択されず処理されません。 プロセス使用率が低い場合は、コンピューター上の他のプロセスによってサーバー プロセスの CPU 不足が発生している可能性があります。  
  
## <a name="user-action"></a>ユーザーの操作  
ブロックが発生して処理が進行していない理由を特定し、それに応じて状況に対処します。 プロセス使用率が低い場合は、他のプロセスによって発生しているシステムへの負荷を確認します。  
  
