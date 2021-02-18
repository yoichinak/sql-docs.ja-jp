---
title: インストール後の手順の実行
titleSuffix: SQL Server Distributed Replay
description: 分散再生をインストールした後、分散再生コントローラー サービスおよび分散再生クライアント サービスのアカウントを変更する必要があります。
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 0a788a2a-9b4f-4bfc-b1b5-83eeb1ea9ab2
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 94cf69eb0a4159c4bfda5a0ef0b79a2b35bbfcb7
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100349545"
---
# <a name="complete-the-post-installation-steps"></a>インストール後の手順の実行

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

分散再生をインストールした後、分散再生コントローラー サービスおよび分散再生クライアント サービスのアカウントを変更する必要があります。  
  
## <a name="to-complete-the-post-installation-steps"></a>インストール後の手順を実行するには  
  
1. **ファイアウォール規則を作成する**:コントローラー コンピューターとクライアント コンピューターで、対応するサービスのファイアウォール経由の受信トラフィックを許可する必要があります。 インストール フォルダーに配置されているサービス実行可能ファイルのファイアウォール ルールを指定します。  
  
    1. コントローラー サービスの場合は、インストール フォルダーにある **DReplayController.exe** のルールを作成します。 たとえば、次のコマンドを実行すると、このルールが有効になります ( `%InstallPath%` はサービスのインストール フォルダーです)。  
  
         `netsh advfirewall firewall add rule name="allow dreplay controller" dir=in program="%InstallPath%\DReplayController\DReplayController.exe" action=allow`  
  
    2. クライアント サービスの場合は、クライアント コンピューターごとに、インストール フォルダーにある **DReplayClient.exe** のルールを作成します。 たとえば、次のコマンドを実行すると、このルールが有効になります ( `%InstallPath%` はサービスのインストール フォルダーです)。  
  
         `netsh advfirewall firewall add rule name="allow dreplay client" dir=in program="%InstallPath%\DReplayClient\DReplayClient.exe" action=allow`  
  
2. **ターゲット サーバーで各クライアントの権限を与える**:クライアント コンピューターへのクライアント サービスのインストールが完了したら、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のターゲット インスタンスの sysadmin ロールにクライアント サービス アカウントを手動で追加する必要があります。  
  
## <a name="net-framework-security"></a>.NET Framework のセキュリティ

分散再生の機能をインストールするには、管理権限が必要です。 sysadmin 権限を持つ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインのみが、テスト サーバーの sysadmin サーバー ロールにクライアント サービス アカウントを追加できます。 Distributed Replay のセキュリティ上の考慮事項の詳細については、「 [Distributed Replay のセキュリティ](../../tools/distributed-replay/distributed-replay-security.md)」を参照してください。