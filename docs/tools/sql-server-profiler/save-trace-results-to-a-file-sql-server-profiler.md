---
title: トレース結果のファイルへの保存
titleSuffix: SQL Server Profiler
description: SQL Server Profiler で、キャプチャされたイベント データのトレース ファイルへの保存、トレース ファイルの最大サイズの指定、およびファイルのロールオーバー オプションの有効化を行う方法について説明します。
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: ac528747-0c19-4f3d-96f5-44c762a4abed
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: b9cd6bc990ccd82ece2e7a9b9aabb9831fbc8f5b
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100345783"
---
# <a name="save-trace-results-to-a-file-sql-server-profiler"></a>トレース結果のファイルへの保存 (SQL Server Profiler)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

このトピックでは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用して、トレース結果をファイルに保存する方法について説明します。  
  
### <a name="to-save-trace-results-to-a-file"></a>トレース結果をファイルに保存するには  
  
1.  **[ファイル]** メニューの **[新しいトレース]** をクリックし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに接続します。  
  
     **[トレースのプロパティ]** ダイアログ ボックスが表示されます。  
  
    > [!NOTE]  
    >  **[接続の確立直後にトレースを開始する]** チェック ボックスがオンになっている場合、 **[トレースのプロパティ]** ダイアログ ボックスは表示されず、すぐにトレースが開始されます。 この設定を無効にするには、 **[ツール]** メニューの **[オプション]** をクリックし、 **[接続の確立直後にトレースを開始する]** チェック ボックスをオフにします。  
  
2.  **[トレース名]** ボックスに、トレースの名前を入力します。  
  
3.  **[ファイルに保存する]** チェック ボックスをオンにします。  
  
     **[名前を付けて保存]** ダイアログ ボックスが表示されます。  
  
4.  **[名前を付けて保存]** ダイアログ ボックスでパスとファイル名を指定します。 **[保存]** をクリックします。  
  
    > [!NOTE]  
    >  SQL Server サービスに、指定したディレクトリのファイルに対して書き込めるアクセス許可があることを確認します。  
  
5.  **[トレースのプロパティ]** ダイアログ ボックスの **[最大ファイル サイズの設定 (MB)]** ボックスに、ファイルの最大サイズを入力します。 既定値は 5 MB です。  
  
6.  必要に応じて、次のオプションを指定します。  
  
    -   **[ファイル ロールオーバーを有効にする]** チェック ボックスをオンにすると、最大ファイル サイズに達したとき、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] によりトレース データ用の新しいファイルが作成されます。 既定では、このオプションはオンになっています。  
  
    -   **[サーバーがトレース データを処理する]** チェック ボックスをオンにすると、サーバーにより、すべてのトレース イベントが記録されます。  
  
        > [!NOTE]  
        >  **[サーバーがトレース データを処理する]** チェック ボックスをオフにすると、イベントを記録することが原因でパフォーマンスが大幅に低下する場合、イベントは記録されなくなります。  
  
## <a name="see-also"></a>参照  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
