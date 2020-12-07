---
title: SqlClient でのイベントのトレースの有効化
description: イベント リスナーを実装して SqlClient でイベントのトレースを有効化する方法と、イベント データにアクセスする方法について説明します。
ms.date: 11/23/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: b45f6146f8b5e2f367281720b0fa1c3395d94256
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123964"
---
# <a name="enable-event-tracing-in-sqlclient"></a>SqlClient でのイベントのトレースの有効化

[!INCLUDE [appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE [Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

[Windows イベント トレーシング (ETW)](/windows/win32/etw/event-tracing-portal) は、効率的なカーネル レベルのトレース機能で、デバッグとテストの目的でドライバー定義イベントをログに記録することができます。 SqlClient では、さまざまな情報レベルでの ETW イベントのキャプチャがサポートされています。 イベント トレースのキャプチャを開始するには、クライアント アプリケーションで SqlClient の EventSource 実装からのイベントをリッスンする必要があります。

```
Microsoft.Data.SqlClient.EventSource
```

現在の実装では、次のイベント キーワードがサポートされています。

| キーワード名 | 値 | [説明] |
| ------------ | ----- | ----------- |
| ExecutionTrace | 1 | コマンドの実行前と実行後の Start/Stop イベントのキャプチャをオンにします。 |
| Trace | 2 | 基本的なアプリケーション フロー トレース イベントのキャプチャをオンにします。 |
| Scope | 4 | enter イベントと exit イベントのキャプチャをオンにします |
| NotificationTrace | 8 | `SqlNotification` トレース イベントのキャプチャをオンにします |
| NotificationScope | 16 | `SqlNotification` スコープの enter イベントと exit イベントのキャプチャをオンにします |
| PoolerTrace | 32 | 接続プール フロー トレース イベントのキャプチャをオンにします。 |
| PoolerScope | 64 | 接続プール スコープ トレース イベントのキャプチャをオンにします。 |
| AdvancedTrace | 128 | 高度なフロー トレース イベントのキャプチャをオンにします。 |
| AdvancedTraceBin  | 256 | 追加情報を含む高度なフロー トレース イベントのキャプチャをオンにします。 |
| CorrelationTrace | 512 | 相関関係フロー トレース イベントのキャプチャをオンにします。 |
| StateDump | 1024 | `SqlConnection` の完全な状態ダンプのキャプチャをオンにします |
| SNITrace | 2048 | マネージド ネットワーク実装からのフロー トレース イベントのキャプチャをオンにします (.NET Core でのみ適用可能) |
| SNIScope | 4096 | マネージド ネットワーク実装からのスコープ イベントのキャプチャをオンにします (.NET Core でのみ適用可能) |
|||

## <a name="example"></a>例
次の例では、**AdventureWorks** サンプル データベースでデータ操作のイベント トレースを有効にし、コンソール ウィンドウにそのイベントを表示します。

[!code-csharp [SqlClientEventSource#1](~/../sqlclient/doc/samples/SqlClientEventSource.cs#1)]

## <a name="event-tracing-support-in-native-sni"></a>ネイティブ SNI でのイベント トレースのサポート

**Microsoft.Data.SqlClient** v2.1.0 においては、**Microsoft.Data.SqlClient.SNI** と **Microsoft.Data.SqlClient.SNI.runtime** でのイベント トレースのサポートが拡張されています。 `SqlClientEventSource` に EventCommand を送信することにより、[Xperf](https://docs.microsoft.com/windows-hardware/test/wpt/) および [PerfView](https://github.com/microsoft/perfview) ツールを使用して、ネイティブ SNI.dll 内のイベントを収集できます。 EventCommand の有効な値を以下に示します。

```cs
// Enables trace events:
EventSource.SendCommand(eventSource, (EventCommand)8192, null);

// Enables flow events:
EventSource.SendCommand(eventSource, (EventCommand)16384, null);

// Enables both trace and flow events:
EventSource.SendCommand(eventSource, (EventCommand)(8192 | 16384), null);
```

次の例では、アプリケーションの対象が .NET Framework のときに、ネイティブ SNI.dll でイベント トレースを有効にします。 

```cs
// Native SNI tracing example
// .NET Framework application
using System;
using System.Diagnostics.Tracing;
using Microsoft.Data.SqlClient;

public class SqlClientListener : EventListener
{
    protected override void OnEventSourceCreated(EventSource eventSource)
    {
        if (eventSource.Name.Equals("Microsoft.Data.SqlClient.EventSource"))
        {
            // Enables both trace and flow events
            EventSource.SendCommand(eventSource, (EventCommand)(8192 | 16384), null);
        }
    }
}

class Program
{
    static string connectionString = @"Data Source = localhost; Initial Catalog = AdventureWorks;Integrated Security=true;";

    static void Main(string[] args)
    {
        using (SqlClientListener listener = new SqlClientListener())
        using (SqlConnection connection = new SqlConnection(connectionString))
        {
            connection.Open();
        }        
    }
}
```

### <a name="use-xperf-to-collect-trace-log"></a>Xperf を使用してトレース ログを収集する

1. 次のコマンド ラインを使用してトレースを開始します。

   ```
   xperf -start trace -f myTrace.etl -on *Microsoft.Data.SqlClient.EventSource
   ```
   
2. ネイティブ SNI のトレースの例を実行して、SQL Server に接続します。

3. 次のコマンド ラインを使用してトレースを停止します。

   ```
   xperf -stop trace
   ```
   
4. PerfView を使用して、ステップ 1 で指定した myTrace.etl ファイルを開きます。 SNI トレース ログは、`Microsoft.Data.SqlClient.EventSource/SNIScope` および `Microsoft.Data.SqlClient.EventSource/SNITrace` のイベント名で見つけることができます。 

   ![PerfView を使用して SNI のトレース ファイルを表示する](media/view-event-trace-native-sni.png)


### <a name="use-perfview-to-collect-trace-log"></a>PerfView を使用してトレース ログを収集する

1. PerfView を開始し、メニュー バーから `Collect > Collect` を実行します。

2. トレース ファイル名、出力パス、プロバイダー名を構成します。

   ![収集の前に PerfView を構成する](media/collect-event-trace-native-sni.png)
   
3. 収集を開始します。

4. ネイティブ SNI のトレースの例を実行して、SQL Server に接続します。

5. PerfView から収集を停止します。 ステップ 2 での構成に従って PerfViewData.etl ファイルが生成されるには、しばらく時間がかかります。

6. PerfView で etl ファイルを開きます。 SNI トレース ログは、`Microsoft.Data.SqlClient.EventSource/SNIScope` および `Microsoft.Data.SqlClient.EventSource/SNITrace` のイベント名で見つけることができます。 


## <a name="external-resources"></a>外部リソース  
詳細については、次のリソースを参照してください。  
  
|リソース|説明|  
|--------------|-----------------|  
|[EventSource クラス](/dotnet/api/system.diagnostics.tracing.eventsource)|ETW イベントを作成する機能を提供します。| 
|[EventListener クラス](/dotnet/api/system.diagnostics.tracing.eventlistener)|イベント ソースからのイベントを有効または無効にするメソッドを提供します。|
