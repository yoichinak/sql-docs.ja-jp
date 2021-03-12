---
title: sqlpackage をダウンロードしてインストールする
description: Windows、macOS、または Linux 用の sqlpackage をダウンロードしてインストールします
ms.custom: tools|sos
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan; sstein
ms.date: 03/10/2021
ms.openlocfilehash: 2077800356a065ae4650cf6ab97ea45c3c537b8c
ms.sourcegitcommit: 81ee3cd57526d255de93afb84186074a3fb9885f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/10/2021
ms.locfileid: "102622768"
---
# <a name="download-and-install-sqlpackage"></a>sqlpackage をダウンロードしてインストールする

sqlpackage は Windows、macOS、Linux 上で実行されます。

.NET Framework の最新リリースと、macOS および Linux のプレビューをダウンロードしてインストールします。

|プラットフォーム|ダウンロード|リリース日|Version|Build
|:---|:---|:---|:---|:---|
|[Windows](#get-sqlpackage-for-windows)|[MSI インストーラー](https://go.microsoft.com/fwlink/?linkid=2157201)|2021 年 3 月 10 日| 18.7 | 15.0.5084.2 |
|[macOS .NET Core](#get-sqlpackage-net-core-for-macos) |[zip ファイル](https://go.microsoft.com/fwlink/?linkid=2157203)|2021 年 3 月 10 日| 18.7| 15.0.5084.2 |
|[Linux .NET Core](#get-sqlpackage-net-core-for-linux) |[zip ファイル](https://go.microsoft.com/fwlink/?linkid=2157202)|2021 年 3 月 10 日| 18.7| 15.0.5084.2 |
|[Windows .NET Core](#get-sqlpackage-net-core-for-windows) |[zip ファイル](https://go.microsoft.com/fwlink/?linkid=2157302)|2021 年 3 月 10 日| 18.7| 15.0.5084.2 |

最新リリースに関する詳細については、[リリース ノート](release-notes-sqlpackage.md)をご覧ください。 追加の言語をダウンロードするには、「[使用できる言語](#available-languages)」を参照してください。


最新の sqlpackage で環境を自動化するときに利用できる、[Linux .NET Core](#get-sqlpackage-net-core-for-linux) の最新版 sqlpackage を指すエバーグリーン リンク ([https://aka.ms/sqlpackage-linux](https://aka.ms/sqlpackage-linux)) が利用できます。

## <a name="dacfx"></a>DacFx
SqlPackage は DacFx フレームワークのコマンドライン インターフェイスであり、一部のパブリック DacFx API が公開されます。 DacServices ([Microsoft.SqlServer.Dac](/dotnet/api/microsoft.sqlserver.dac.dacservices)) は、データベースの配置をアプリケーション パイプラインに統合するための関連メカニズムです。  DacServices API は、NuGet ([Microsoft.SqlServer.DACFx](https://www.NuGet.org/packages/Microsoft.SqlServer.DACFx)) を介してパッケージ内で使用できます。  現在の DacFx のバージョンは 150.4897.1 です。

.NET CLI を介して NuGet パッケージをインストールするには、次のコマンドを使用します。

```cmd
dotnet add package Microsoft.SqlServer.DACFx
```

>[!NOTE]
> 追加の NuGet パッケージは、DacFx 名 "Microsoft.SqlServer.DacFx.x64" と "Microsoft.SqlServer.DacFx.x86" で公開されていました。 両方のプラットフォームは、"Microsoft. SqlServer. DACFx" パッケージでサポートされています。 x64 または x86 のバリアントではなく、このパッケージへの参照を新規に作成する必要があります。

## <a name="get-sqlpackage-for-windows"></a>Windows 用の sqlpackage を取得する

このリリースの sqlpackage には、標準の Windows インストーラーのエクスペリエンスと、.zip が含まれています。 

1. [Windows 用の DacFramework.msi インストーラー](https://go.microsoft.com/fwlink/?linkid=2157201)をダウンロードして実行します。
2. 新しいコマンド プロンプト ウィンドウを開き、sqlpackage.exe を実行します
    - sqlpackage は ```C:\Program Files\Microsoft SQL Server\150\DAC\bin``` フォルダーにインストールされます

## <a name="get-sqlpackage-net-core-for-windows"></a>Windows 用の sqlpackage .NET Core を取得する

1. [Windows 用の sqlpackage](https://go.microsoft.com/fwlink/?linkid=2157302) をダウンロードします。
2. ファイルを抽出するには、エクスプローラーでファイルを右クリックして [すべて展開...] を選択し、ターゲット ディレクトリを選択します。
3. 新しいターミナル ウィンドウを開き、sqlpackage が抽出された場所へ cd を実行します。

   ```cmd
   > sqlpackage
   ```

## <a name="get-sqlpackage-net-core-for-macos"></a>macOS 用の sqlpackage .NET Core を取得する

1. [macOS 用の sqlpackage](https://go.microsoft.com/fwlink/?linkid=2157203) をダウンロードします。
2. ファイルを抽出して sqlpackage を起動するには、新しいターミナル ウィンドウを開いて次のコマンドを入力します。

   ```bash
   $ mkdir sqlpackage
   $ unzip ~/Downloads/sqlpackage-osx-<version string>.zip -d ~/sqlpackage 
   $ echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bash_profile
   $ source ~/.bash_profile
   $ sqlpackage
   ```

   > [!NOTE]
   > macOS で sqlpackage を実行するには、セキュリティ設定の変更が必要になる場合があります。 コマンド ラインから Gatekeeper を操作するために次のコマンドを実行してください。

   **sqlpackage の実行前:**
   ```bash
   $ sudo spctl --master-disable
   ```

   **sqlpackage の実行後:**
   ```bash
   $ sudo spctl --master-enable
   ```

## <a name="get-sqlpackage-net-core-for-linux"></a>Linux 用の sqlpackage .NET Core を取得する

1. インストーラーのいずれか、または tar.gz アーカイブを使用して [Linux 用の sqlpackage](https://go.microsoft.com/fwlink/?linkid=2157202) をダウンロードします。
2. ファイルを抽出して sqlpackage を起動するには、新しいターミナル ウィンドウを開いて次のコマンドを入力します。

   ```bash
   $ cd ~
   $ mkdir sqlpackage
   $ unzip ~/Downloads/sqlpackage-linux-<version string>.zip -d ~/sqlpackage 
   $ echo "export PATH=\"\$PATH:$HOME/sqlpackage\"" >> ~/.bashrc
   $ chmod a+x ~/sqlpackage/sqlpackage
   $ source ~/.bashrc
   $ sqlpackage
   ```

   > [!NOTE]
   > Debian、Redhat、および Ubuntu では、依存関係が不足する場合があります。 ご自身の Linux のバージョンに応じて、次のコマンドを使ってこれらの依存関係をインストールします。

   **Debian:**

   ```bash
   $ sudo apt-get install libunwind8
   ```

   **Redhat:**

   ```bash
   $ yum install libunwind
   $ yum install libicu
   ```

   **Ubuntu:**

   ```bash
   $ sudo apt-get install libunwind8

   # install the libicu library based on the Ubuntu version
   $ sudo apt-get install libicu52      # for 14.x
   $ sudo apt-get install libicu55      # for 16.x
   $ sudo apt-get install libicu57      # for 17.x
   $ sudo apt-get install libicu60      # for 18.x
   $ sudo apt-get install libicu60      # for 20.x
   ```

## <a name="uninstall-sqlpackage"></a>sqlpackage をアンインストールする

Windows インストーラーを使って sqlpackage をインストールした場合は、Windows アプリケーションを削除するのと同じ方法でアンインストールします。

.zip やその他のアーカイブを使って sqlpackage をインストールした場合は、そのファイルを削除します。

## <a name="supported-operating-systems"></a>サポートされるオペレーティング システム

sqlpackage は Windows、macOS、Linux 上で実行され、.NET Core 3.1 を利用して構築されます。  [.NET Core 3.1 OS 要件](https://github.com/dotnet/core/blob/master/release-notes/3.1/3.1-supported-os.md)は sqlpackage に適用されます。

### <a name="windows-x64"></a>Windows (x64)

- Windows 10 (1607+)
- Windows 8.1
- Windows 7 SP1
- Windows サーバー コア
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2019

### <a name="macos"></a>macOS

- macOS 10.15 "Catalina"
- macOS 10.14 "Mojave"
- macOS 10.13 "High Sierra"

### <a name="linux-x64"></a>Linux (x64)

- Red Hat Enterprise Linux 7+
- SUSE Linux Enterprise Server v12 SP2+
- Ubuntu 16.04、18.04、20.04

## <a name="available-languages"></a>使用できる言語

sqlpackage の今回のリリースは、次の言語でインストールできます。

sqlpackage Windows:  
[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2157201&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2157201&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2157201&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2157201&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2157201&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2157201&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2157201&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2157201&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2157201&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2157201&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2157201&clcid=0x40a)

sqlpackage .NET Core Windows:  
[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2157302&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2157302&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2157302&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2157302&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2157302&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2157302&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2157302&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2157302&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2157302&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2157302&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2157302&clcid=0x40a)

sqlpackage .NET Core macOS:  
[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2157203&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2157203&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2157203&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2157203&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2157203&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2157203&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2157203&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2157203&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2157203&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2157203&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2157203&clcid=0x40a)

sqlpackage .NET Core Linux:  
[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2157202&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2157202&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2157202&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2157202&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2157202&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2157202&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2157202&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2157202&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2157202&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2157202&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2157202&clcid=0x40a)


## <a name="next-steps"></a>次の手順

- [sqlpackage](sqlpackage.md) について詳しく学習する

[Microsoft プライバシーに関する声明](https://go.microsoft.com/fwlink/?LinkId=521839)