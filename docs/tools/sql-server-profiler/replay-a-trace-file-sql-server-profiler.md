---
title: トレース ファイルを再生する
titleSuffix: SQL Server Profiler
description: SQL Server Profiler でトレース ファイルを再生し、問題解決に役立てます。 再生の機能とオプションについて説明します。
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 9e361275-c8fd-4499-8389-242cf8e27415
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: b7d6139941e7ee3b80e62596e95f0d5d492cbc1d
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100349379"
---
# <a name="replay-a-trace-file-sql-server-profiler"></a>トレース ファイルの再生 (SQL Server Profiler)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

再生は、保存したトレースを開いて再実行する機能です。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] には、ユーザー接続と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証をシミュレートできるマルチスレッド再生エンジンが備わっています。 再生は、アプリケーションまたはプロセスに関する問題のトラブルシューティングを行う際に役立ちます。 問題を特定して修正を実装したら、修正されたアプリケーションまたはプロセスに対して、発生する可能性のある問題を検出したトレースを実行します。 その後、元のトレースを再生し、結果を比較します。  
  
 再生を有効にするには、監視する他のイベント クラスに加えて、特定のイベント クラスをキャプチャする必要があります。 **TSQL_Replay** トレース テンプレートを使用すると、これらのイベントが既定でキャプチャされます。 詳細については、「 [再生を実行するための必要条件](../../tools/sql-server-profiler/replay-requirements.md)」を参照してください。  
  
### <a name="to-replay-a-trace-file"></a>トレース ファイルを再生するには  
  
1.  **[ファイル]** メニューの **[開く]** をポイントし、 **[トレース ファイル]** をクリックします。 再生に必要なイベント クラスが含まれたトレース ファイルを選択します。  
  
2.  **[再生]** メニューの **[開始]** をクリックし、トレースを再生するサーバー インスタンスに接続します。  
  
3.  **[構成の再生]** ダイアログ ボックスの **[再生オプションの基本設定]** タブで、 **[再生サーバー]** を指定します。 **[再生サーバー]** ボックスに表示されているサーバーを変更するには、 **[変更]** をクリックします。  
  
4.  必要に応じて、再生の保存先として次のいずれかを選択します。  
  
    -   **[ファイルに保存]** : 再生の保存先となるファイルを指定します。  
  
    -   **[テーブルに保存]** : 再生の保存先となるデータベース テーブルを指定します。  
  
5.  **[トレースされた順番にイベントを再生します。このオプションはデバッグを有効にします。]** または **[複数のスレッドを使用してイベントを再生します。このオプションはパフォーマンスを最適にし、デバッグを無効にします。]** のいずれかを選択します。 次の表では、これらの設定の違いについて説明します。  
  
    |オプション|説明|  
    |------------|-----------------|  
    |**[トレースされた順番にイベントを再生します。このオプションはデバッグを有効にします。]**|記録された順番にイベントを再生します。 このオプションにより、デバッグが有効になります。|  
    |**[複数のスレッドを使用してイベントを再生します。このオプションはパフォーマンスを最適にし、デバッグを無効にします。]**|このオプションでは、複数のスレッドを使用して、順序に関係なく各イベントを再生します。 このオプションにより、パフォーマンスが最適化されます。|  
  
6.  **[再生結果を表示する]** チェック ボックスをオンにすると、実行時に再生が表示されます。  
  
7.  必要に応じて、 **[再生オプションの詳細設定]** タブをクリックし、次のオプションを構成します。  
  
    -   すべてのサーバー プロセス ID (SPID) を再生するには、 **[システム SPID を再生する]** チェック ボックスをオンにします。  
  
    -   特定の SPID に属しているプロセスに再生を制限するには、 **[1 つの SPID のみ再生する]** チェック ボックスをオンにします。 **[再生する SPID]** ボックスには、SPID を入力します。  
  
    -   特定の期間に発生したイベントを再生するには、 **[日時により再生を制限する]** チェック ボックスをオンにします。 **[開始時刻]** と **[終了時刻]** の日時を選択し、再生に含める期間を指定します。  
  
    -   再生中の SQL Server によるプロセスの管理方法を制御するには、 **[ヘルス モニター オプション]** を構成します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Profiler の実行に必要な権限](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)   
 [トレースの再生](../../tools/sql-server-profiler/replay-traces.md)   
 [トレース ファイルを開く &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
