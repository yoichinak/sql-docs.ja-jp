---
title: システム要件、インストール、およびドライバー ファイル | Microsoft Docs
description: この記事では、Microsoft ODBC Driver for SQL Server のシステム要件について説明します。
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d90fa182-1dab-4d6f-bd85-a04dd1479986
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2f0ce55639f5d6835c50744114a48d510d41c887
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87930393"
---
# <a name="system-requirements-installation-and-driver-files"></a>システム必要条件、インストール、およびドライバー ファイル

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

この記事では、SQL Server に接続する ODBC ドライバーについて説明します。

## <a name="sql-version-compatibility"></a>SQL バージョンの互換性

互換性とは、ドライバーが、リリースの時点で SQL の既存のリリースに対して互換性のテストが行われていることを示します。 SQL Server のリリースでは、ほとんどの場合、既存のクライアント ドライバーとの下位互換性を維持するようにしています。 ただし、SQL Server リリースの新機能は、古いクライアント ドライバーでは使用できない場合があります。

|データベースのバージョン&nbsp;&#8594;<br />&#8595; ドライバーのバージョン|Azure SQL データベース|Azure Synapse Analytics|Azure SQL Managed Instance|SQL Server 2019|SQL Server 2017|SQL Server 2016|SQL Server 2014|SQL Server 2012|SQL Server 2008 R2|SQL Server 2008|SQL Server 2005|
|----|---|---|---|---|---|---|---|---|---|---|---|
|17.6|はい|はい|はい|はい|はい|はい|はい|はい|   |   |   |
|17.5|はい|はい|はい|はい|はい|はい|はい|はい|   |   |   |
|17.4|はい|はい|はい|はい|はい|はい|はい|はい|   |   |   |
|17.3|はい|はい|はい|はい|はい|はい|はい|はい|はい|はい|   |
|17.2|はい|はい|はい|   |はい|はい|はい|はい|はい|はい|   |
|17.1|はい|はい|はい|   |はい|はい|はい|はい|はい|はい|   |
|17.0|はい|はい|はい|   |はい|はい|はい|はい|はい|はい|   |
|13.1|   |   |   |   |はい|はい|はい|はい|はい|はい|   |
|13  |   |   |   |   |   |はい|はい|はい|はい|はい|   |
|11  |   |   |   |   |   |   |はい|はい|はい|はい|はい|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

### <a name="connection-string-details"></a>接続文字列の詳細

接続文字列で指定するドライバー名は `ODBC Driver 11 for SQL Server` または `ODBC Driver 13 for SQL Server` (13 と 13.1 の両方) または `ODBC Driver 17 for SQL Server` です。

## <a name="supported-operating-systems"></a>サポートされるオペレーティング システム

次のマトリックスは、Windows オペレーティング システムのバージョンでサポートされているドライバーのバージョンを示しています。

|オペレーティング システム&nbsp;&#8594;<br />&#8595; ドライバーのバージョン|Windows Server 2019|Windows Server 2016|Windows Server 2012 R2|Windows Server 2012|Windows Server 2008 R2|Windows 10|Windows 8.1|Windows 7|Windows Vista SP2|
|----|---|---|---|---|---|---|---|---|---|
|17.6|はい|はい|はい|はい|   |はい|はい|   |   |
|17.5|はい|はい|はい|はい|   |はい|はい|   |   |
|17.4|はい|はい|はい|はい|はい|はい|はい|はい|   |
|17.3|はい|はい|はい|はい|はい|はい|はい|はい|   |
|17.2|   |はい|はい|はい|はい|はい|はい|はい|   |
|17.1|   |はい|はい|はい|はい|はい|はい|はい|   |
|17.0|   |はい|はい|はい|はい|はい|はい|はい|   |
|13.1|   |はい|はい|はい|はい|はい|はい|はい|   |
|13  |   |   |   |はい|はい|   |はい|はい|   |
|11  |   |   |   |はい|はい|   |   |はい|はい|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

## <a name="installing-microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server のインストール

[Windows 向けのダウンロード](../download-odbc-driver-for-sql-server.md#download-for-windows)のいずれかから `msodbcsql.msi` を実行すると、ドライバーがインストールされます。

> [!NOTE]
> Driver 17.1.0.1 以下をインストールしているお客様は、新しいバージョンの Driver をインストールする前にこれを手動でアンインストールすることをお勧めします。

### <a name="side-by-side-with-native-client"></a>Native Client とサイド バイ サイド

ドライバーは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client とサイド バイ サイドでインストールできます。 ドライバーのメジャー バージョン (11、13、17) はすべて、相互にサイド バイ サイドでインストールすることもできます。

`msodbcsql.msi` を呼び出すと、既定ではクライアント コンポーネントのみがインストールされます。 クライアント コンポーネントは、ドライバーを使用して開発されたアプリケーションの実行をサポートするファイルです。 SDK コンポーネントをインストールするには、コマンド ラインで `ADDLOCAL=ALL` を指定します。 次に例を示します。
  
```console
msiexec /i msodbcsql.msi ADDLOCAL=ALL  
```  

### <a name="end-user-license"></a>エンドユーザー ライセンス

`/passive`、`/qn`、`/qb`、または `/qr` オプションを使用してインストールする場合は、`IACCEPTMSODBCSQLLICENSETERMS=YES` を指定してエンド ユーザー ライセンスの条項に同意します。 このオプションは、すべて大文字で指定する必要があります。 次に例を示します。
  
```console
msiexec /quiet /passive /qn /i msodbcsql.msi IACCEPTMSODBCSQLLICENSETERMS=YES ADDLOCAL=ALL  
```  

### <a name="silent-uninstall"></a>サイレント アンインストール

サイレント アンインストールを行う方法を次の例に示します。
  
```console
msiexec /quiet /passive /qn /uninstall msodbcsql.msi  
```  

### <a name="indicate-dependency"></a>依存関係を示す

アプリケーションでは、ドライバーを使用する場合、`APPGUID` インストール オプションを使ってドライバーに依存していることを示す必要があります。 これを示すことにより、ドライバーのインストーラーは、アンインストール前に依存するアプリケーションを報告できます。 ドライバーの依存関係を指定するには、ドライバーのサイレント インストールを行うときに `APPGUID` コマンド ライン パラメーターをご利用の製品コードに設定します Microsoft インストーラーを使用してアプリケーションのセットアップ プログラムをバンドルするときは、製品コードを作成する必要があります。 次に例を示します。
  
```console
msiexec /i msodbcsql.msi APPGUID={ <Your dependent application's APPGUID> }  
```  

## <a name="command-line-tools-sqlcmdexe-and-bcpexe"></a>コマンドライン ツール: sqlcmd.exe および bcp.exe

ドライバーで使用するための `bcp.exe` および `sqlcmd.exe` のツールは、[Microsoft Command Line Utilities 11 for SQL Server](https://www.microsoft.com/download/details.aspx?id=36433)、[Microsoft Command Line Utilities 13 for SQL Server](https://www.microsoft.com/download/details.aspx?id=52680)、または [Microsoft Command Line Utilities 13.1 for SQL Server](https://www.microsoft.com/download/details.aspx?id=53591) でダウンロードできます。 `sqlcmd.exe` および `bcp.exe` をインストールするにはドライバーが必要です。
  
`bcp.exe` および `sqlcmd.exe` はバージョン 11 の場合は `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC` の `110\Tools` サブフォルダーに、13 と 13.1 の場合は `130\Tools` にインストールされます。

BCP 関数を使用するアプリケーションでは、アプリケーションのコンパイルに使用したヘッダー ファイルおよびライブラリに付属するものと同じバージョンのドライバーを指定する必要があります。  

たとえば、`msodbcsql11.lib` と `msodbcsql.h` で ODBC アプリケーションをコンパイルするときは、接続文字列で "DRIVER={ODBC Driver 11 for SQL Server}" を使用します。

## <a name="components-of-the-microsoft-odbc-driver-for-ssnoversion-on-windows"></a>Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] on Windows のコンポーネント

Windows 上の ODBC ドライバーには、次のコンポーネントが含まれています。

| コンポーネント | 説明 |
| :-------- | :---------- |
|msodbcsql17.dll または <br/> msodbcsql13.dll または <br/> msodbcsql11.dll|ドライバーのすべての機能を含む DLL (ダイナミック リンク ライブラリ) ファイル。 このファイルは %SYSTEMROOT%\System32 にインストールされます。|  
|msodbcdiag17.dll または <br/> msodbcdiag13.dll または <br/> msodbcdiag11.dll|ドライバーの診断 (トレース) インターフェイスを含むダイナミック リンク ライブラリ (DLL) ファイル。 このファイルは %SYSTEMROOT%\System32 にインストールされます。|
|msodbcsqlr17.rll または <br/> msodbcsqlr13.rll または <br/> msodbcsqlr11.rll|ドライバー ライブラリに付随するリソース ファイル。 このファイルは %SYSTEMROOT%\System32\1033 にインストールされます。| 
|s13ch_msodbcsql.chm または <br/> s11ch_msodbcsql.chm |ドライバーのデータ ソースを作成する方法が説明されているデータ ソース ウィザードのヘルプ ファイル。 このファイルは %SYSTEMROOT%\System32\1033 にインストールされます <br /> <br /> **注:** ODBC Driver 17 の chm ファイルはありません。 |  
|msodbcsql.h|ドライバーを使用するために必要な新しい定義がすべて含まれているヘッダー ファイル。<br /><br /> **注:** msodbcsql.h と odbcss.h を同じプログラムで参照することはできません。<br /><br /> ODBC Driver 17 または 13 用の msodbcsql.h は、%PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK にインストールされます。 <br /> ODBC Driver 11 用の msodbcsql.h は、%PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK にインストールされます。| 
|msodbcsql17.lib または <br/> msodbcsql13.lib または <br/> msodbcsql11.lib|ドライバーの一部である **bcp** ユーティリティ関数を呼び出すために必要なライブラリ ファイル。<br /><br /> **注:** ご利用のプログラムでこのライブラリ ファイルを参照する場合は、ライブラリ ファイルがシステム パス、およびアプリケーションを使用するプログラムのシステム パスに含まれることを確認してください。<br /><br /> msodbcsql17.lib や msodbcsql13.lib は、%PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK にインストールされます。<br /> msodbcsql11.lib は %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK にインストールされます。|
| &nbsp; | &nbsp; |

## <a name="see-also"></a>関連項目

[Microsoft ODBC Driver for SQL Server on Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
