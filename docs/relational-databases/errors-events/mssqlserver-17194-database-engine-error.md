---
description: MSSQLSERVER_17194
title: MSSQLSERVER_17194 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "17194"
helpviewer_keywords:
- 17194 (Database Engine error)
ms.assetid: 0d03eb20-28a7-4ceb-8903-7f9420a620f7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e6d652da7734e8ad5819ed8e5e84a8d27787cf48
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482846"
---
# <a name="mssqlserver_17194"></a>MSSQLSERVER_17194
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|17194|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名||  
|メッセージ テキスト|サーバーはログインに必要な SSL プロバイダーを読み込めませんでした。接続が閉じられました。 SSL は、管理者が行ったサーバーの構成方法に応じて、ログイン シーケンスの暗号化またはすべての通信の暗号化に使用されます。 エラー メッセージ(0xXXXX) の詳細については、オンライン ブックを参照してください。 [CLIENT:11.11.11.11]|  
  
## <a name="explanation"></a>説明  
このエラーは、クライアントが接続を閉じたことを示しています。 このエラーは、接続のタイムアウトが原因で発生した可能性があります。 エラー メッセージにはオペレーティング システムで生成された値が表示されます。この値で、原因となっている問題を確認できます。  
  
## <a name="user-action"></a>ユーザーの操作  
メッセージ内のエラー コードが 0x2746 (10 進値では 10054) の場合、接続がクライアントによってリセットされたことを意味します。通常はタイムアウトが原因です。エラーを解決するには、クライアントまたは呼び出し側のプログラムで接続のタイムアウトを増やします。  
  
エラー メッセージにその他の値が示されている場合、解決方法を確認するには、オペレーティング システム コマンド **net helpmsg** を実行します (実行時に、エラー コードの 10 進値を指定します)。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続する方法の詳細については、「[Server Network Configuration](~/database-engine/configure-windows/server-network-configuration.md)」 (サーバー ネットワークの構成) と「[Client Network Configuration](~/database-engine/configure-windows/client-network-configuration.md)」 (クライアント ネットワーク構成) を参照してください。  
  
## <a name="internal-only"></a>内部使用のみ  
