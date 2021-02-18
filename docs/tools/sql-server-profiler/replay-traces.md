---
title: トレースの再生
titleSuffix: SQL Server Profiler
description: 1 台のコンピューターからの SQL Server Profiler のデータを再生する方法と、再生でブレークポイントとシミュレートされたユーザー接続を使用して問題をトラブルシューティングする方法を確認します。
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: da958d3c-7f3e-44c9-aecc-8a9493bea7c0
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 52da7b97159ed6c7ca85d63afab6b6b3dbb92934
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100335878"
---
# <a name="replay-traces"></a>トレースの再生

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

再生とは、トレースでキャプチャされたアクティビティを再現する機能です。 トレースの作成または編集を行うときに、そのトレースをファイルに保存して後で再生できます。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用して、1 つのコンピューターからのトレース アクティビティを再生できます。 ワークロードが大きい場合、Distributed Replay Utility を使用して複数のコンピューターからのトレース データを再生できます。  
  
 このセクションでは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]の再生機能の使用方法について説明します。 Distributed Replay Utility の詳細については、「 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)」を参照してください。  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] には、ユーザー接続と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証をシミュレートできるマルチスレッド再生エンジンが備わっています。 再生は、アプリケーションまたはプロセスに関する問題のトラブルシューティングを行う際に役立ちます。 問題を特定して修正を実装したら、発生する可能性がある問題を検出したトレースを、修正されたアプリケーションまたはプロセスに対して実行します。 その後、元のトレースを再生し、結果を比較します。  
  
 トレースの再生では、[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] の **[再生]** メニューの **[ブレークポイントの設定/解除]** や **[カーソルまで実行]** オプションを使用したデバッグがサポートされます。 これらのオプションでは、長いスクリプトを段階的に分析できるように、トレースの再生を短いセグメントに分割できるので、長いスクリプトの分析が特に強化されます。  
  
 トレースの再生に必要な権限については、「 [SQL Server Profiler の実行に必要な権限](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[再生を実行するための必要条件](../../tools/sql-server-profiler/replay-requirements.md)|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]で再生できるようにトレース定義に含める必要があるイベントについて説明します。|  
|[再生オプション &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-options-sql-server-profiler.md)|**の** [構成の再生] [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]ダイアログ ボックスで設定できるオプションについて説明します。|  
|[トレースの再生に関する注意点 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/considerations-for-replaying-traces-sql-server-profiler.md)|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] で再生できないトレース イベント、およびトレースの再生によるサーバー パフォーマンスへの影響について説明します。|  
  
## <a name="see-also"></a>参照  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)  
  
  
