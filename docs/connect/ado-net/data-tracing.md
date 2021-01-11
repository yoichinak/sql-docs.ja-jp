---
title: SqlClient でのデータ トレース
description: Microsoft SqlClient Data Provider for SQL Server によって組み込みのデータ トレース機能が提供される方法について説明します。
ms.date: 12/04/2020
ms.assetid: a6a752a5-d2a9-4335-a382-b58690ccb79f
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: fc8b5a7ca06af3c3e3ea83fcb747f79517e5ef7a
ms.sourcegitcommit: 4419e99d77ee2c73f9da1559c7944f7702f2de30
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/23/2020
ms.locfileid: "97744437"
---
# <a name="data-tracing-in-sqlclient"></a>SqlClient でのデータ トレース

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

.NET には、Microsoft SqlClient Data Provider for SQL Server と SQL Server ネットワーク プロトコルによってサポートされている組み込みのデータ トレーシング機能が搭載されています。

データ アクセス API 呼び出しのトレースは、次の問題を診断する際に役立ちます。

- クライアント プログラムとデータベース間のスキーマの不一致

- データベースの使用不可またはネットワーク ライブラリの問題

- 誤った SQL がアプリケーションによりハードコーディングまたは生成された

- プログラミング ロジックが不適切

- Microsoft SqlClient Data Provider for SQL Server と独自のコンポーネントの間の相互作用に起因する問題。

トレースを拡張することにより異なるトレース技術をサポートできます。このため、開発者はアプリケーション スタックのあらゆるレベルで問題をトレースできます。 Microsoft SqlClient Data Provider for SQL Server では、一般化されたトレースおよびインストルメンテーション API を利用します。

.NET におけるマネージド トレースの設定と構成の詳細については、「[データ アクセスのトレース](/previous-versions/sql/sql-server-2012/hh880086(v=msdn.10))」を参照してください。

## <a name="access-diagnostic-information-in-the-extended-events-log"></a>拡張イベント ログの診断情報へのアクセス

Microsoft SqlClient Data Provider for SQL Server では、[データ アクセスのトレース](/previous-versions/sql/sql-server-2012/hh880086(v=msdn.10))により、拡張イベント ログのサーバーの接続のリング バッファーやアプリケーションのパフォーマンス情報から、接続の障害などのクライアントのイベントを診断情報と関連付けることを容易にします。 拡張イベント ログを表示する方法については、「[イベント セッション データの表示](/previous-versions/sql/sql-server-2012/hh710068(v=sql.110))」を参照してください。

接続操作では、Microsoft SqlClient Data Provider for SQL Server によってクライアント接続 ID が送信されます。 接続に失敗した場合は、接続リング バッファー ([接続リング バッファーによる SQL Server 2008 での接続トラブルシューティング](/archive/blogs/sql_protocols/connectivity-troubleshooting-in-sql-server-2008-with-the-connectivity-ring-buffer)に関する記事を参照) にアクセスし、`ClientConnectionID` フィールドを見つけて、接続エラーに関する診断情報を取得することができます。 クライアント接続 ID は、エラーが発生した場合にのみリング バッファーに記録されます。 ログイン前のパケットを送信する前に接続に失敗した場合、クライアント接続 ID は生成されません。 クライアント接続 ID は 16 バイトの GUID です。 拡張イベント セッション内のイベントに `client_connection_id` アクションが追加された場合にも、拡張イベントのターゲット出力のクライアント接続 ID を見つけることができます。 それ以上にクライアントのドライバーの診断について支援が必要な場合は、データ アクセスのトレースを有効にし、接続コマンドを再実行して、データ アクセスのトレースの `ClientConnectionID` フィールドを確認することができます。

`SqlConnection.ClientConnectionID` プロパティを使用して、クライアント接続 ID をプログラムによって取得できます。

> [!NOTE]
> Microsoft SqlClient Data Provider for SQL Server では、バージョン 2.1.0 以降のサーバー プロセス ID をサポートしています。 これは、`SqlConnection.ServerProcessId` プロパティを使用してプログラムで取得できます。

`ClientConnectionID` と `ServerProcessId` は、正常に接続を確立する <xref:Microsoft.Data.SqlClient.SqlConnection> オブジェクトで使用できます。 接続試行が失敗すると、`ClientConnectionID` は `SqlException.ToString` を通じて利用可能になることがあります。

また、Microsoft SqlClient Data Provider for SQL Server では、スレッド固有のアクティビティ ID も送信されます。 TRACK_CAUSALITY オプションが有効な状態でセッションが開始された場合、アクティビティ ID は拡張イベントのセッションでキャプチャされます。 アクティブな接続のパフォーマンスの問題については、クライアントのデータ アクセスのトレース (`ActivityID` フィールド) からアクティビティ ID を取得した後、その拡張イベントの出力のアクティビティ ID を検索できます。 拡張イベント内のアクティビティ ID は、16 バイトの GUID (クライアント接続 ID の GUID とは異なる) の後に 4 バイトのシーケンス番号が付いたものです。 シーケンス番号は、スレッド内で要求の順序を表し、スレッドのバッチと RPC ステートメントの相対的順序を示します。 `ActivityID` は、現在、データ アクセスのトレースが有効な場合、データ アクセスのトレースの構成のワードの 18 番目のビットが有効にされると、オプションとして SQL のバッチ ステートメントと RPC の要求に送信されるようになっています。

次の SQL ステートメントは、Transact-SQL を使用して拡張イベント セッションを開始するサンプルです。このセッションはリング バッファーに保存され、RPC およびバッチ操作でクライアントから送信されたアクティビティ ID が記録されます。

```sql
create event session MySession on server
add event connectivity_ring_buffer_recorded,
add event sql_statement_starting (action (client_connection_id)),
add event sql_statement_completed (action (client_connection_id)),
add event rpc_starting (action (client_connection_id)),
add event rpc_completed (action (client_connection_id))
add target ring_buffer with (track_causality=on)
```

## <a name="see-also"></a>関連項目
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
