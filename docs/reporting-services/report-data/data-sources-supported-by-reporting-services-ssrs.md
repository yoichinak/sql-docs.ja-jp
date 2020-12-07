---
title: Reporting Services でサポートされるデータ ソース | Microsoft Docs
description: Microsoft SQL Server、Oracle、ODBC など、Reporting Services でサポートされているさまざまなデータ ソースについて説明します。
ms.date: 05/21/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- SQL Server data processing extension [Reporting Services]
- XML data processing extension [Reporting Services]
- reports [Reporting Services], data
- data processing extensions [Reporting Services], data sources
- Oracle [Reporting Services]
- OLE DB data processing extension
- data sources [Reporting Services], about data sources
- ODBC data processing extension
- Reporting Services, data sources
ms.assetid: 9d11d055-a3be-45aa-99a7-46447a94ed42
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5b8fb15c2fb479471000fc9979c691761e4d81cd
ms.sourcegitcommit: 985e2e8e494badeac6d6b652cd35765fd9c12d80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2020
ms.locfileid: "93328564"
---
# <a name="data-sources-supported-by-reporting-services-ssrs"></a>Reporting Services でサポートされるデータ ソース (SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] でレポート データをデータ ソースから取得する処理は、データ処理拡張機能を使用するモジュール式の拡張可能なデータ レイヤーを通して行われます。 レポート データをデータ ソースから取得するには、対象となるデータ ソースの種類 (データ ソースで動作しているバージョンのソフトウェア) およびデータ ソース プラットフォーム (32 ビットまたは 64 ビット [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]) がサポートされているデータ処理拡張機能を選択する必要があります。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]を配置すると、レポート作成クライアントとレポート サーバーの両方にデータ処理拡張機能セットが自動的にインストールおよび登録され、さまざまな種類のデータ ソースにアクセスできるようになります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、次のデータ ソースの種類がインストールされます。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (MDX、DMX、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]、およびテーブル モデル用)  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]  
  
-   Oracle  
  
-   SAP BW 
  
-   [!INCLUDE[extEssbase](../../includes/extessbase-md.md)]  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint リスト  
  
-   Teradata  
  
-   OLE DB (OLE DB)  
  
-   ODBC  
  
-   XML  
  
 また、システム管理者は、カスタム データ処理拡張機能や標準の [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダーをインストールして登録できます。 レポートの処理や表示を行うには、データ処理拡張機能およびデータ プロバイダーをレポート サーバーにインストールし登録する必要があります。レポートをプレビューするには、データ処理拡張機能およびデータ プロバイダーをレポート作成クライアントにインストールし登録する必要があります。 データ処理拡張機能およびデータ プロバイダーは、インストールされているプラットフォームに対してネイティブでコンパイルされます。 SOAP Web サービスを使用してデータ ソースをプログラムで配置する場合は、データ ソース拡張機能を定義する必要があります。 **RSReportDesigner.config** ファイルのデータ拡張機能の値を使用します。 既定では、このファイルは次のフォルダーにあります。  
  
```  
<drive letter>\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies  
```  
  
 たとえば、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ拡張機能は OLEDB-MD です。  
  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Microsoft ダウンロード センター [およびサードパーティのサイトには、ダウンロードとしてサードパーティの標準](https://www.microsoft.com/download/default.aspx) データ プロバイダーが多数用意されています。 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] パブリック フォーラムで、サードパーティ データ プロバイダーに関する情報を検索することもできます。  
  
> [!NOTE]  
>  標準 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダーは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理機能拡張により提供される機能をすべてサポートするわけではありません。 また、一部の OLE DB データ プロバイダーと ODBC ドライバーは、レポートを作成およびプレビューすることができますが、レポート サーバーでパブリッシュされたレポートをサポートするようには設計されていません。 たとえば、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet の場合、レポート サーバーでの使用はサポートされていません。 詳細については、「[データ処理拡張機能と .NET Framework データ プロバイダー (SSRS)](../../reporting-services/report-data/data-processing-extensions-and-net-framework-data-providers-ssrs.md)」を参照してください。  
  
 カスタムのデータ処理拡張機能の詳細については、「 [Implementing a Data Processing Extension](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)」を参照してください。 標準 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダーの詳細については、 <xref:System.Data> 名前空間のセクションを参照してください。   
  
## <a name="platform-support-for-report-data-sources"></a>レポート データ ソースに対するプラットフォームのサポート  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の配置で使用できるデータ ソースは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエディション、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のバージョン、およびプラットフォームによって異なります。 機能について詳しくは、「[SQL Server の各エディションがサポートする Reporting Services の機能](../../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)」をご覧ください。 このトピックでは、サポートされるデータ ソースに関する情報をバージョンおよびプラットフォームごとに表に示します。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ ソースに関するプラットフォームの考慮事項は、レポート作成クライアントの場合とレポート サーバーの場合で異なります。  
  
### <a name="on-the-report-authoring-client"></a>レポート作成クライアント  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] は 32 ビット アプリケーションです。 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] は、Itanium ベースのプラットフォームではサポートされていません。 x64 プラットフォームでは、レポート デザイナーでレポートを編集およびプレビューするために、32 ビットのデータ プロバイダーを (x86) プラットフォーム ディレクトリにインストールしておく必要があります。  
  
### <a name="on-the-report-server"></a>レポート サーバー  
 レポートを 64 ビットのレポート サーバーに展開する場合は、そのレポート サーバーに、ネイティブでコンパイル済みの 64 ビット データ プロバイダーがインストールされている必要があります。 64 ビット インターフェイスによる 32 ビット データ プロバイダーのラップはサポートされていません。 詳細については、データ プロバイダーのマニュアルを参照してください。  
  
## <a name="supported-data-sources"></a>サポートされるデータ ソース  
 次の表は、レポート データセットおよびレポート モデルのデータを取得するときに使用できる、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] データ処理拡張機能およびデータ プロバイダーを示しています。 拡張機能またはデータ プロバイダーの詳細を参照する場合は、2 番目の列のリンクをクリックしてください。 以下に、表の列の説明を示します。  
  
-   レポート データのソース:アクセス先のデータの種類 (リレーショナル データベース、多次元データベース、フラット ファイル、XML など)。 この列では、"レポートに対して [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] で使用できるデータの種類" がわかります。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ ソースの種類:[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] でデータ ソースを定義するときにドロップダウン リストに表示されるデータ ソースの種類のうちの 1 つ。 このリストには、インストールおよび登録された DPE とデータ プロバイダーから取得した値が設定されます。 この列では、"レポート データ ソースを作成するときにドロップダウン リストから選択するべきデータ ソースの種類" がわかります。  
  
-   データ処理拡張機能/データ プロバイダーの名前:[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能または選択された [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ ソースの種類に対応する他のデータ プロバイダー。 この列では、"データ ソースの種類を選択したときに、どのデータ処理拡張機能またはデータ プロバイダーが使用されるか" がわかります。  
  
-   基になるデータ プロバイダーのバージョン (省略可):データ ソースの種類によっては複数のデータ プロバイダーをサポートします。 たとえば、同じプロバイダーに異なるバージョンが存在する場合や、特定の種類のデータ プロバイダーとして複数のサードパーティによる実装が存在する場合があります。 プロバイダー名は、データ ソースを構成した後の接続文字列に含まれることがよくあります。 この列では、データ ソースの種類を選択した後に、 **[接続プロパティ]** ダイアログ ボックスで選択するべきデータ プロバイダーがわかります。  
  
-   データ ソース *\<platform>* : 対象データ ソースのデータ処理拡張機能またはデータ プロバイダーによりサポートされるデータ ソースのプラットフォーム。 この列では、"このデータ処理拡張機能またはこのデータ プロバイダーが、この種類のプラットフォームのデータ ソースからデータを取得できるかどうか" がわかります。  
  
-   データ ソースのバージョン:DPE またはデータ プロバイダーでサポートされている対象データ ソースのバージョン。 この列では、"このデータ処理拡張機能またはこのデータ プロバイダーが、このバージョンのデータ ソースからデータを取得できるかどうか" がわかります。  
  
-   RS *\<platform>* : カスタムの DPE またはデータ プロバイダーをインストールできる、レポート サーバーおよびレポート作成クライアントのプラットフォーム。 組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能は、インストールされた [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]に含まれています。 カスタムのデータ処理拡張機能または [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダーは、特定のプラットフォーム用にネイティブにコンパイルする必要があります。 この列では、"このデータ処理拡張機能またはこのデータ プロバイダーを、この種類のプラットフォームにインストールできるかどうか" がわかります。  
  
###  <a name="types-of-data-sources"></a><a name="DataSourcesTable"></a> データ ソースの種類  
  
|レポート データの<br /><br /> ソース|Reporting Services データ ソースの種類|データ処理拡張機能/データ プロバイダーの名前|基になるデータ プロバイダーのバージョン<br /><br /> (省略可能)|Data<br /><br /> source<br /><br /> プラットフォーム x86|Data<br /><br /> source<br /><br /> プラットフォーム x64|データ ソースのバージョン|RS<br /><br /> プラットフォーム x86|RS<br /><br /> プラットフォーム x64|  
|-------------------------------|-----------------------------------------|------------------------------------------------------|-------------------------------------------------------|--------------------------------------|--------------------------------------|----------------------------|-------------------------|-------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リレーショナル データベース|[Microsoft SQL Server](#MicrosoftSQLServer)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|System.Data.SqlClient を拡張|Y|Y|SQL Server 2012 以降。|Y|Y|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リレーショナル データベース|OLEDB|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|System.Data.OledbClient を拡張|Y|Y|SQL Server 2012 以降。|Y|Y|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リレーショナル データベース|[ODBC](#ODBC)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|System.Data.OdbcClient を拡張|Y|○|SQL Server 2012 以降。|Y|○|  
|[!INCLUDE[ssSDS](../../includes/sssds-md.md)]|[Microsoft Azure SQL Database](#Azure)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|System.Data.SqlClient を拡張|該当なし|なし|[!INCLUDE[ssSDS](../../includes/sssds-md.md)]|Y|○|
|Azure Synapse Analytics|[Microsoft Azure SQL Database](#Azure)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|System.Data.SqlClient を拡張|該当なし|なし|Azure Synapse Analytics|Y|○| 
|[!INCLUDE[ssDW](../../includes/ssdw-md.md)] アプライアンス|[Microsoft 並列データ ウェアハウス](#PWD)|非推奨とされている [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|該当なし|該当なし|なし|[!INCLUDE[ssDWfull](../../includes/ssdwfull-md.md)]|N|×|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多次元データベースまたはテーブル データベース|[Microsoft SQL Server Analysis Services](#AnalysisServices)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|ADOMD.NET を使用|Y|○|SQL Server 2012 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 以降|Y|○|  
|Power BI Premium データセット (Reporting Services 2019 および Power BI Report Server (2020 年 1 月) 以降) |[Microsoft SQL Server Analysis Services](#AnalysisServices)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|ADOMD.NET を使用|Y|○|SQL Server 2019 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 以降|Y|○|
|Azure Analysis Services |[Microsoft SQL Server Analysis Services](#AnalysisServices)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|ADOMD.NET を使用|Y|○|SQL Server 2017 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 以降|Y|○| 
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多次元データベース|OLEDB|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|System.Data.OledbClient を拡張<br /><br /> バージョン 10.0|Y|○|SQL Server 2012 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|Y|○|
|SharePoint リスト|[Microsoft SharePoint リスト](#SharePointList)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|Lists.asmx または SharePoint オブジェクト モデル API インターフェイスからデータを取得。<br /><br /> 詳細については、「 [注意](#SharePointList)」を参照してください。|N|Y|SharePoint 2013 製品以降|Y|○|   
|XML|[XML](#XML)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|XML データ ソースにはプラットフォーム依存関係がありません。|該当なし|なし|[!INCLUDE[vstecwebservices](../../includes/vstecwebservices-md.md)] またはドキュメント|Y|○|  
|レポート サーバー モデル|レポート モデル|パブリッシュされた SMDL ファイル用の、非推奨とされている [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|モデルのデータ ソースには組み込みのデータ処理拡張機能が使用されます。<br /><br /> Oracle ベースのモデルには、Oracle クライアント コンポーネントが必要です。<br /><br /> Teradata ベースのモデルには、Teradata からの .NET Data Provider for Teradata が必要です。<br /><br /> プラットフォームのサポートについては、Teradata のマニュアルを参照してください。|該当なし|なし|モデルの作成は次から可能です。[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降<br /><br /> [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]<br /><br /> Oracle 9.2.0.3 以降<br /><br /> Teradata V14、v13、v12、および v6.2|N|N|  
|SAP 多次元データベース|SAP BW|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|プラットフォームのサポートについては、SAP のマニュアルを参照してください。|該当なし|なし|SAP BW 7.0 - 7.5|Y|該当なし|  
|[!INCLUDE[extEssbase](../../includes/extessbase-md.md)]|[Hyperion Essbase](#Hyperion)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|プラットフォームのサポートについては、Hyperion のマニュアルを参照してください。|Y|該当なし|[!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 9.3.1|Y|該当なし|  
|Oracle リレーショナル データベース|[Oracle](#OracleClient)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|Oracle クライアント コンポーネント 12c 以降が必要です。|Y|該当なし|Oracle 11g、11g R2、12c、18c、19c|Y|○|  
|Teradata |[Teradata](#Teradata)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|Teradata からの .NET Data Provider for Teradata を拡張<br /><br /> Teradata からの .NET Data Provider for Teradata が必要です。<br /><br /> プラットフォームのサポートについては、Teradata のマニュアルを参照してください。|Y|該当なし|Teradata v15<br /><br />Teradata v14<br /><br /> Teradata v13|○|N|  
|DB2 リレーショナル データベース|登録済みのカスタマイズされたデータ拡張機能名||2004 Host Integration (HI) Server<br /><br /> |Y|該当なし|なし|○|N|  
|汎用 OLE DB データ ソース|OLEDB|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|OLE DB をサポートする任意のデータ ソース。<br /><br /> プラットフォームのサポートについては、データ ソースのマニュアルを参照してください。|Y|該当なし|OLE DB をサポートする任意のデータ ソース。 詳細については、「 [注意](#OLEDBStandard)」を参照してください。|Y|該当なし|  
|汎用 ODBC データ ソース|[ODBC](#ODBCGeneric)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|ODBC をサポートする任意のデータ ソース。<br /><br /> プラットフォームのサポートについては、データ ソースのマニュアルを参照してください。|Y|該当なし|ODBC をサポートする任意のデータ ソース。 詳細については、「 [注意](#ODBCGeneric)」を参照してください。|Y|Y|  
  
 外部データ ソースの使用に関する詳細については、「[外部データ ソースのデータを追加する &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md)」を参照してください。  
  
 サードパーティの標準 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダーは多数あります。 詳細については、サードパーティの Web サイトまたはフォーラムを検索してください。  
  
 カスタム データ処理拡張機能または標準 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダーをインストールおよび登録するには、データ プロバイダー リファレンス ドキュメントを参照する必要があります。 詳細については、「[標準 .NET Framework データ プロバイダーを登録する &#40;SSRS&#41;](../../reporting-services/report-data/register-a-standard-net-framework-data-provider-ssrs.md)」を参照してください。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
## <a name="reporting-services-data-processing-extensions"></a>Reporting Services データ処理拡張機能  
 次のデータ処理拡張機能は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] および [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]と一緒に自動的にインストールされます。 詳細情報およびインストールの確認方法については、「 [RSReportDesigner 構成ファイル](../../reporting-services/report-server/rsreportdesigner-configuration-file.md) 」および「 [RsReportServer.config 構成ファイル](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)」を参照してください。  
  
> [!NOTE]
>  現在、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ処理拡張機能はサポートされていません。  
  
 レポート ビルダーがサポートしているデータ処理拡張機能の詳細については、「[データ接続文字列を作成する - レポート ビルダーおよび SSRS](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)」を参照してください。
  
###  <a name="microsoft-sql-server-data-processing-extension"></a><a name="MicrosoftSQLServer"></a> Microsoft SQL Server データ処理拡張機能  
 データ ソースの種類 **Microsoft SQL Server** は、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をラップし、拡張したものです。 このデータ処理拡張機能は、x86 および [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]ベースのプラットフォーム用にネイティブでコンパイルされ、これらのプラットフォームで実行されます。  
  
 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] では、このデータ拡張機能に関連付けられているクエリ デザイナーは Visual Database Tools デザイナーです。 クエリ デザイナーをグラフィカル モードで使用すると、クエリが分析され、再作成される場合があります。 クエリに使用する [!INCLUDE[tsql](../../includes/tsql-md.md)] 構文を制御するには、テキストベースのクエリ デザイナーを使用します。 詳細については、「 [グラフィカル クエリ デザイナーのユーザー インターフェイス](../../reporting-services/report-data/graphical-query-designer-user-interface.md)」を参照してください。  
  
 詳細については、「[SQL Server の接続の種類 (SSRS)](../../reporting-services/report-data/sql-server-connection-type-ssrs.md)」を参照してください。  
  
 レポート ビルダーでは、このデータ拡張機能に関連付けられているクエリ デザイナーはリレーショナル クエリ デザイナーです。 
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
###  <a name="microsoft-azure-sql-database-processing-extension"></a><a name="Azure"></a> Microsoft Azure SQL Database 処理拡張機能  
 データ ソースの種類 **Microsoft Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)]** は、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をラップし、拡張したものです。  
  
 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]では、このデータ拡張機能に関連付けられているグラフィカル クエリ デザイナーは、リレーショナル クエリ デザイナーです。 **Microsoft SQL Server** のデータ ソースの種類で使う Visual Database Tools デザイナーではありません。  
  
 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]は、 **Microsoft Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)]** と **Microsoft SQL Server** のデータ ソースの種類を自動的に区別し、データ ソースの種類に関連付けられているグラフィカル クエリ デザイナーを開きます。  
  
 クエリ デザイナーをグラフィカル モードで使用すると、クエリが分析され、再作成される場合があります。 クエリの作成に、テキスト ベースのクエリ デザイナーを使用することもできます。 クエリに使用する [!INCLUDE[tsql](../../includes/tsql-md.md)] 構文を制御するには、テキストベースのクエリ デザイナーを使用します。   
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]、Azure Synapse Analytics、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からのデータの取得は似ていますが、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] にのみ適用される要件がいくつかあります。 [Azure SQL 接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/sql-azure-connection-type-ssrs.md) に関するページを参照してください。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
###  <a name="microsoft-sql-server-parallel-data-warehouse-processing-extension"></a><a name="PWD"></a> Microsoft SQL Server 並列データ ウェアハウス処理拡張機能  
このデータ ソースは非推奨となりました。 Microsoft Analytics Platform (APS) に接続するには、SQL Server データ ソースの種類を使用してください。
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
###  <a name="microsoft-sql-server-analysis-services-data-processing-extension"></a><a name="AnalysisServices"></a> Microsoft SQL Server Analysis Services データ処理拡張機能  
 データ ソースの種類に **[Microsoft SQL Server Analysis Services]** を選択した場合は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 用の [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダーを拡張する [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能を選択しています。 このデータ処理拡張機能は、x86 および x64 ベースのプラットフォーム用にネイティブでコンパイルされ、これらのプラットフォームで実行されます。  
  
 このデータ プロバイダーは、ADOMD.NET オブジェクト モデルを使用して、XML for Analysis (XMLA) Version 1.1 を使用したクエリを作成します。 結果はフラット化された行セットとして返されます。 詳細については、「[MDX のための Analysis Services の接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)」、「[DMX のための Analysis Services の接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)」、「[Analysis Services の MDX クエリ デザイナーのユーザー インターフェイス](../../reporting-services/report-data/analysis-services-mdx-query-designer-user-interface.md)」、および「[Analysis Services の DMX クエリ デザイナーのユーザー インターフェイス](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md)」を参照してください。 
 
 Azure Analysis Services および Power BI Premium データセット データ ソースの場合、データ ソースへの接続に使用される資格情報に対して、多要素認証を無効にする必要があることに注意してください。 環境に対して多要素認証を有効にする必要がある場合は、データ ソースで使用される資格情報の多要素認証を無効にするオプションとして、<a href="/azure/active-directory/conditional-access/overview">Azure Active Directory の条件付きアクセス</a>を確認してください。
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ ソースに接続する場合、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ処理拡張機能では、複数値パラメーターがサポートされ、セルおよびメンバーのプロパティが [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] でサポートされる拡張プロパティにマップされます。 詳細については、「[Analysis Services データベースに対する拡張フィールド プロパティ &#40;SSRS&#41;](../../reporting-services/report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ ソースからモデルを作成することもできます。  
  
###  <a name="ole-db-data-processing-extension"></a><a name="OLEDBAll"></a> OLE DB Data Processing Extension  
 OLE DB データ処理拡張機能では、レポートで使用するデータ ソースのバージョンに基づいて、追加のデータ プロバイダー レイヤーを選択する必要があります。 特定のデータ プロバイダーを選択しなかった場合は、既定値が使用されます。 [データ ソース] または [共有データ ソース] ダイアログ ボックスで **[編集]** ボタンをクリックして **[接続プロパティ]** ダイアログ ボックスにアクセスし、特定のデータ プロバイダーを選びます。  
  
 OLE DB に関連付けられたクエリ デザイナーの詳細については、「 [グラフィカル クエリ デザイナーのユーザー インターフェイス](../../reporting-services/report-data/graphical-query-designer-user-interface.md)」を参照してください。 OLE DB プロバイダーに対するサポートの詳細については、 [サポート技術情報の「](https://support.microsoft.com/default.aspx/kb/811241) Visual Studio .NET デザイナーのツールでサポートされる OLE DB プロバイダー [!INCLUDE[msCoName](../../includes/msconame-md.md)] 」を参照してください。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
####  <a name="ole-db-for-sql-server"></a><a name="OLEDBSQL"></a> OLE DB for SQL Server  
 データ ソースの種類に **[OLE DB]** を選択した場合は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Data Provider for OLE DB を拡張した [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ処理拡張機能が選択されます。 このデータ処理拡張機能は、x86 および x64 プラットフォーム用にネイティブでコンパイルされ、これらのプラットフォームで実行されます。  
  
 詳細については、「[OLE DB の接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/ole-db-connection-type-ssrs.md)」を参照してください。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
#### <a name="ole-db-for-olap-70"></a>OLE DB for OLAP 7.0  
 OLE DB Provider for OLAP Services 7.0 はサポートされません。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
####  <a name="ole-db-for-oracle"></a><a name="OracleOLEDB"></a> OLE DB for Oracle  
 OLE DB for Oracle データ処理拡張機能では、次の Oracle データ型はサポートされません: BLOB、CLOB、NCLOB、BFILE、UROWID。  
  
 位置に依存する無名パラメーターはサポートされます。 この拡張機能では、名前付きパラメーターはサポートされません。 名前付きパラメーターを使用するには、 [Oracle](#OracleClient) データ処理拡張機能を使用します。  
  
 Oracle をデータ ソースとして構成する方法の詳細については、「 [Reporting Services を使用して Oracle データ ソースの構成およびアクセスを行う方法](https://support.microsoft.com/kb/834305)」を参照してください。 追加の権限の構成の詳細については、 [サポート技術情報の「](https://support.microsoft.com/kb/870668) NETWORK SERVICE セキュリティ プリンシパルに権限を追加する方法 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 」を参照してください。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
####  <a name="ole-db-standard-net-framework-data-provider"></a><a name="OLEDBStandard"></a> 標準の OLE DB .NET Framework データ プロバイダー  
 OLE DB [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダーをサポートするデータ ソースからデータを取得するには、データ ソースの種類に **OLE DB** を使用して、既定のデータ プロバイダーを選択するか、または **[接続文字列]** ダイアログ ボックスでインストール済みのデータ プロバイダーから選択します。  
  
> [!NOTE]  
>  レポート作成クライアントのレポートのプレビューに対応しているデータ プロバイダーもありますが、すべての OLE DB データ プロバイダーが、レポート サーバーでパブリッシュされたレポートをサポートするように設計されているわけではありません。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
###  <a name="odbc-data-processing-extension"></a><a name="ODBC"></a> ODBC Data Processing Extension  
 データ ソースの種類に **[ODBC]** を選択した場合は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Data Provider for ODBC を拡張した [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ処理拡張機能が選択されます。 このデータ処理拡張機能は、x86 および [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)] プラットフォーム用にネイティブでコンパイルされ、これらのプラットフォームで動作します。 この拡張機能を使用すると、ODBC プロバイダーを持つ任意のデータ ソースのデータに接続し、データを取得できます。  
  
> [!NOTE]  
>  レポート作成クライアントのレポートのプレビューに対応しているデータ プロバイダーもありますが、すべての ODBC データ プロバイダーが、レポート サーバーでパブリッシュされたレポートをサポートするように設計されているわけではありません。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
####  <a name="odbc-standard-net-framework-data-provider"></a><a name="ODBCGeneric"></a> 標準の ODBC .NET Framework データ プロバイダー  
 標準の ODBC [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダーをサポートするデータ ソースからデータを取得するには、データ ソースの種類に **[ODBC]** を使用して、既定のデータ プロバイダーを選択するか、または **[接続文字列]** ダイアログ ボックスでインストール済みのデータ プロバイダーから選択します。  
  
> [!NOTE]  
>  レポート作成クライアントのレポートのプレビューに対応しているデータ プロバイダーもありますが、すべての ODBC データ プロバイダーが、レポート サーバーでパブリッシュされたレポートをサポートするように設計されているわけではありません。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
###  <a name="oracle-data-processing-extension"></a><a name="OracleClient"></a> Oracle データ処理拡張機能  
 データ ソースの種類として **[Oracle]** を選択すると、Oracle Data Provider を直接使う [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能が選択されて、System.Data.OracleClient を経由しなくなります。 Oracle データベースからレポート データを取得するには、管理者が Oracle クライアント ツールをインストールする必要があります。 クライアント アプリケーションのバージョンは 11g 以降である必要があります。 これらのツールをレポート作成クライアントにインストールすると、レポートをプレビューすることができ、レポート サーバーにインストールすると、パブリッシュされたレポートを表示できます。  
 
Oracle クライアント ツールをインストールするには、次のようにします。
 
1.  [Oracle のダウンロード サイト](https://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)に移動します
2.  Windows 用 ODAC 12c リリース 4 (12.1.0.2.4) をダウンロードします (サーバー用の 64 ビット、ツール用の 32 ビット)。
3.  Data Provider for .NET 4 をインストールします
  
 この拡張機能では、名前付きパラメーターがサポートされます。 Oracle Version 11g 以降の場合、複数値パラメーターがサポートされます。 位置に依存する無名パラメーターを使用するには、OLE DB データ処理拡張機能と [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Oracle データ プロバイダーを組み合わせて使用します。 Oracle をデータ ソースとして構成する方法の詳細については、「 [Reporting Services を使用して Oracle データ ソースの構成およびアクセスを行う方法](https://support.microsoft.com/kb/834305)」を参照してください。 追加の権限の構成の詳細については、 [サポート技術情報の「](https://support.microsoft.com/kb/870668) NETWORK SERVICE セキュリティ プリンシパルに権限を追加する方法 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 」を参照してください。  
  
 複数の入力パラメーターを使用してストアド プロシージャからデータを取得できますが、ストアド プロシージャから返せるのは 1 つの出力カーソルのみです。 詳細については、「DataReader を使用してデータを取得する」の「[Oracle REF CURSOR による結果の取得](/dotnet/framework/data/adonet/retrieving-data-using-a-datareader#returning-results-with-oracle-ref-cursors)」を参照してください。
  
 詳細については、「[Oracle の接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/oracle-connection-type-ssrs.md)」を参照してください。 関連付けられたクエリ デザイナーの詳細については、「 [グラフィカル クエリ デザイナーのユーザー インターフェイス](../../reporting-services/report-data/graphical-query-designer-user-interface.md)」を参照してください。  
  
 Oracle データベースに基づくモデルを作成することもできます。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
###  <a name="teradata-data-processing-extension"></a><a name="Teradata"></a> Teradata データ処理拡張機能  
 データ ソースの種類に **[Teradata]** を選択した場合は、.NET Framework Data Provider for Teradata を拡張した [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能が選択されます。 Teradata からレポート データを取得するには、システム管理者はレポート作成クライアントに .NET Framework Data Provider for Teradata をインストールしてクライアント上でレポートを編集およびプレビューし、レポート サーバー上でパブリッシュされたレポートを表示する必要があります。  
  
 レポート サーバー プロジェクトには、この拡張で使用できるグラフィカル クエリ デザイナーはありません。 クエリを作成するにはテキストベースのクエリ デザイナーを使用する必要があります。  
  
 次の表に、 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]のレポート定義でデータ ソースを定義する場合にサポート対象となる .NET Data Provider for Teradata のバージョンを示します。  
  
|[!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] のバージョン|Teradata のバージョン|.NET Framework Data Provider for Teradata のバージョン|  
|-----------------------------------|-------------------------------|-------------------------------------------------------|    
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|12.00|12.00.01|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|6.20|12.00.01|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|13.00|13.0.0.1|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|12.00|12.00.01|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|6.20|12.00.01|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|13.00|13.0.0.1|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|6.20|12.00.01|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|12.00|12.00.01|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|13.00|13.0.0.1|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|14.00|14.00.01| 
|SQL Server 2016|13.00|13.0.0.1|  
|SQL Server 2016|14.00|14.00.01|
|SQL Server 2016|15.00|15.00.01| 
  
 この拡張機能では、複数値パラメーターがサポートされます。 クエリ モード TEXT の EXECUTE コマンドを使用すると、クエリでマクロを指定できます。  
  
 詳細については、「[Teradata の接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/teradata-connection-type-ssrs.md)」を参照してください。  
 
 [データ ソースの表に戻る](#DataSourcesTable)  
  
###  <a name="sharepoint-list-data-extension"></a><a name="SharePointList"></a> SharePoint リスト データ拡張機能  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、レポートのデータ ソースに SharePoint リストを使用できるように、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint リスト データ拡張機能が含まれています。 リスト データは、以下から取得できます。  
  
-   SharePoint Server 2016  

-   [!INCLUDE[SPS2013](../../includes/sps2013-md.md)]  
  
 SharePoint リスト データ プロバイダーの実装には、3 つの方法があります。  
  
1.  [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]のレポート ビルダーまたはレポート デザイナーなどのレポート作成環境、あるいはネイティブ モードで構成されたレポート サーバーの場合、リスト データは SharePoint サイトの Lists.asmx Web サービスから取得されます。  
  
2.  SharePoint 統合モードで構成されたレポート サーバーの場合、リスト データは対応する Lists.asmx Web サービス、または SharePoint API に対するプログラム呼び出しのいずれかから取得されます。 このモードでは、SharePoint ファームからリスト データを取得できます。  
  
3.  [!INCLUDE[SPS2013](../../includes/sps2013-md.md)] および SharePoint Server 2016 では、[!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint テクノロジ用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインを使うことで、SharePoint サイトの Lists.asmx Web サービスから、または SharePoint ファームを構成する SharePoint サイトから、リスト データを取得できます。 このシナリオは、レポート サーバーが不要なため、 *ローカル モード* とも呼ばれています。  
  
 指定できる資格情報は、クライアント アプリケーションが使用している実装によって異なります。 詳細については、「[SharePoint リストの接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/sharepoint-list-connection-type-ssrs.md)」を参照してください。  
  
###  <a name="xml-data-processing-extension"></a><a name="XML"></a> XML データ処理拡張機能  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、レポート内で XML データを使用できるように、XML データ処理拡張機能が含まれています。 データは、XML ドキュメントや Web サービス、または URL を使用してアクセス可能な Web ベースのアプリケーションから取得できます。 詳細については、「[XML の接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/xml-connection-type-ssrs.md)」を参照してください。 関連付けられているクエリ デザイナーの詳細については、「 [グラフィカル クエリ デザイナーのユーザー インターフェイス](../../reporting-services/report-data/graphical-query-designer-user-interface.md)」の「テキスト ベースのクエリ デザイナー」セクションを参照してください。
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
###  <a name="sap-bw-data-processing-extension"></a><a name="SAPBW"></a> SAP BW データ処理拡張機能  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、SAP BW データ ソースからのデータをレポートで使用できるデータ処理拡張機能が含まれます。
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
###  <a name="hyperion-essbase-business-intelligence-data-processing-extension"></a><a name="Hyperion"></a> Hyperion Essbase Business Intelligence のデータ拡張機能  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、レポートの [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] データ ソースからのデータを使用できるデータ処理拡張機能が含まれます。  
  
 詳細については、「[Hyperion Essbase の接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/hyperion-essbase-connection-type-ssrs.md)」を参照してください。 関連付けられているクエリ デザイナーの詳細については、「 [Hyperion Essbase Query Designer User Interface](../../reporting-services/report-data/hyperion-essbase-query-designer-user-interface.md)」を参照してください。  
  
 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] の詳細については、[Hyperion Essbase での SQL Server Reporting Services の使用](../../reporting-services/report-data/hyperion-essbase-query-designer-user-interface.md)に関するページを参照してください。 
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
## <a name="see-also"></a>参照  
 [データ接続文字列を作成する - レポート ビルダーおよび SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [レポート データセット (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)  
その他の質問 [Reporting Services のフォーラムにアクセスします](https://go.microsoft.com/fwlink/?LinkId=620231)
  
