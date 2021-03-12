---
title: SqlClient トラブルシューティング ガイド
description: よく見られる問題の解決方法について説明するページです。
ms.date: 03/03/2021
dev_langs:
- csharp
- vb
ms.assetid: 6f5ff56a-a57e-49d7-8ae9-bbed697e42e3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-jizho2
ms.openlocfilehash: 725d1522f98e721f581a7d4b7614181fd2632962
ms.sourcegitcommit: 15c7cd187dcff9fc91f2daf0056b12ed3f0403f0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2021
ms.locfileid: "102464805"
---
# <a name="sqlclient-troubleshooting-guide"></a>SqlClient トラブルシューティング ガイド

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

## <a name="exceptions-when-connecting-to-sql-server"></a>SQL Server への接続時に発生する例外

接続の確立に失敗する理由はさまざまです。 その問題の多くを分析して解決するためのガイドとして使用できるトラブルシューティングのヒントを以下に示します。

### <a name="unable-to-load-native-sni-server-name-indication-library"></a>ネイティブ SNI (Server Name Indication) ライブラリを読み込めない

#### <a name="issues-in-net-framework-applications"></a>.NET Framework アプリケーションの問題

観察されたスタックトレース:

```log
TypeInitializationException: The type initializer for 'Microsoft.Data.SqlClient.SNILoadHandle' threw an exception.
DllNotFoundException: Unable to load DLL 'Microsoft.Data.SqlClient.SNI.x64.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)
```

```log
TypeInitializationException: The type initializer for 'Microsoft.Data.SqlClient.SNILoadHandle' threw an exception.
DllNotFoundException: Unable to load DLL 'Microsoft.Data.SqlClient.SNI.x86.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)
```

SNI は、Windows 上での実行時にさまざまなネットワーク操作を行うために SqlClient が依存するネイティブ C++ ライブラリです。 MSBuild プロジェクト SDK を使用してビルドされた .NET Framework アプリケーションの場合、ネイティブ DLL は復元コマンドを使用して管理されません。 そのため、".targets" ファイルが、必要な "コピー" 操作を定義する "Microsoft.Data.SqlClient.SNI" NuGet パッケージに含まれます。

"Microsoft.Data.SqlClient" ライブラリに対して直接的な依存関係が作成された場合、含まれている ".targets" ファイルは自動的に参照されます。 推移的な (間接的な) 参照が行われるシナリオでは、この ".targets" ファイルを手動で参照し、必要に応じて "コピー" 操作を実行できるようにする必要があります。

**推奨される解決策:** "コピー" 操作が実行されるように、".targets" ファイルがアプリケーションの ".csproj" ファイルで参照されていることを確認してください。

これらのターゲットには、Microsoft のよく知られている、一般的に使用されているターゲットのみが含まれます。 外部のツールまたはアプリケーションによってバイナリをコピーするカスタム ターゲットが定義されている場合は、ツールの管理者が新しいターゲットを定義して、ネイティブ SNI DLL が Microsoft.Data.SqlClient.dll バイナリと共にコピーされ、クライアント アプリケーションの実行時に使用できるようにする必要があります。

#### <a name="issues-in-net-core-applications"></a>.NET Core アプリケーションの問題

観察されたスタックトレース:

```log
System.TypeInitializationException: The type initializer for 'Microsoft.Data.SqlClient.TdsParser' threw an exception.
---> System.TypeInitializationException: The type initializer for 'Microsoft.Data.SqlClient.SNILoadHandle' threw an exception.
---> System.DllNotFoundException: Unable to load shared library 'Microsoft.Data.SqlClient.SNI.dll' or one of its dependencies.
```

> [!NOTE]
> このエラーは、Windows アプリケーションでのみ発生する可能性があります。 これが Unix 環境で発生する場合は、ご自分のアプリケーションが Windows ではなく Unix ランタイムを適切にターゲットとするように構築されていることを確認する必要があります。

SNI は、Windows 上での実行時にさまざまなネットワーク操作を行うために SqlClient が依存するネイティブ C++ ライブラリです。 Microsoft.Data.SqlClient では、.NET Core でのこのライブラリの読み込みとアンロードが管理されません。

**推奨される解決策:** ネイティブ ランタイム ライブラリが .NET Core プロセスに読み込まれるファイルシステムに "実行" アクセス許可が付与されていることを確認します。 それでも問題が解決しない場合は、[dotnet/runtime](https://github.com/dotnet/runtime) リポジトリにイシューを報告して、さらにサポートを求めることができます。

#### <a name="native-sni-pdb-not-found-errors"></a>ネイティブ SNI (pdb が見つからない) エラー

観察されたスタックトレース:

```log
An assembly specified in the application dependencies manifest (sql2csv.deps.json) was not found:
  package: 'Microsoft.Data.SqlClient.SNI.runtime', version: '2.0.0'
  path: 'runtimes/win-x64/native/Microsoft.Data.SqlClient.SNI.pdb'
```

**推奨される解決策:** クライアント アプリケーションでバージョン [v2.1.0](https://www.nuget.org/packages/Microsoft.Data.SqlClient/2.1.0) 以上の Microsoft.Data.SqlClient パッケージが参照されていることを確認します。 EF Core を使用する場合は、このパッケージ バージョンの Microsoft.Data.SqlClient への参照を直接追加して依存関係をオーバーライドしてください。

### <a name="hostname-resolution-errors"></a>ホスト名の解決エラー

観察されたスタックトレース:

```log
Microsoft.Data.SqlClient.SqlException (0x80131904): A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible.
Verify that the instance name is correct and that SQL Server is configured to allow remote connections.
(provider: TCP Provider, error: 0 - No such host is known.)
```

```log
Microsoft.Data.SqlClient.SqlException (0x80131904): A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible.
Verify that the instance name is correct and that SQL Server is configured to allow remote connections.
(provider: TCP Provider, error: 35 - An internal exception was caught)
```

```log
Microsoft.Data.SqlClient.SqlException (0x80131904): A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible.
Verify that the instance name is correct and that SQL Server is configured to allow remote connections.
(provider: TCP Provider, error: 35 - An internal exception was caught)
 ---> System.Net.Internals.SocketExceptionFactory+ExtendedSocketException (00000005, 0xFFFDFFFF): Name does not resolve
```

#### <a name="possible-reasons"></a>考えられる原因

- TCP および名前付きパイプ プロトコルが SQL Server 上で有効になっていない

  **推奨される解決策:** SQL Server 構成マネージャー コンソールから、TCP および名前付きパイプ プロトコルを SQL Server 上で有効にします。

- ホスト名が不明

  **推奨される解決策:** 接続が開始されているクライアントから、ホスト名がサーバーの IP アドレスに解決されることを確認します。


### <a name="login-phase-errors"></a>ログイン フェーズのエラー

観察されたスタックトレース:

```log
Microsoft.Data.SqlClient.SqlException (0x80131904): A connection was successfully established with the server, but then an error occurred during the pre-login handshake.
(provider: SSL Provider, error: 31 - Encryption(ssl/tls) handshake failed)
System.IO.EndOfStreamException: End of stream reached
```

```log
A connection was successfully established with the server, but then an error occurred during the login process.
(provider: SSL Provider, error: 0 - The target principal name is incorrect.)
```

```log
Microsoft.Data.SqlClient.SqlException (0x80131904): Connection Timeout Expired. The timeout period elapsed during the post-login phase. The connection could have timed out while waiting for server to complete the login process and respond; Or it could have timed out while attempting to create multiple active connections.
The duration spent while attempting to connect to this server was - [Pre-Login] initialization=837; handshake=394; [Login] initialization=3; authentication=15; [Post-Login] complete=1027;
---> System.ComponentModel.Win32Exception (258): Unknown error 258
at Microsoft.Data.SqlClient.SqlInternalConnection.OnError(SqlException exception, Boolean breakConnection, Action1 wrapCloseInAction)
```

#### <a name="possible-reasons-and-solutions"></a>考えられる原因と解決策

- SQL Server で TLS 1.2 がサポートされていない

  通常、このエラーは、TLS 1.2 がサポートされている最低限の TLS プロトコルである Docker イメージ コンテナー、Unix クライアント、または Windows クライアントなどのクライアント環境で発生します。

  **推奨される解決策:** サポートされているバージョンの SQL Server <sup>1</sup> に最新の更新プログラムをインストールし、そのサーバーで TLS 1.2 プロトコルが有効になっていることを確認します。

  " _<sup>1</sup> サポートされている SQL Server のバージョンと Microsoft.Data.SqlClient のさまざまなバージョンの一覧については、「[SqlClient ドライバーのサポート ライフサイクル](sqlclient-driver-support-lifecycle.md)」を参照してください。_ "

  **安全でないソリューション:** TLS 1.0 を使用して接続するように Docker イメージまたはクライアント環境で TLS/SSL 設定を構成します。

  ```docker
  MinProtocol = TLSv1
  CipherString = DEFAULT@SECLEVEL=1
  ```

  > [!NOTE]
  > TLS 1.0 または TLS 1.1 を使用する Windows または Linux 環境から Microsoft.Data.SqlClient v2.0 以上を使用して接続する場合、ターゲットの SQL Server とクライアントが接続の確立時に最小の TLS バージョン 1.2 をネゴシエートできないと、セキュリティ警告メッセージがスローされます: `Security Warning: The negotiated <TLS1.0 | TLS1.1> is an insecure protocol and is supported for backward compatibility only. The recommended protocol version is TLS 1.2 and later.`

- SQL Server による暗号化の強制

  ターゲット サーバーが、[強制的に暗号化] プロパティがオンになっている Azure SQL インスタンスまたはオンプレミスの SQL Server であった場合、暗号化された接続が確立され、それに対してクライアントはサーバーとの信頼関係を確立する必要があります。

  **推奨される解決策:** この問題を解決するには、次の 2 つのオプションを使用できます。

    1. クライアント環境に、ターゲット SQL Server の TLS/SSL 証明書をインストールする。 暗号化が必要な場合は検証されます。
    2. 接続文字列で "Trust Server Certificate = true" プロパティを設定する。

  **安全でないソリューション:** SQL Server の [強制的に暗号化] 設定を無効にします。

- TLS/SSL 証明書が SHA-256 以上で署名されていない。

  **推奨される解決策:** SHA-256 以上のハッシュ アルゴリズムを使用してハッシュが署名されているサーバーの新しい TLS/SSL 証明書を生成します。

- Linux と .NET 5 以降での厳密に制限された暗号スイート

  .NET 5 で導入された Linux クライアントに関する破壊的変更では、許可されている暗号スイートの厳密に制限された一覧が既定で使用されます。 `CipherSuitePolicy` 値を指定するか、_OpenSSL_ の構成ファイルを変更することにより、レガシ クライアントが許可されるように (またはレガシ サーバーに接続できるように) 既定の暗号スイートの一覧を増やすことが必要になる場合があります。
  
  推奨される操作の詳細については、「[Linux 上の .NET 用の既定の TLS 暗号スイート](/dotnet/core/compatibility/cryptography/5.0/default-cipher-suites-for-tls-on-linux)」を参照してください。

### <a name="connection-pool-exhaustion-errors"></a>接続プール不足のエラー

観察されたスタックトレース:

```log
System.InvalidOperationException: Timeout expired. The timeout period elapsed prior to obtaining a connection from the pool.
This may have occurred because all pooled connections were in use and max pool size was reached.
```

#### <a name="possible-reasons-and-solutions"></a>考えられる原因と解決策

クライアント アプリケーションによって、特定の時点で接続プールがアクティブに保持できるよりも多くの接続が開かれています。

**推奨される解決策:** [最大プール サイズ] 接続プロパティをより高い値に設定し、使用されていない接続を適切なタイミングで閉じます。

## <a name="contact-support"></a>サポートに問い合わせる

このガイドで接続の問題が解決しない場合は、[dotnet/sqlclient](https://github.com/dotnet/SqlClient) リポジトリで既存のイシューを参照し、必要に応じて新しいイシューを作成することができます。
