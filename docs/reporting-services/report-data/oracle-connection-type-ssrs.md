---
title: Oracle の接続の種類 (SSRS および Power BI Report Server)
description: データ ソースを構築する方法については、この記事の Oracle の接続の種類に関する情報を参照してください。
ms.date: 11/03/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 9db86dd2-beda-42d8-8af7-2629d58a8e3d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f92b7e0a414cbe6b9cbdb9dcc04cc8779ff4cff6
ms.sourcegitcommit: 985e2e8e494badeac6d6b652cd35765fd9c12d80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2020
ms.locfileid: "93328474"
---
# <a name="oracle-connection-type-ssrs--power-bi-report-server"></a>Oracle の接続の種類 (SSRS および Power BI Report Server)

Oracle データベースのデータをレポート内で使用するには、種類が Oracle のレポート データ ソースに基づいたデータセットが必要です。 このビルトイン データ ソースの種類は、Oracle Data Provider を直接使用し、Oracle クライアント ソフトウェア コンポーネントが必要です。 この記事では、Reporting Services、Power BI Report Server、レポート ビルダー、Power BI Desktop のドライバーをダウンロードしてインストールする方法について説明します。


この記事の情報を使用して、データ ソースを構築してください。 手順については、「 [データ接続を追加および確認する (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)」を参照してください。 

> [!IMPORTANT]
> Oracle の Managed および Unmanaged ODP.NET ドライバーの登録に Oracle の OraProvCfg.exe ツールを使用する次のコマンドは、上記の Microsoft 製品で使用する例として提供しています。 お使いの環境に固有の ODP.NET ドライバーの構成については、Oracle のサポートに問い合わせるか、[.NET 用の Oracle Data Provider の構成](https://docs.oracle.com/en/database/oracle/oracle-database/19/odpnt/InstallConfig.html#GUID-1F689B90-2CC4-4907-B8FE-A5F4EE36F673)に関する Oracle のドキュメントを参照する必要があります。

## <a name="64-bit-drivers-for-the-report-servers"></a>レポート サーバー用の 64 ビット ドライバー

Oracle ダウンロード サイトで、[Oracle 64-bit ODAC Oracle Universal Installer (OUI)](https://www.oracle.com/technetwork/topics/dotnet/downloads/odacdeploy-4242173.html) をインストールします。 Oracle ODAC ドライバー 12.2 以降を使用している場合は、次の手順のみが必要です。 それ以外の場合、新しい Oracle ホームのコンピューター全体ではない構成に既定でインストールされます。 これらの手順では、c:\oracle64 フォルダーに ODAC 18.x ファイルがインストールされていることを前提としています。


### <a name="paginated-rdl-reports-use-managed-odpnet"></a>Managed ODP.NET を使用するページ分割された (RDL) レポート

Power BI Report Server と SQL Server Reporting Services 2016 以降では、ページ分割された (RDL) レポートに対していずれも **Managed ODP.NET** を使用します。 次の手順に従って、Managed ODP.NET を登録します。

1. ODP.NET Managed Client を GAC に登録します。

   ```
   C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:gac /providerpath:C:\oracle64\product\18.0.0\client_1\odp.net\managed\common\Oracle.ManagedDataAccess.dll
   ```

2. ODP.NET Managed Client エントリを machine.config に追加します。

   ```
   C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:config /force /product:odpm /frameworkversion:v4.0.30319 /providerpath:C:\oracle64\product\18.0.0\client_1\odp.net\managed\common\Oracle.ManagedDataAccess.dll
   ```

### <a name="power-bi-reports-use-unmanaged-odpnet"></a>Power BI レポートに Unmanaged ODP.NET を使用する

Power BI Report Server は、Power BI のレポートに **Unmanaged ODP.NET** を使用します。 次の手順に従って、Unmanaged ODP.NET を登録します。

1. ODP.NET Unmanaged Client を GAC に登録します。

   ```
   C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:gac /providerpath:C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll
   ```
2. ODP.NET Unmanaged Client エントリを machine.config に追加します。

   ```
   C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:config /force /product:odp /frameworkversion:v4.0.30319 /providerpath:C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll
   ```

## <a name="32-bit-drivers-for-report-builder"></a>レポート ビルダー用の 32 ビット ドライバー

レポート ビルダーは、ページ分割された (RDL) レポートの作成に、 **Managed ODP.NET** を使用します。 Oracle ODAC ドライバー 12.2 以降を使用している場合は、次の手順のみが必要です。 それ以外の場合、新しい Oracle ホームのコンピューター全体ではない構成に既定でインストールされます。 これらの手順では、レポート ビルダーがインストールされている c:\oracle32 フォルダーに ODAC 18.x ファイルがインストールされていることを前提としています。 次の手順に従って、Managed ODP.NET を登録します。

1. Oracle ダウンロード サイトで、[Oracle 32-bit ODAC Oracle Universal Installer (OUI)](https://www.oracle.com/technetwork/topics/dotnet/downloads/odacdev-4242174.html) をインストールします。

2. ODP.NET Managed Client を GAC に登録します。

   ```
   C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:gac /providerpath:C:\oracle32\product\18.0.0\client_1\odp.net\managed\common\Oracle.ManagedDataAccess.dll
   ```

3. ODP.NET Managed Client エントリを machine.config に追加します。

   ```
   C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:config /force /product:odpm /frameworkversion:v4.0.30319 /providerpath:C:\oracle32\product\18.0.0\client_1\odp.net\managed\common\Oracle.ManagedDataAccess.dll
   ```

## <a name="64-bit-and-32-bit-drivers-for-power-bi-desktop"></a>Power BI Desktop 用の 64 ビットと 32 ビットのドライバー

Power BI Desktop は、Power BI のレポートの作成に **Unmanaged ODP.NET** を使用します。 Oracle ODAC ドライバー 12.2 以降を使用している場合は、次の手順のみが必要です。 それ以外の場合、新しい Oracle ホームのコンピューター全体ではない構成に既定でインストールされます。 これらの手順では、64 ビットの Power BI Desktop には c:\oracle64 フォルダーに、32 ビットの Power BI Desktop には c:\oracle32 フォルダーに、ODAC 18.x ファイルがインストールされていることを前提としています。 次の手順に従って、Unmanaged ODP.NET を登録します。

### <a name="64-bit-power-bi-desktop"></a>64 ビット Power BI Desktop

1. Oracle ダウンロード サイトで、[Oracle 64-bit ODAC Oracle Universal Installer (OUI)](https://www.oracle.com/technetwork/topics/dotnet/downloads/odacdeploy-4242173.html) をインストールします。
2. ODP.NET Unmanaged Client を GAC に登録します。

   ```
   C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:gac /providerpath:C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll
   ```

3. ODP.NET Unmanaged Client エントリを machine.config に追加します。

   ```
   C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:config /force /product:odp /frameworkversion:v4.0.30319 /providerpath:C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll
   ```

### <a name="32-bit-power-bi-desktop"></a>32 ビット Power BI Desktop

1. Oracle ダウンロード サイトで、[Oracle 32-bit ODAC Oracle Universal Installer (OUI)](https://www.oracle.com/technetwork/topics/dotnet/downloads/odacdev-4242174.html) をインストールします。

2. ODP.NET Unmanaged Client を GAC に登録します。

   ```
   C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:gac /providerpath:C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll
   ```

3. ODP.NET Unmanaged Client エントリを machine.config に追加します。

   ```
   C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:config /force /product:odp /frameworkversion:v4.0.30319 /providerpath:C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll
   ```

##  <a name="connection-string"></a><a name="Connection"></a> 接続文字列  

データ ソースへの接続に使用する接続情報および資格情報については、データベース管理者に問い合わせてください。 次に示す接続文字列の例では、Unicode を使用して "Oracle18" というサーバー上の Oracle データベースを指定しています。 サーバー名は、Tnsnames.ora 構成ファイルで Oracle サーバー インスタンス名として定義されたものと一致する必要があります。  
  
```  
Data Source="Oracle"; Unicode="True"  
```  
  
接続文字列の例の詳細については、「[データ接続文字列を作成する - レポート ビルダーおよび SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)」を参照してください。  
  
##  <a name="credentials"></a><a name="Credentials"></a> [資格情報]  
クエリの実行、ローカルでのレポートのプレビュー、およびレポート サーバーからのレポートのプレビューには、資格情報が必要です。  
  
レポートをパブリッシュした後、レポートをレポート サーバーで実行するときに、データを取得するための権限が有効な状態になるように、データ ソースの資格情報を変更する必要が生じる場合があります。  
  
詳細については、「 [レポート データ ソースに関する資格情報と接続情報を指定する](specify-credential-and-connection-information-for-report-data-sources.md)」をご覧ください。  
  
##  <a name="queries"></a><a name="Query"></a> クエリ  
データセットを作成するには、ボックスの一覧からストアド プロシージャを選択するか、SQL クエリを作成します。 クエリを作成するには、テキストベースのクエリ デザイナーを使用する必要があります。 詳細については、「[テキストベースのクエリ デザイナーのユーザー インターフェイス &#40;レポート ビルダー&#41;](../../reporting-services/report-data/text-based-query-designer-user-interface-report-builder.md)」を参照してください。  
  
結果セットを 1 つだけ返すストアド プロシージャを指定できます。 カーソルベースのクエリの使用はサポートされていません。  
  
##  <a name="parameters"></a><a name="Parameters"></a> パラメーター  

クエリにクエリ変数が含まれている場合は、対応するレポート パラメーターが自動的に生成されます。 この拡張機能では、名前付きパラメーターがサポートされます。 Oracle Version 9 以降の場合、複数値パラメーターがサポートされます。  
  
 レポート パラメーターは、既定のプロパティ値を使用して作成されます。この既定のプロパティ値は、変更が必要になることがあります。 たとえば、各レポート パラメーターのデータ型は **Text** です。 レポート パラメーターを作成した後に、既定値の変更が必要になる場合があります。 詳細については、「 [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)にあります。  
  
##  <a name="remarks"></a><a name="Remarks"></a> 解説  

Oracle データ ソースに接続するには、システム管理者が、Oracle データベースからのデータの取得をサポートするバージョンの .NET Data Provider for Oracle をインストールしておく必要があります。 このデータ プロバイダーは、レポート ビルダーがインストールされているコンピューターとレポート サーバーにインストールされている必要があります。  
  
詳細については、次の記事を参照してください。  
  
- [Reporting Services を使用して Oracle データ ソースの構成およびアクセスを行う方法](/archive/blogs/dataaccesstechnologies/configure-oracle-data-source-for-sql-server-reporting-services-ssdt-and-report-server)  
- [NETWORK SERVICE セキュリティ プリンシパルに権限を追加する方法](https://support.microsoft.com/kb/870668)  
  
### <a name="alternate-data-extensions"></a>代替データ拡張機能 

Oracle データベースからのデータの取得は、OLE DB のデータ ソースの種類を使用して行うこともできます。 詳細については、「[OLE DB の接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/ole-db-connection-type-ssrs.md)」を参照してください。  

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions" 

### <a name="report-models"></a>レポート モデル

 Oracle データベースに基づくモデルを作成することもできます。  
::: moniker-end

### <a name="platform-and-version-information"></a>プラットフォームおよびバージョン情報  

プラットフォームとバージョンのサポートについて詳しくは、「[Reporting Services でサポートされるデータ ソース &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)」をご覧ください。  

## <a name="see-also"></a>参照

[レポート パラメーター &#40;レポート ビルダーおよびレポート デザイナー&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   

[データのフィルター、グループ化、および並べ替え &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   

[式 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)
