---
title: Microsoft Drivers for PHP のシステム要件
description: Microsoft Drivers for PHP for SQL Server では、さまざまな PHP バージョン、オペレーティング システム、SQL Server バージョンがサポートされています。
ms.custom: ''
ms.date: 03/09/2021
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b52bb4597b76ca831b94899e040a814b11b2a903
ms.sourcegitcommit: 81ee3cd57526d255de93afb84186074a3fb9885f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/10/2021
ms.locfileid: "102622668"
---
# <a name="system-requirements-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft SQL Server 用 Drivers for PHP のシステム要件

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] を使用して SQL サーバーまたは Azure SQL データベースのデータにアクセスするためにシステムにインストールする必要があるコンポーネントの一覧を示します。

Microsoft PHP Drivers for SQL Server のバージョン 4.0 以降が正式にサポートされます。 PHP ドライバーのサポートのライフサイクルと要件の詳細については、[サポート マトリックス](microsoft-php-drivers-for-sql-server-support-matrix.md)を参照してください。

## <a name="php"></a>PHP

最新の安定した PHP バイナリをダウンロードし、インストールする方法については、[PHP Web サイト](https://php.net)を参照してください。  Microsoft Drivers for PHP for SQL Server では、「[PHP バージョンのサポート](microsoft-php-drivers-for-sql-server-support-matrix.md#php-version-support)」で詳しく説明されている適切なバージョンの PHP が必要です。

-   PHP のバージョンに対応する正しいバージョンのドライバー ファイルを有効にする必要があります。 さまざまなドライバー ファイルの詳細については、「[ドライバー バージョン](#driver-versions)」を参照してください。 ドライバーをダウンロードするには、「[Download the Microsoft Drivers for PHP for SQL Server](download-drivers-php-sql-server.md)」 (Microsoft SQL Server 用 Drivers for PHP をダウンロードする) を参照してください。 PHP のドライバーを構成する方法については、「[Loading the Microsoft Drivers for PHP for SQL Server](loading-the-php-sql-driver.md)」 (Microsoft SQL Server 用 Drivers for PHP を読み込む) を参照してください。

-   Web サーバーが必要です。 Web サーバーは、PHP を実行するように構成する必要があります。 IIS での PHP アプリケーションのホスティングの詳細については、[PHP の Web サイトのチュートリアル](http://docs.php.net/manual/da/install.windows.iis7.php)を参照してください。

    [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] は IIS 10 と FastCGI でテストされています。

> [!NOTE]
> Microsoft は、IIS のサポートのみを提供しています。

## <a name="odbc-driver"></a>ODBC ドライバー

PHP が実行されるコンピューター上に、正しいバージョンの Microsoft ODBC Driver for SQL Server が必要です。 サポートされるプラットフォーム用のドライバーのサポートされるすべてのバージョンを、[こちらのページ](../odbc/download-odbc-driver-for-sql-server.md)からダウンロードできます。

64 ビット版の Windows にドライバーの Windows バージョンをダウンロードする場合は、ODBC 64 ビット インストーラーによって、32 ビットと 64 ビットの ODBC ドライバーの両方がインストールされます。 Windows の 32 ビット版を使用する場合は、ODBC x86 インストーラーを使用します。 Windows 以外のプラットフォームでは、64 ビット版のドライバーのみを使用できます。

|PHP ドライバー バージョン &#8594;<br />&#8595; ODBC ドライバーのバージョン|5.9|5.8|5.6|5.3|5.2|4.3|4.0|3.2|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|ODBC ドライバー 17 以降 |はい|Yes|Yes|Yes|はい|   |   |   |
|ODBC ドライバー 13.1|はい|Yes|Yes|Yes|Yes|Yes|はい|   |
|ODBC ドライバー 13  |   |   |   |   |   |   |はい|   |
|ODBC ドライバー 11  |   |はい|Yes|Yes|Yes|Yes|Yes|はい|

SQLSRV ドライバーを使用している場合、[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] によって使用されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Microsoft ODBC Driver for SQL Server のバージョンに関する情報が [sqlsrv_client_info](sqlsrv-client-info.md) によって返されます。 PDO_SQLSRV ドライバーを使用している場合、[PDO::getAttribute](pdo-getattribute.md) を使用して、バージョンを確認できます。

## <a name="sql-server"></a>SQL Server

サポートされている SQL Server バージョンの詳細については、[サポートされるデータベース バージョン](microsoft-php-drivers-for-sql-server-support-matrix.md#sql-server-version-certified-compatibility)に関する記事をご覧ください。

## <a name="operating-systems"></a>オペレーティング システム

サポートされるオペレーティング システムの詳細については、「[サポートされるオペレーティング システム](microsoft-php-drivers-for-sql-server-support-matrix.md#supported-operating-systems)」を参照してください。

## <a name="driver-versions"></a>ドライバー バージョン

このセクションでは、[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] の各バージョンに含まれるドライバー ファイルの一覧を示します。 各インストール パッケージには、スレッド化されたバリアントとスレッド化されていないバリアントの SQLSRV ドライバー ファイルと PDO_SQLSRV ドライバー ファイルが含まれています。 Windows では、32 ビットと 64 ビットのバリアントも使用できます。 PHP ランタイムで使用するドライバーを構成するには、「[Microsoft Drivers for PHP for SQL Server の読み込み](loading-the-php-sql-driver.md)」のインストール手順に従います。

サポートされている Linux と macOS のバージョンでは、[Linux と macOS のインストール手順](installation-tutorial-linux-mac.md)に関する記事に従って、PHP の PECL パッケージ システムを使用して適切なドライバーをインストールできます。 別の方法として、[Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) GitHub プロジェクト ページからプラットフォーム用の事前構築済みバイナリをダウンロードできます。次の表に、事前構築済みバイナリ パッケージに含まれるファイルを示します。

**Microsoft SQL Server 用 Drivers 5.9 for PHP:**

Windows では、次のドライバー ファイルが提供されています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|PHP .dll で使用|
|---------------|:---------------:|:----------------:|---------------------|
|32-bit php_sqlsrv_73_nts.dll<br />32-bit php_pdo_sqlsrv_73_nts.dll|7.3|no |32 ビット php7.dll|
|32-bit php_sqlsrv_73_ts.dll <br />32-bit php_pdo_sqlsrv_73_ts.dll |7.3|はい|32 ビット php7ts.dll|
|64-bit php_sqlsrv_73_nts.dll<br />64-bit php_pdo_sqlsrv_73_nts.dll|7.3|no |64 ビット php7.dll|
|64-bit php_sqlsrv_73_ts.dll <br />64-bit php_pdo_sqlsrv_73_ts.dll |7.3|はい|64 ビット php7ts.dll|
|32 ビット php_sqlsrv_74_nts.dll<br />32 ビット php_pdo_sqlsrv_74_nts.dll|7.4|no |32 ビット php7.dll|
|32 ビット php_sqlsrv_74_ts.dll <br />32 ビット php_pdo_sqlsrv_74_ts.dll |7.4|はい|32 ビット php7ts.dll|
|64 ビット php_sqlsrv_74_nts.dll<br />64 ビット php_pdo_sqlsrv_74_nts.dll|7.4|no |64 ビット php7.dll|
|64 ビット php_sqlsrv_74_ts.dll <br />64 ビット php_pdo_sqlsrv_74_ts.dll |7.4|はい|64 ビット php7ts.dll|
|32 ビット php_sqlsrv_80_nts.dll<br />32 ビット php_pdo_sqlsrv_80_nts.dll|8.0|no |32 ビット php8.dll|
|32 ビット php_sqlsrv_80_ts.dll <br />32 ビット php_pdo_sqlsrv_80_ts.dll |8.0|yes|32 ビット php8ts.dll|
|64 ビット php_sqlsrv_80_nts.dll<br />64 ビット php_pdo_sqlsrv_80_nts.dll|8.0|no |64 ビット php8.dll|
|64 ビット php_sqlsrv_80_ts.dll <br />64 ビット php_pdo_sqlsrv_80_ts.dll |8.0|yes|64 ビット php8ts.dll|

Linux では、次のドライバー ファイルが提供されています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_73_nts.so<br />php_pdo_sqlsrv_73_nts.so|7.3|no |
|php_sqlsrv_73_ts.so <br />php_pdo_sqlsrv_73_ts.so |7.3|はい|
|php_sqlsrv_74_nts.so<br />php_pdo_sqlsrv_74_nts.so|7.4|no |
|php_sqlsrv_74_ts.so <br />php_pdo_sqlsrv_74_ts.so |7.4|はい|
|php_sqlsrv_80_nts.so<br />php_pdo_sqlsrv_80_nts.so|8.0|no |
|php_sqlsrv_80_ts.so <br />php_pdo_sqlsrv_80_ts.so |8.0|yes|

**Microsoft Drivers 5.8 for PHP for SQL Server:**

Windows では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|PHP .dll で使用|
|---------------|:---------------:|:----------------:|---------------------|
|32-bit php_sqlsrv_72_nts.dll<br />32-bit php_pdo_sqlsrv_72_nts.dll|7.2|no |32 ビット php7.dll|
|32-bit php_sqlsrv_72_ts.dll <br />32-bit php_pdo_sqlsrv_72_ts.dll |7.2|はい|32 ビット php7ts.dll|
|64-bit php_sqlsrv_72_nts.dll<br />64-bit php_pdo_sqlsrv_72_nts.dll|7.2|no |64 ビット php7.dll|
|64-bit php_sqlsrv_72_ts.dll <br />64-bit php_pdo_sqlsrv_72_ts.dll |7.2|はい|64 ビット php7ts.dll|
|32-bit php_sqlsrv_73_nts.dll<br />32-bit php_pdo_sqlsrv_73_nts.dll|7.3|no |32 ビット php7.dll|
|32-bit php_sqlsrv_73_ts.dll <br />32-bit php_pdo_sqlsrv_73_ts.dll |7.3|はい|32 ビット php7ts.dll|
|64-bit php_sqlsrv_73_nts.dll<br />64-bit php_pdo_sqlsrv_73_nts.dll|7.3|no |64 ビット php7.dll|
|64-bit php_sqlsrv_73_ts.dll <br />64-bit php_pdo_sqlsrv_73_ts.dll |7.3|はい|64 ビット php7ts.dll|
|32 ビット php_sqlsrv_74_nts.dll<br />32 ビット php_pdo_sqlsrv_74_nts.dll|7.4|no |32 ビット php7.dll|
|32 ビット php_sqlsrv_74_ts.dll <br />32 ビット php_pdo_sqlsrv_74_ts.dll |7.4|はい|32 ビット php7ts.dll|
|64 ビット php_sqlsrv_74_nts.dll<br />64 ビット php_pdo_sqlsrv_74_nts.dll|7.4|no |64 ビット php7.dll|
|64 ビット php_sqlsrv_74_ts.dll <br />64 ビット php_pdo_sqlsrv_74_ts.dll |7.4|はい|64 ビット php7ts.dll|

Linux では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|no |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|はい|
|php_sqlsrv_73_nts.so<br />php_pdo_sqlsrv_73_nts.so|7.3|no |
|php_sqlsrv_73_ts.so <br />php_pdo_sqlsrv_73_ts.so |7.3|はい|
|php_sqlsrv_74_nts.so<br />php_pdo_sqlsrv_74_nts.so|7.4|no |
|php_sqlsrv_74_ts.so <br />php_pdo_sqlsrv_74_ts.so |7.4|はい|

**Microsoft SQL Server 用 Drivers 5.6 for PHP:**

Windows では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|PHP .dll で使用|
|---------------|:---------------:|:----------------:|---------------------|
|32-bit php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|no |32 ビット php7.dll|
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|はい|32 ビット php7ts.dll|
|64-bit php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|no |64 ビット php7.dll|
|64-bit php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|はい|64 ビット php7ts.dll|
|32-bit php_sqlsrv_72_nts.dll<br />32-bit php_pdo_sqlsrv_72_nts.dll|7.2|no |32 ビット php7.dll|
|32-bit php_sqlsrv_72_ts.dll <br />32-bit php_pdo_sqlsrv_72_ts.dll |7.2|はい|32 ビット php7ts.dll|
|64-bit php_sqlsrv_72_nts.dll<br />64-bit php_pdo_sqlsrv_72_nts.dll|7.2|no |64 ビット php7.dll|
|64-bit php_sqlsrv_72_ts.dll <br />64-bit php_pdo_sqlsrv_72_ts.dll |7.2|はい|64 ビット php7ts.dll|
|32-bit php_sqlsrv_73_nts.dll<br />32-bit php_pdo_sqlsrv_73_nts.dll|7.3|no |32 ビット php7.dll|
|32-bit php_sqlsrv_73_ts.dll <br />32-bit php_pdo_sqlsrv_73_ts.dll |7.3|はい|32 ビット php7ts.dll|
|64-bit php_sqlsrv_73_nts.dll<br />64-bit php_pdo_sqlsrv_73_nts.dll|7.3|no |64 ビット php7.dll|
|64-bit php_sqlsrv_73_ts.dll <br />64-bit php_pdo_sqlsrv_73_ts.dll |7.3|はい|64 ビット php7ts.dll|

Linux では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|no |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|はい|
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|no |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|はい|
|php_sqlsrv_73_nts.so<br />php_pdo_sqlsrv_73_nts.so|7.3|no |
|php_sqlsrv_73_ts.so <br />php_pdo_sqlsrv_73_ts.so |7.3|はい|

**Microsoft SQL Server 用 Drivers 5.3 for PHP:**

Windows では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|PHP .dll で使用|
|---------------|:---------------:|:----------------:|---------------------|
|32-bit php_sqlsrv_7_nts.dll <br />32-bit php_pdo_sqlsrv_7_nts.dll |7.0|no |32 ビット php7.dll|
|32-bit php_sqlsrv_7_ts.dll  <br />32-bit php_pdo_sqlsrv_7_ts.dll  |7.0|はい|32 ビット php7ts.dll|
|64-bit php_sqlsrv_7_nts.dll <br />64-bit php_pdo_sqlsrv_7_nts.dll |7.0|no |64 ビット php7.dll|
|64-bit php_sqlsrv_7_ts.dll  <br />64-bit php_pdo_sqlsrv_7_ts.dll  |7.0|はい|64 ビット php7ts.dll|
|32-bit php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|no |32 ビット php7.dll|
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|はい|32 ビット php7ts.dll|
|64-bit php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|no |64 ビット php7.dll|
|64-bit php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|はい|64 ビット php7ts.dll|
|32-bit php_sqlsrv_72_nts.dll<br />32-bit php_pdo_sqlsrv_72_nts.dll|7.2|no |32 ビット php7.dll|
|32-bit php_sqlsrv_72_ts.dll <br />32-bit php_pdo_sqlsrv_72_ts.dll |7.2|はい|32 ビット php7ts.dll|
|64-bit php_sqlsrv_72_nts.dll<br />64-bit php_pdo_sqlsrv_72_nts.dll|7.2|no |64 ビット php7.dll|
|64-bit php_sqlsrv_72_ts.dll <br />64-bit php_pdo_sqlsrv_72_ts.dll |7.2|はい|64 ビット php7ts.dll|

Linux では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|no |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|はい|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|no |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|はい|
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|no |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|はい|

**Microsoft SQL Server 用 Drivers 5.2 for PHP:**

Windows では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|PHP .dll で使用|
|---------------|:---------------:|:----------------:|---------------------|
|32-bit php_sqlsrv_7_nts.dll <br />32-bit php_pdo_sqlsrv_7_nts.dll |7.0|no |32 ビット php7.dll|
|32-bit php_sqlsrv_7_ts.dll  <br />32-bit php_pdo_sqlsrv_7_ts.dll  |7.0|はい|32 ビット php7ts.dll|
|64-bit php_sqlsrv_7_nts.dll <br />64-bit php_pdo_sqlsrv_7_nts.dll |7.0|no |64 ビット php7.dll|
|64-bit php_sqlsrv_7_ts.dll  <br />64-bit php_pdo_sqlsrv_7_ts.dll  |7.0|はい|64 ビット php7ts.dll|
|32-bit php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|no |32 ビット php7.dll|
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|はい|32 ビット php7ts.dll|
|64-bit php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|no |64 ビット php7.dll|
|64-bit php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|はい|64 ビット php7ts.dll|
|32-bit php_sqlsrv_72_nts.dll<br />32-bit php_pdo_sqlsrv_72_nts.dll|7.2|no |32 ビット php7.dll|
|32-bit php_sqlsrv_72_ts.dll <br />32-bit php_pdo_sqlsrv_72_ts.dll |7.2|はい|32 ビット php7ts.dll|
|64-bit php_sqlsrv_72_nts.dll<br />64-bit php_pdo_sqlsrv_72_nts.dll|7.2|no |64 ビット php7.dll|
|64-bit php_sqlsrv_72_ts.dll <br />64-bit php_pdo_sqlsrv_72_ts.dll |7.2|はい|64 ビット php7ts.dll|

Linux では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|no |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|はい|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|no |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|はい|
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|no |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|はい|

**Microsoft SQL Server 用 Drivers 4.3 for PHP:**

Windows では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|PHP .dll で使用|
|---------------|:---------------:|:----------------:|---------------------|
|32-bit php_sqlsrv_7_nts.dll <br />32-bit php_pdo_sqlsrv_7_nts.dll |7.0|no |32 ビット php7.dll|
|32-bit php_sqlsrv_7_ts.dll  <br />32-bit php_pdo_sqlsrv_7_ts.dll  |7.0|はい|32 ビット php7ts.dll|
|64-bit php_sqlsrv_7_nts.dll <br />64-bit php_pdo_sqlsrv_7_nts.dll |7.0|no |64 ビット php7.dll|
|64-bit php_sqlsrv_7_ts.dll  <br />64-bit php_pdo_sqlsrv_7_ts.dll  |7.0|はい|64 ビット php7ts.dll|
|32-bit php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|no |32 ビット php7.dll|
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|はい|32 ビット php7ts.dll|
|64-bit php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|no |64 ビット php7.dll|
|64-bit php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|はい|64 ビット php7ts.dll|

Linux では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|no |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|はい|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|no |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|はい|

**Microsoft SQL Server 用 Drivers 4.0 for PHP**

Windows では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|PHP .dll で使用|
|---------------|:---------------:|:----------------:|---------------------|
|php_sqlsrv_7_nts_x86.dll<br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|no|32 ビット php7.dll|
|php_sqlsrv_7_ts_x86.dll<br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|はい|32 ビット php7ts.dll|
|php_sqlsrv_7_nts_x64.dll<br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|no|64 ビット php7.dll|
|php_sqlsrv_7_ts_x64.dll<br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|はい|64 ビット php7ts.dll|

Linux では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|no |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|はい|

**Microsoft SQL Server 用 Drivers 3.2 for PHP**

Windows では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|PHP .dll で使用|
|---------------|:---------------:|:----------------:|---------------------|
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|no|php5.dll|
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|はい|php5ts.dll|
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|no|php5.dll|
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|はい|php5ts.dll|
|php_sqlsrv_56_nts.dll<br />php_pdo_sqlsrv_56_nts.dll|5.6|no|php5.dll|
|php_sqlsrv_56_ts.dll<br />php_pdo_sqlsrv_56_ts.dll|5.6|はい|php5ts.dll|

## <a name="see-also"></a>参照

- [Microsoft Drivers for PHP for SQL Server の概要](getting-started-with-the-php-sql-driver.md)
- [SQL Server 用 Microsoft Drivers for PHP のためのプログラミング ガイド](programming-guide-for-php-sql-driver.md)
- [SQLSRV ドライバー API リファレンス](sqlsrv-driver-api-reference.md)
- [PDO_SQLSRV ドライバー API リファレンス](pdo-sqlsrv-driver-reference.md)
