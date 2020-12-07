---
title: レポート ビューアー コントロールの概要
description: Report Viewer コントロールを使用して、Reporting Services の RDL レポートを WebForms アプリと WinForms アプリに統合できます。
ms.custom: seo-lt-2019
ms.date: 09/01/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: conceptual
ms.assetid: 01a821c4-2920-400c-be03-93d26c749bb1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d4195123fbe1660c1c081c810d2b5b6b0feebd80
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891512"
---
# <a name="integrate-reporting-services-using-the-report-viewer-controls---get-started"></a>レポート ビューアー コントロールを使用した Reporting Services の統合 - 概要

Report Viewer コントロールを使用して、Reporting Services の RDL レポートを WebForms アプリと WinForms アプリに統合できます。 最新の更新プログラムの詳細については、[changelog](./release-notes-ssrs-application-integration.md) を参照してください。

## <a name="add-the-report-viewer-control-to-a-new-web-project"></a>新しい Web プロジェクトにレポート ビューアー コントロールを追加する

1. 新しい **[ASP.NET 空の Web サイト]** を作成するか、既存の ASP.NET プロジェクトを開きます。

    .NET Framework 4.6 以降のバージョンを使用できます。

    ![新しい ASP.NET 空の Web サイトの作成のスクリーンショット。](../../reporting-services/application-integration/media/ssrs-create-new-aspnet-project-4-6.png)

2. **NuGet パッケージ マネージャー コンソール**から ReportViewer 2016 コントロール NuGet パッケージをインストールします。

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WebForms
    ```
3. 新しい .aspx パッケージをプロジェクトに追加し、ページ内で使用できるように ReportViewer コントロール アセンブリを登録します。

    ```
    <%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>
    ```
    
4. ページに **ScriptManagerControl** を追加します。

5. ページに ReportViewer コントロールを追加します。 リモート レポート サーバーでホストされているレポートを参照するように次のスニペットを更新することができます。

    ```
    <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
      <ServerReport ReportPath="" ReportServerUrl="" />
    </rsweb:ReportViewer>
    ```
    
最終的なページは次のようになります。

```html
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="Sample" %>

<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <meta http-equiv="X-UA-Compatible" content="IE=edge" /> 
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
    <asp:ScriptManager runat="server"></asp:ScriptManager>        
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
            <ServerReport ReportServerUrl="https://AContosoDepartment/ReportServer" ReportPath="/LatestSales" />
        </rsweb:ReportViewer>
    </form>
</body>
</html>
```

## <a name="update-an-existing-project-to-use-the-report-viewer-control"></a>レポート ビューアー コントロールを使用するように既存のプロジェクトを更新する

すべてのアセンブリ参照がバージョン *15.0.0.0* に更新されていることを確認します。ビューア― コントロールを参照しているプロジェクトの web.config とすべての .aspx ページも含めて確認してください。

### <a name="sample-webconfig-changes"></a>サンプル web.config の変更

```xml
<?xml version="1.0"?>
<!--
  For more information on how to configure your ASP.NET application, please visit
  https://go.microsoft.com/fwlink/?LinkId=169433
  -->
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.6">
      <assemblies>
        <!-- All assemblies updated to version 15.0.0.0. -->
        <add assembly="Microsoft.ReportViewer.Common, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.DataVisualization, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.Design, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.ProcessingObjectModel, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebDesign, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WinForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </assemblies>
      <buildProviders>
        <!-- Version updated to 15.0.0.0. -->
        <add extension=".rdlc"
          type="Microsoft.Reporting.RdlBuildProvider, Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </buildProviders>
    </compilation>
    <httpRuntime targetFramework="4.6"/>
    <httpHandlers>
      <!-- Version updated to 15.0.0.0 -->
      <add path="Reserved.ReportViewerWebControl.axd" verb="*"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"
        validate="false"/>
    </httpHandlers>
  </system.web>
  <system.webServer>
    <validation validateIntegratedModeConfiguration="false"/>
    <modules runAllManagedModulesForAllRequests="true"/>
    <handlers>
      <!-- Version updated to 15.0.0.0 -->
      <add name="ReportViewerWebControlHandler" verb="*" path="Reserved.ReportViewerWebControl.axd" preCondition="integratedMode"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
    </handlers>
  </system.webServer>
</configuration>
```

### <a name="sample-aspx"></a>サンプル .aspx

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="SampleAspx" %>

<!-- Update version to 15.0.0.0 -->
<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>
```

## <a name="add-the-report-viewer-control-to-a-new-windows-forms-project"></a>新しい Windows フォーム プロジェクトにレポート ビューアー コントロールを追加する

1. 新しい **Windows フォーム アプリケーション**を作成するか、既存のプロジェクトを開きます。

    .NET Framework 4.6 以降のバージョンを使用できます。
    
    ![新しい Windows フォーム アプリケーションの作成のスクリーンショット。](../../reporting-services/application-integration/media/ssrs-create-new-winforms-project-4-6.png)

2. **NuGet パッケージ マネージャー コンソール**から ReportViewer 2016 コントロール NuGet パッケージをインストールします。

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WinForms
    ```
3. コードから新しいコントロールを追加するか、[コントロールをツールボックスに追加](#add-the-control-to-visual-studio-toolbar)します。

    ```csharp
    private Microsoft.Reporting.WinForms.ReportViewer reportViewer1;
    
    private void InitializeComponent()
    {
        this.reportViewer1 = new Microsoft.Reporting.WinForms.ReportViewer();
        this.SuspendLayout();
        // 
        // reportViewer1
        // 
        this.reportViewer1.Location = new System.Drawing.Point(168, 132);
        this.reportViewer1.Name = "reportViewer1";
        this.reportViewer1.ServerReport.BearerToken = null;
        this.reportViewer1.Size = new System.Drawing.Size(396, 246);
        this.reportViewer1.TabIndex = 0;
        // 
        // Form1
        // 
        this.Controls.Add(this.reportViewer1);
    }
    ```

## <a name="how-to-set-100-height-on-the-report-viewer-control"></a>ReportViewer コントロールで 100% の高さを設定する方法

ビューア― コントロールの高さが 100% に設定されている場合、親要素は定義済みの高さであるか、すべての祖先はパーセントによって定義される高さである必要があります。

### <a name="set-the-height-of-all-the-ancestors-to-100"></a>すべての先祖の高さを 100% に設定する

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <style>
        html,body,form,#div1 {
            height: 100%; 
        }
    </style>
   </head>
<body>
    <form id="form1" runat="server">
    <div id="div1" >
            <asp:ScriptManager runat="server"></asp:ScriptManager>
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote" Height="100%" Width="100%">
            <ServerReport ReportServerUrl="https://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>
```

### <a name="set-the-parents-height-attribute"></a>親の height 属性を設定する

ビューポートの割合の長さについては、「[Viewport-percentage lengths](http://www.w3.org/TR/css3-values/#viewport-relative-lengths)」(ビューポートの割合の長さ) を参照してください。

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
</head>
<body>
    <form id="form1" runat="server">
    <div style="height:100vh;">
            <asp:ScriptManager runat="server"></asp:ScriptManager>
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote" Height="100%" Width="100%">
            <ServerReport ReportServerUrl="https://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>
```

## <a name="add-the-control-to-visual-studio-toolbar"></a>Visual Studio ツール バーにコントロールを追加する

Report Viewer コントロールは NuGet パッケージとして出荷されるようになったため、既定では Visual Studio ツールボックスに表示されません。 コントロールをツールボックスに手動で追加できます。

1. 前述のように、WinForms または WebForms 用の NuGet パッケージをインストールします。

2. ツールボックスに表示されている ReportViewer コントロールを削除します。

    ![レポート ビューアー コントロールの削除のスクリーンショット。](../../reporting-services/application-integration/media/ssrs-remove-old-rvcontrol-toolbox.png)

3. ツールボックス内のいずれかの場所を右クリックし、 **[アイテムの追加]** を選択します。

    ![ツールボックスの [アイテムの選択] オプションのスクリーンショット。](../../reporting-services/application-integration/media/ssrs-toolbox-choose-item.png)
    
4. **[.NET Framework コンポーネント]** の **[参照]** を選択します。

    ![[.NET Framework コンポーネント] ダイアログボックスの [参照] ボタンのスクリーンショット。](../../reporting-services/application-integration/media/ssrs-toolbox-browse.png)

5. インストールされた NuGet パッケージから **Microsoft.ReportViewer.WinForms.dll** または **Microsoft.ReportViewer.WebForms.dll** を選択します。

    > [!NOTE] 
    > NuGet パッケージは、プロジェクトのソリューション ディレクトリにインストールされます。 dll のパスは、`{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.Winforms.{version}\lib\net40` または `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.WebForms.{version}\lib\net40` のようになります。

6. ツールボックス内に新しいコントロールが表示されます。 必要に応じて、ツールボックス内の別のタブに移動することができます。

    ![ツールボックスの新しいレポート ビューアー コントロールのスクリーンショット。](../../reporting-services/application-integration/media/ssrs-toolbox-rvcontrol.png)

## <a name="common-issues"></a>一般的な問題
    
ビューアー コントロールは、モダン ブラウザー向けに設計されています。 IE 互換モードを使用してブラウザーにページを表示すると、コントロールが想定どおりに動作しない場合があります。 イントラネット サイトでは、既定のブラウザーの動作をオーバーライドするメタ タグが必要な場合があります。

```html
<meta http-equiv="X-UA-Compatible" content="IE=edge" />
```

## <a name="nugetorg-pages"></a>NuGet.org ページ

レポート ビューアー コントロールの WebForm と WinForm のバージョンに関する NuGet.org サイトの記事のリンクは次のとおりです。

- Microsoft.ReportingServices.ReportViewerControl.WebForms [https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.WebForms/](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.WebForms/)
- Microsoft.ReportingServices.ReportViewerControl.Winforms [https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.WinForms/](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.WinForms/)


## <a name="forum-feedback"></a>フォーラムのフィードバック

問題が発生した場合は、[Reporting Services フォーラム](/answers/topics/sql-server-reporting-services.html) でチームにお知らせください。

## <a name="see-also"></a>関連項目

[Report Viewer コントロールのデータ コレクション](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls-data-collection.md)