---
title: SqlClient の AppContext スイッチ
description: SqlClient 内で提供されている AppContext スイッチの使用方法について説明します。
ms.date: 06/15/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: 8704cb5bf6492fc90f90344103359abdd7a32e2e
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081511"
---
# <a name="appcontext-switches-in-sqlclient"></a>SqlClient の AppContext スイッチ

[!INCLUDE [Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

AppContext クラスを使用すれば、SqlClient によって、以前の動作に依存する呼び出し元を引き続きサポートしながら、新しい機能を提供することができます。 ユーザーは、特定の AppContext スイッチを設定することによって、動作の変更をオプトアウトすることができます。

## <a name="enabling-decimal-truncation-behavior"></a>小数点の切り捨て動作の有効化

[!INCLUDE [appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

Microsoft.Data.SqlClient 2.0 以降では、SQL Server の場合と同様に、既定では 10 進データが丸められます。 以前の切り捨て動作を有効にするには、アプリケーションの起動時に、AppContext スイッチ **"Switch.Microsoft.Data.SqlClient.TruncateScaledDecimal"** を `true` に設定します。

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.TruncateScaledDecimal", true);
```

## <a name="enabling-managed-networking-on-windows"></a>Windows でのマネージド ネットワークの有効化

[!INCLUDE [appliesto-xxxx-netcore-netst-md](../../includes/appliesto-xxxx-netcore-netst-md.md)]

Windows 上の SqlClient では既定では SNI ネットワーク インターフェイスのネイティブ実装が使用されます。 マネージド SNI 実装を使用できるようにするには、アプリケーションの起動時に AppContext スイッチ **"Switch.Microsoft.Data.SqlClient.UseManagedNetworkingOnWindows"** を `true` に設定します。

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.UseManagedNetworkingOnWindows", true);
```

このスイッチにより、Windows 上の .NET Core 2.1 以降および .NET Standard 2.0 以降のプロジェクトにおいてマネージド ネットワーク実装を使用するようにドライバーの動作が切り替えられます。それにより、Microsoft.Data.SqlClient ライブラリのネイティブ ライブラリに対するすべての依存関係が削除されます。 これは、テストおよびデバッグのみを目的としています。

> [!NOTE]
> ネイティブ実装と比較すると、いくつかの既知の相違点があります。 たとえば、マネージド実装では、非ドメイン Windows 認証はサポートされていません。

## <a name="disabling-transparent-network-ip-resolution"></a>透過的なネットワーク IP の解決の無効化

[!INCLUDE [appliesto-netfx-xxxx-xxxx-md](../../includes/appliesto-netfx-xxxx-xxxx-md.md)]

透過的なネットワーク IP の解決 (TNIR) は、既存の MultiSubnetFailover 機能の改訂です。 TNIR は、ホスト名の解決された最初の IP が応答せず、ホスト名に複数の IP が関連付けられている場合に、ドライバーの接続シーケンスに影響を及ぼします。 TNIR は、MultiSubnetFailover と連動して、次の 3 つの接続シーケンスを提供します。<br />
* 0:1 つの IP が試行され、その後にすべての IP が並列で試行されます
* 1:すべての IP が並列で試行されます
* 2:すべての IP が 1 つずつ試行されます

|TransparentNetworkIPResolution|MultiSubnetFailover|動作|
|--------|--------|--------|
|True|True|1|
|正しい|誤り|0|
|False|True|1|
|False|False|2|

TransparentNetworkIPResolution は既定では有効になっています。 MultiSubnetFailover は既定では無効になっています。 TNIR を無効にするには、アプリケーションの起動時に、AppContext スイッチ **"Switch.Microsoft.Data.SqlClient.DisableTNIRByDefaultInConnectionString"** を `true` に設定します。

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.DisableTNIRByDefaultInConnectionString", true);
```

これらのプロパティの設定方法の詳細については、「[SqlConnection.ConnectionString プロパティ](/dotnet/api/microsoft.data.sqlclient.sqlconnection.connectionstring)」を参照してください。 

## <a name="enable-a-minimum-timeout-during-login"></a>ログイン中に最小タイムアウトを有効にする

[!INCLUDE [appliesto-netfx-xxxx-xxxx-md](../../includes/appliesto-netfx-xxxx-xxxx-md.md)]

ログインの試行が無制限に待機しないようにするには、アプリケーションの起動時に AppContext スイッチ **Switch.Microsoft.Data.SqlClient.UseOneSecFloorInTimeoutCalculationDuringLogin** を `true` に設定します。

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.UseOneSecFloorInTimeoutCalculationDuringLogin", false);
```

## <a name="disable-blocking-behavior-of-readasync"></a>ReadAsync のブロック動作を無効にする

[!INCLUDE [appliesto-netfx-xxxx-xxxx-md](../../includes/appliesto-netfx-xxxx-xxxx-md.md)]

既定では、ReadAsync は同期的に実行され、.NET Framework 上の呼び出し元スレッドをブロックします。 このブロック動作を無効にするには、アプリケーションの起動時に AppContext スイッチ **Switch.Microsoft.Data.SqlClient.MakeReadAsyncBlocking** を `false` に設定します。

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.MakeReadAsyncBlocking", false);
```

## <a name="see-also"></a>関連項目

[AppContext クラス](/dotnet/api/system.appcontext?view=netcore-3.1&preserve-view=true)