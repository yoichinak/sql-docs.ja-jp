---
title: MSSQLSERVER_17132 | Microsoft Docs
description: SQL Server コンピューターはクライアントのログイン パケットを処理できませんでした。 エラーの説明と、考えられる解決策をご確認ください。
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 17132 (Database Engine error)
ms.assetid: d1d198bd-6730-4394-bd5f-28f320c01a38
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 887dde5194364affa8915ab1a30e13220ecb8e2e
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99196772"
---
# <a name="mssqlserver_17132"></a>MSSQLSERVER_17132
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|17132|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|INIT_NODESSPACE|  
|メッセージ テキスト|記述子用のメモリが不足しているので、サーバーのスタートアップに失敗しました。 不要なメモリ負荷を減らすか、システム メモリを増やしてください。|  
  
## <a name="explanation"></a>説明  
サーバー内部の記述子を格納するための十分なメモリの割り当てに失敗しました。  
  
## <a name="user-action"></a>ユーザーの操作  
コンピューターにメモリを追加してください。 一般的なメモリのトラブルシューティング手順を使用できます。  
  
