---
description: MSSQLSERVER_9790
title: MSSQLSERVER_9790 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 9790 (Database Engine error)
ms.assetid: 83fd379f-5deb-4f97-8cb4-282e3d3fed94
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3ac65e87697c70a72cf62cf7d63bb5332e1f8665
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99187551"
---
# <a name="mssqlserver_9790"></a>MSSQLSERVER_9790
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|9790|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SB3_XMIT_ERROR_ENTRANCE_BROKER_SINGLE_USER|  
|メッセージ テキスト|着信メッセージをルーティングできません。 ルーティング情報を保持するシステム データベース MSDB がシングル ユーザー モードです。|  
  
## <a name="explanation"></a>説明  
MSDB データベースがシングル ユーザー モードであったため、外部から受信したメッセージを分類しようとしたときにエラーが発生しました。  
  
## <a name="user-action"></a>ユーザーの操作  
ALTER DATABASE コマンドを使用して、MSDB をマルチ ユーザー モードに変更します。  
  
