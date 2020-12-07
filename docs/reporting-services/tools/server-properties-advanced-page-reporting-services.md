---
title: サーバーのプロパティの [詳細設定] ページ | Microsoft Docs
description: '[サーバーのプロパティ] の [詳細設定] ページを使用すると、レポート サーバーのシステム プロパティを設定できます。 このツールにはグラフィカル ユーザー インターフェイスが用意されているので、コードを記述しなくてもプロパティを設定できます。'
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
ms.date: 10/19/2020
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: e8bb8de8d13a9b7696bb6505363b15d38cd35994
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194278"
---
# <a name="server-properties-advanced-page---power-bi-report-server--reporting-services"></a>[サーバーのプロパティ] の [詳細設定] ページ - Power BI Report Server と Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

このページを使用して、レポート サーバーのシステム プロパティを設定します。 システム プロパティを設定する方法はいくつかあります。 このツールにはグラフィカル ユーザー インターフェイスが用意されているので、コードを記述しなくてもプロパティを設定できます。

このページを開くには、SQL Server Management Studio を起動してレポート サーバー インスタンスに接続し、レポート サーバー名を右クリックして **[プロパティ]** をクリックします。 **[詳細設定]** を選択するとこのページが開きます。

## <a name="options"></a>Options

### <a name="accesscontrolallowcredentials"></a>AccessControlAllowCredentials
(Power BI Report Server、Reporting Services 2017 以降のみ) `credentials` フラグが true に設定されている場合に、クライアント要求に対する応答を公開できるかどうかを示します。 既定値は **false** です。

### <a name="accesscontrolallowheaders"></a>AccessControlAllowHeaders
(Power BI Report Server、Reporting Services 2017 以降のみ) クライアントから要求を行うときにサーバーで許可するヘッダーのコンマ区切りの一覧。 このプロパティは、空の文字列にすることができます。* を指定すると、すべてのヘッダーが許可されます。

### <a name="accesscontrolallowmethods"></a>AccessControlAllowMethods
(Power BI Report Server、Reporting Services 2017 以降のみ) クライアントから要求を行うときにサーバーで許可する HTTP メソッドのコンマ区切りの一覧。 既定値は GET、PUT、POST、PATCH、DELETE です。* を指定すると、すべてのメソッドが許可されます。

### <a name="accesscontrolalloworigin"></a>AccessControlAllowOrigin
(Power BI Report Server、Reporting Services 2017 以降のみ) クライアントから要求を行うときにサーバーで許可する要求元のコンマ区切りの一覧。 既定値は空白で、すべての要求を防ぎます。* を指定すると、資格情報が設定されていない場合にすべての要求元が許可されます。資格情報が指定されている場合は、要求元の明示的なリストを指定する必要があります。

### <a name="accesscontrolexposeheaders"></a>AccessControlExposeHeaders
(Power BI Report Server、Reporting Services 2017 以降のみ) サーバーからクライアントに対して公開されるヘッダーのコンマ区切りの一覧。 既定値は空白です。

### <a name="accesscontrolmaxage"></a>AccessControlMaxAge
(Power BI Report Server、Reporting Services 2017 以降のみ) プレフライト要求の結果をキャッシュできる秒数を指定します。 既定値は 600 (10 分) です。

### <a name="allowedresourceextensionsforupload"></a>AllowedResourceExtensionsForUpload
(Power BI Report Server、Reporting Services 2017 以降のみ) レポート サーバーにアップロードできるリソースの拡張機能を設定します。 &ast;.rdl や &ast;.pbix のような組み込みのファイルの種類用の拡張子は含める必要はありません。 既定値は "&ast;、&ast;.xml、&ast;.xsd、&ast;.xsl、&ast;.png、&ast;.gif、&ast;.jpg、&ast;.tif、&ast;.jpeg、&ast;.tiff、&ast;.bmp、&ast;.pdf、&ast;.svg、&ast;.rtf、&ast;.txt、&ast;.doc、&ast;.docx、&ast;.pps、&ast;.ppt、&ast;.pptx" です。

### <a name="customheaders"></a>CustomHeaders 

(Power BI Report Server 2020 年 1 月、Reporting Services 2019 以降のみ)

指定された正規表現パターンに一致するすべての URL のヘッダー値を設定します。 ユーザーは、有効な XML を使用して CustomHeaders 値を更新し、選択した要求 URL のヘッダー値を設定できます。 管理者は、XML 内に任意の数のヘッダーを追加できます。 Reporting Services 2019 では、既定でカスタム ヘッダーは存在せず、値は空白です。 Power BI Report Server 2020 年 1 月以降では、値は既定で次のようになっています。

```xml
<CustomHeaders>
    <Header>
        <Name>X-Frame-Options</Name>
        <Pattern>(?(?=.*api.*|.*rs:embed=true.*|.*rc:toolbar=false.*)(^((?!(.+)((\/api)|(\/(.+)(rs:embed=true|rc:toolbar=false)))).*$))|(^(?!(http|https):\/\/([^\/]+)\/powerbi.*$)))</Pattern>
        <Value>SAMEORIGIN</Value>
    </Header>
</CustomHeaders>
```

> [!NOTE]
> ヘッダーが多すぎると、パフォーマンスに影響する可能性があります。 

トポロジの構成を検証して、一連のヘッダーが Reporting Services の配置と互換性があることを確認することをお勧めします。 ブラウザーにも適切な設定がない場合は、ブラウザーでエラーが発生する設定を選択することができます。 たとえば、サーバーが https 用に構成されていない場合は、HSTS 構成を追加しないでください。 互換性のないヘッダーは、ブラウザー レンダリング エラーになる可能性があります。

#### <a name="customheaders-xml-format"></a>CustomHeaders XML 形式

```xml
<CustomHeaders>
    <Header>
        <Name>{Name of the header}</Name>
        <Pattern>{Regex pattern to match URLs}</Pattern>
        <Value>{Value of the header}</Value>
    </Header>
</CustomHeaders>
```

#### <a name="setting-the-customheaders-property"></a>CustomHeaders プロパティの設定

- パラメーターとして CustomHeaders プロパティを渡す [SetSystemProperties](/dotnet/api/reportservice2010.reportingservice2010.setsystemproperties) SOAP エンドポイントを使用して設定できます。
- REST エンドポイント [UpdateSystemProperties](https://app.swaggerhub.com/apis/microsoft-rs/PBIRS/2.0#/System/UpdateSystemProperties): `/System/Properties` を使用して CustomHeaders プロパティを渡すことができます

#### <a name="example"></a>例

次の例は、一致する正規表現パターンを持つ URL の HSTS およびその他のカスタム ヘッダーを設定する方法を示しています。

```xml
<CustomHeaders>
    <Header>
        <Name>Strict-Transport-Security</Name>
        <Pattern>(.+)\/Reports\/mobilereport(.+)</Pattern>
        <Value>max-age=86400; includeSubDomains=true</Value>
    </Header>
    <Header>
        <Name>Embed</Name>
        <Pattern>(.+)(/reports/)(.+)(rs:embed=true)</Pattern>
        <Value>True</Value>
    </Header>
</CustomHeaders>
```

上記の XML の最初のヘッダーによって、一致する要求に `Strict-Transport-Security: max-age=86400; includeSubDomains=true` ヘッダーが追加されます。
- http://adventureworks/Reports/mobilereport/New%20Mobile%20Report - 正規表現が一致し、HSTS ヘッダーが設定されます
- http://adventureworks/ReportServer/mobilereport/New%20Mobile%20Report - 一致しません

上記の XML の 2 番目のヘッダーによって、`/reports/` および `rs:embed=true` クエリ パラメーターを含む URL の `Embed: True` ヘッダーが追加されます。
- https://adventureworks/reports/mobilereport/New%20Mobile%20Report?rs:embed=true - 一致します
- https://adventureworks/reports/mobilereport/New%20Mobile%20Report?rs:embed=false - 一致しません

### <a name="editsessioncachelimit"></a>EditSessionCacheLimit
レポート編集セッションでアクティブにできるデータ キャッシュ エントリの数を指定します。 既定の数は 5 です。  

### <a name="editsessiontimeout"></a>EditSessionTimeout
レポート編集セッションがタイムアウトするまでの秒数を指定します。既定値は 7,200 秒 (2 時間) です。 

### <a name="enablecdnvisuals"></a>EnableCDNVisuals 
(Power BI レポート サーバーのみ) 有効にすると、Power BI レポートには、Microsoft がホストするコンテンツ配信ネットワーク (CDN) から最新の認定カスタム ビジュアルが読み込まれます。 サーバーからインターネット リソースにアクセスできない場合は、このオプションをオフにすることができます。 この場合、サーバーに発行されたレポートからカスタム ビジュアルが読み込まれます。 既定値は **True** です。  

###  <a name="enableclientprinting"></a>EnableClientPrinting  
レポート サーバーからのダウンロードに RSClientPrint ActiveX コントロールが使用可能かどうかを示します。 有効値は **true** および **false**です。 既定値は **true** です。 このコントロールに必要な追加設定に関する詳細については、「 [Reporting Services のクライアント側印刷機能の有効化と無効化](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)」を参照してください。  

### <a name="enablecustomvisuals"></a>EnableCustomVisuals 
(Power BI Report Server のみ) Power BI カスタム ビジュアルの表示を有効にします。 値は True と False です。 *既定値は True です。*  

###  <a name="enableexecutionlogging"></a>EnableExecutionLogging  
レポート実行のログ記録が有効になっているかどうかを示します。 既定値は **true** です。 レポート サーバー実行ログの詳細については、「 [レポート サーバー ExecutionLog と ExecutionLog3 ビュー](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)」を参照してください。  

### <a name="enableintegratedsecurity"></a>EnableIntegratedSecurity
Windows 統合セキュリティをレポート データ ソース接続でサポートするかどうかを決定します。 既定値は **True**です。 有効な値は次のとおりです。

|値|説明|
|---------|---------|
|**True**|Windows 統合セキュリティが有効になります。|
|**False**|Windows 統合セキュリティは無効になります。 Windows 統合セキュリティを使用するように構成されているレポート データ ソースは実行されません。|

### <a name="enableloadreportdefinition"></a>EnableLoadReportDefinition
ユーザーがレポート ビルダーのレポートから計画されていないレポートを実行できるかどうかを指定するには、このオプションを選択します。 このオプションをオンにすると、レポート サーバーの **EnableLoadReportDefinition** プロパティが設定されます。  

このオプションをオフにした場合は、このプロパティが False に設定されます。 データ ソースとしてレポート モデルを使用するレポートのクリックスルー レポートは、レポート サーバーによって生成されません。 LoadReportDefinition メソッドへの呼び出しはいずれもブロックされます。  

この機能を無効にすることで、悪意のあるユーザーが LoadReportDefinition 要求でレポート サーバーを過負荷にするサービス拒否攻撃の脅威を軽減することができます。  

### <a name="enablemyreports"></a>EnableMyReports  
個人用レポート機能が有効になっているかどうかを指定します。 値 **true** は、機能が有効になっていることを示します。  

### <a name="enablepowerbireportexportdata"></a>EnablePowerBIReportExportData 
(Power BI Report Server のみ) Power BI ビジュアルからの Power BI Report Server データのエクスポートを有効にします。 値は True、False です。  既定値は True です。 

### <a name="enablepowerbireportexportunderlyingdata"></a>EnablePowerBIReportExportUnderlyingData 
(Power BI Report Server のみ) ユーザーが Power BI Report Server 上の Power BI ビジュアルから基になるデータをエクスポートできるかどうかを示します。 True の値は、機能が有効になっていることを示します。

### <a name="enableremoteerrors"></a>EnableRemoteErrors
リモート コンピューターからレポートを要求したユーザーに返されるエラー メッセージに、外部エラー情報 (レポート データ ソースに関するエラー情報など) を含めます。 有効値は **true** および **false**です。 既定値は **false** です。 詳細については、「[リモート エラーの有効化 (Reporting Services)](../../reporting-services/report-server/enable-remote-errors-reporting-services.md)」を参照してください。  

### <a name="enabletestconnectiondetailederrors"></a>EnableTestConnectionDetailedErrors
ユーザーがレポート サーバーを使用してデータ ソース接続をテストする際に、クライアント コンピューターに詳細なエラー メッセージを送信するかどうかを指定します。 既定値は **true** です。 このオプションを **false**に設定した場合は、一般的なエラー メッセージだけが送信されます。

###  <a name="executionlogdayskept"></a>ExecutionLogDaysKept  
レポート実行情報を実行ログに保持する日数。 このプロパティの有効値は、 **-1** - **2**、**147**、**483**、**647**です。 値が **-1** の場合、エントリは実行ログ テーブルから削除されません。 既定値は **60**です。  

> [!NOTE]
> **0 の値を設定すると、実行ログからすべてのエントリが "** *削除*" されます。 値が **-1** の場合、実行ログのエントリは保持され、それらは削除されません。

### <a name="executionloglevel"></a>ExecutionLogLevel
実行ログ レベルを設定します。 *既定値は Normal です。*

### <a name="externalimagestimeout"></a>ExternalImagesTimeout
この時間以内に外部画像ファイルを取得しないと接続がタイムアウトになる時間の長さを指定します。既定値は **600** 秒です。  

### <a name="interprocesstimeoutminutes"></a>InterProcessTimeoutMinutes
(Power BI Report Server、Reporting Services 2019 以降のみ) プロセス タイムアウトを分単位で設定します。 *既定値は 30 です。*

### <a name="maxfilesizemb"></a>MaxFileSizeMb
レポートの最大ファイル サイズを MB 単位で設定します。 *既定値は 1000 です。最大値は 2000 です。*

### <a name="modelcleanupcycleminutes"></a>ModelCleanupCycleMinutes 
(Power BI Report Server のみ) 使用されていないモデルがメモリ内にあるかどうかを確認する頻度を分単位で設定します。 *既定値は 15 です。*

### <a name="modelexpirationminutes"></a>ModelExpirationMinutes 
(Power BI Report Server のみ) 未使用のモデルがメモリから削除される頻度を分単位で設定します。 *既定値は 60 です。*

###  <a name="myreportsrole"></a>MyReportsRole  
ユーザーの個人用レポート フォルダーに、セキュリティ ポリシーを作成する際に使用するロールの名前。 既定値は **My Reports Role**です。  

### <a name="officeaccesstokenexpirationseconds"></a>OfficeAccessTokenExpirationSeconds 
(Power BI Report Server、Reporting Services 2019 以降のみ) Office アクセス トークンの有効期限を秒単位で設定します。 *既定値は 60 です。*

### <a name="officeonlinediscoveryurl"></a>OfficeOnlineDiscoveryURL 
(Power BI Report Server のみ) Excel ブックを表示するための Office Online Server インスタンスのアドレスを設定します。

### <a name="rdlxreporttimetout"></a>RDLXReportTimetout
RDLX レポート *(SharePoint Server の Power View レポート)* レポート サーバーの名前空間で管理されるすべてのレポートに対する、処理タイムアウト値 (秒単位)。 この値はレポート レベルでオーバーライドできます。 このプロパティを設定すると、レポート サーバーは指定された時間が経過した後、レポートの処理を停止しようとします。 有効値は **-1** ～ **2**、**147**、**483**、**647**です。 値に **-1**を設定すると、名前空間内のレポートが処理中にタイムアウトしません。 既定値は **1800**です。

### <a name="requireintune"></a>RequireIntune
(Power BI Report Server、Reporting Services 2017 以降のみ) Intune で Power BI モバイル アプリを介して組織のレポートにアクセスすることを必須にします。 *既定値は False です。*

### <a name="restrictedresourcemimetypeforupload"></a>RestrictedResourceMimeTypeForUpload
(Power BI Report Server 2019 年 1 月、Reporting Services 2017 以降のみ) ユーザーがコンテンツをアップロードすることを許可されていない一連の MIME タイプ。 制限された MIME タイプに既に格納されているリソースは、ブラウザーから開いたり実行したりするのではなく、application/octet-stream 形式でのみダウンロードできます。  既定では、この一覧に制限されたアイテムはありませんが、組織には、安全性の高いエクスペリエンスを提供するために、これを設定することをお勧めします。

### <a name="schedulerefreshtimeoutminutes"></a>ScheduleRefreshTimeoutMinutes 
(Power BI Report Server のみ) AS モデルが埋め込まれた Power BI レポートに対してスケジュールされた更新のデータ更新のタイムアウト (分単位)。 既定値は 120 分です。

### <a name="sessiontimeout"></a>SessionTimeout
セッションがアクティブな状態になっている期間 (秒単位)。 既定値は **600**です。  

### <a name="sharepointintegratedmode"></a>SharePointIntegratedMode
この読み取り専用プロパティは、サーバー モードを示します。 この値が False の場合、レポート サーバーはネイティブ モードで実行されます。  

### <a name="showdownloadmenu"></a>ShowDownloadMenu
(Power BI Report Server、Reporting Services 2017 以降のみ) クライアント ツールのダウンロード メニューを有効にします。 *既定値は true です。*

### <a name="sitename"></a>SiteName
Web ポータルのページ タイトルに表示されるレポート サーバー サイトの名前。 既定値は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] です。 このプロパティには空の文字列を指定できます。 最大長は 8,000 文字です。  

### <a name="snapshotcompression"></a>SnapshotCompression
スナップショットの圧縮方法を定義します。 既定値は **SQL**です。 有効な値は次のとおりです。

|値|説明|
|---------|---------|
|**SQL**|スナップショットは、レポート サーバー データベースへの格納時に圧縮されます。 この圧縮は現在の動作です。|
|**なし**|スナップショットは圧縮されません。|
|**すべて**|すべてのストレージ オプションのスナップショットが圧縮されます。このオプションには、レポート サーバー データベースやファイル システムが含まれます。|

### <a name="storedparameterslifetime"></a>StoredParametersLifetime
保存したパラメーターを保持できる最大日数を指定します。 有効値は **-1**、 **+1** ～ **2,147,483,647**です。 既定値は **180** 日です。  

### <a name="storedparametersthreshold"></a>StoredParametersThreshold
レポート サーバーが保存できるパラメーター値の最大数を指定します。 有効値は **-1**、 **+1** ～ **2,147,483,647**です。 既定値は **1500**です。  

### <a name="supportedhyperlinkschemes"></a>SupportedHyperlinkSchemes 
(Power BI Report Server 2019 年 1 月、Reporting Services 2019 以降のみ) 表示できるハイパーリンク アクションで定義できる URI スキームのコンマ区切りの一覧を設定するか、"&ast;" を設定してすべてのハイパーリンク スキームを有効にします。 たとえば、"http,https" を設定すると、"https://www. contoso.com” へのハイパーリンクは許可されますが、“mailto:bill@contoso.com” または “javascript:window.open(‘ www.contoso.com’, ‘_blank’)” へのハイパーリンクは削除されます。 既定値は “&ast;” です。

### <a name="systemreporttimeout"></a>SystemReportTimeout
レポート サーバー名前空間で管理されているすべてのレポートの既定のレポート処理タイムアウト値 (秒単位)。 この値はレポート レベルでオーバーライドできます。 このプロパティを設定すると、レポート サーバーは指定された時間が経過した後、レポートの処理を停止しようとします。 有効値は **-1** ～ **2**、**147**、**483**、**647**です。 値に **-1**を設定すると、名前空間内のレポートが処理中にタイムアウトしません。 既定値は **1800**です。  

### <a name="systemsnapshotlimit"></a>SystemSnapshotLimit
レポートに格納されるスナップショットの最大数。 有効値は **-1** ～ **2**、**147**、**483**、**647**です。 値が **-1**の場合、スナップショットに制限はありません。  

### <a name="timerinitialdelayseconds"></a>TimerInitialDelaySeconds
(Power BI Report Server、Reporting Services 2017 以降のみ) 初期時間の遅延時間 (秒単位) を設定します。 *既定値は 60 です。*

### <a name="trustedfileformat"></a>TrustedFileFormat
(Power BI Report Server、Reporting Services 2017 以降のみ) ブラウザー内で Reporting Services ポータル サイト以下の開いているすべての外部ファイル形式を設定します。 外部ファイルの形式が一覧に含まれない場合は、オプションのダウンロードを求めるメッセージがブラウザーに表示されます。 既定値は、jpg、jpeg、jpe、wav、bmp、pdf、img、gif、json、mp4、web、png です。

### <a name="usesessioncookies"></a>UseSessionCookies
レポート サーバーがクライアント ブラウザーとの通信時にセッションクッキーを使用する必要があるかどうかを指定します。 既定値は **true** です。  

## <a name="see-also"></a>参照

[レポート サーバーのプロパティを設定する (Management Studio)](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
[Management Studio でレポート サーバーに接続する](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
[Reporting Services のプロパティ](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties.md)   
[Management Studio のレポート サーバーの F1 ヘルプ](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
[レポート サーバーのシステム プロパティ](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
[配置タスクおよび管理タスクのスクリプト作成](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
[個人用レポートの有効化と無効化](../../reporting-services/report-server/enable-and-disable-my-reports.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
