---
title: 以前のリリースの SQL Server Data Tools (SSDT)
description: どのバージョンの SSDT および SSDT-BI が、どのバージョンの Visual Studio で動作するかを確認します。 さまざまなバージョンの SSDT と SSDT-BI をインストールする方法を参照してください。
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 5d32e301-0f44-4916-b0db-76e8322c0ab7
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan
ms.custom: seo-lt-2019
ms.date: 06/17/2020
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 5c88e83bcc0b4722bf52da697bdaa03af37b972d
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988588"
---
# <a name="previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi"></a>以前のリリースの SQL Server Data Tools (SSDT と SSDT-BI)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

SQL Server Data Tools (SSDT) には、SQL Server のコンテンツ タイプ (リレーショナル データベース、Analysis Services モデル、Reporting Services レポート、および Integration Services パッケージ) を構築するためのプロジェクト テンプレートとデザイン サーフェイスが収録されています。

SSDT には後方互換性があるため、[最新の SSDT](download-sql-server-data-tools-ssdt.md) でも古いバージョンの SQL Server を実行するデータベース、モデル、レポート、パッケージの設計と配置を行うことができます。

SQL Server のコンテンツ タイプの作成に使用される Visual Studio シェルは、これまでにさまざまな名前でリリースされてきました。たとえば、 **SQL Server Data Tools**、 **SQL Server Data Tools - Business Intelligence**、 **Business Intelligence Development Studio**です。 以前のバージョンに付属しているプロジェクト テンプレート セットの内容は、バージョンごとに異なります。 すべてのプロジェクト テンプレートを 1 つの SSDT でまとめて入手するには、 [最新バージョン](download-sql-server-data-tools-ssdt.md)が必要です。 それがない場合は、以前のバージョンをいくつもインストールしなければ、SQL Server で使われるテンプレートのすべてをそろえることはできません。 インストールされるシェルは、Visual Studio のバージョンごとに 1 つだけです。別のバージョンの SSDT をインストールすると、不足しているテンプレートだけが追加されます。

## <a name="previous-ssdt-releases"></a>以前の SSDT リリース

以前のバージョンの SSDT をダウンロードするには、関連セクションでダウンロード リンクを選択します。

| SSDT のバージョン | Visual Studio のバージョン |
|--------------|-----------------------|
| [15.8](#ssdt-for-visual-studio-vs-2017) | 2017 |
| [17.4](#ssdt-for-visual-studio-vs-2015) | 2015 |
| [16.5](#ssdt-for-visual-studio-vs-2013) | 2013 |
| [11.1.50727.1](#ssdt-for-visual-studio-vs-2012) | 2012 |

### <a name="ssdt-for-visual-studio-vs-2017"></a>SSDT for Visual Studio (VS) 2017

**[SSDT for Visual Studio 2017 (15.8) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2124319)**

**SSDT for Visual Studio 2017** の今回のリリースは、次の言語でインストールできます。

[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x40a)

### <a name="ssdt-for-visual-studio-vs-2015"></a>SSDT for Visual Studio (VS) 2015

このバージョンの SSDT をインストールするには、ISO イメージをダウンロードする必要があります。 この ISO ファイルは、SSDT に必要なすべてのコンポーネントが含まれた自己完結型ファイルであり、再開可能なダウンロード マネージャーを使用してダウンロードできます (ネットワークの帯域幅が限られている場合や信頼性が低い場合に便利です)。 ダウンロードが完了したら、ISO はドライブとしてマウントすることができます。

インストールする手順:

1. **[SSDT for Visual Studio 2015 (17.4) をダウンロードします](https://go.microsoft.com/fwlink/?linkid=2132817)** 。

2. ISO イメージを開きます。

3. *SSDTSetup.exe* ファイルを実行します。

    ![ISO イメージ](media/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi/iso-image.png)

**SSDT for Visual Studio 2015** の今回のリリースは、次の言語でインストールできます。

| Language | SHA256 ハッシュ |
|----------|-------------|
| [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x804) | 79A958B122DDEC2857F1F4B9F0272A6BD2106BB17B4DA94CC68CACFCDDC16EAE |
| [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x404) | 8F9661883F2D2D28D6928AE66242DB465DBB25696EDFE0348D222421CEAB000A |
| [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x409) | 7727BA227A9E49C2DFCC1E9F2A10924CC472E3425653DC7DE8E4B830712B302E |
| [フランス語](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x40c) | 2DF6655819F604E8D20A396CA9FDFEE279C5A9E50776FFC143A5BA4C3E2F1849 |
| [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x407) | 5C44502DEE8B31675D0B10B4CE8CA6F5D96A2692CC498B9859A77C24F30EF870 |
| [イタリア語](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x410) | 6A616F6E3A1C7DD52457FB8C8692E5C1C551032FF46AD8C5112CF9364F17C631 |
| [日本語](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x411) | 1244A5EADF673E4BD36E9967A2008F65CA2A1D40E8E7DD4D17640A6FC1EACA9A |
| [韓国語](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x412) | 6E0E057A853F54AB87F3F8984954F590FCCD3BE2EC2139F02EFA085FEA6D3E61 |
| [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x416) | 24122C092464B299F41A7644814F375F0CC2786877BCAE0282221FF8D73BD100 |
| [ロシア語](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x419) | 2CDE208C241C3F13D2EC37294C10503C7A9D1222ED33F6FE54849169F30BE697 |
| [スペイン語](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x40a) | BD12844E6F0A0ECFD5815D01EDFB8018CE9B4A1044DE8DF96AC740D85E800FD6 |

### <a name="ssdt-for-visual-studio-vs-2013"></a>SSDT for Visual Studio (VS) 2013

このバージョンの SSDT をインストールするには、ISO イメージをダウンロードする必要があります。 この ISO ファイルは、SSDT に必要なすべてのコンポーネントが含まれた自己完結型ファイルであり、再開可能なダウンロード マネージャーを使用してダウンロードできます (ネットワークの帯域幅が限られている場合や信頼性が低い場合に便利です)。 ダウンロードが完了したら、ISO はドライブとしてマウントすることができます。

インストールする手順:

1. **[SSDT for Visual Studio 2013 (16.5) をインストールします](https://go.microsoft.com/fwlink/?linkid=832312)**

2. ISO イメージを開きます。

3. *SSDTSetup.exe* ファイルを実行します。

    ![ISO イメージ](media/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi/iso-image.png)

**SSDT for Visual Studio 2013** の今回のリリースは、次の言語でインストールできます。

| Language | SHA256 ハッシュ |
|----------|-------------|
| [簡体中国語](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x804) | 79A958B122DDEC2857F1F4B9F0272A6BD2106BB17B4DA94CC68CACFCDDC16EAE |
| [繁体中国語](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x404) | 8F9661883F2D2D28D6928AE66242DB465DBB25696EDFE0348D222421CEAB000A |
| [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x409) | 7727BA227A9E49C2DFCC1E9F2A10924CC472E3425653DC7DE8E4B830712B302E |
| [フランス語](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x40c) | 2DF6655819F604E8D20A396CA9FDFEE279C5A9E50776FFC143A5BA4C3E2F1849 |
| [ドイツ語](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x407) | 5C44502DEE8B31675D0B10B4CE8CA6F5D96A2692CC498B9859A77C24F30EF870 |
| [イタリア語](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x410) | 6A616F6E3A1C7DD52457FB8C8692E5C1C551032FF46AD8C5112CF9364F17C631 |
| [日本語](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x411) | 1244A5EADF673E4BD36E9967A2008F65CA2A1D40E8E7DD4D17640A6FC1EACA9A |
| [韓国語](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x412) | 6E0E057A853F54AB87F3F8984954F590FCCD3BE2EC2139F02EFA085FEA6D3E61 |
| [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x416) | 24122C092464B299F41A7644814F375F0CC2786877BCAE0282221FF8D73BD100 |
| [ロシア語](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x419) | 2CDE208C241C3F13D2EC37294C10503C7A9D1222ED33F6FE54849169F30BE697 |
| [スペイン語](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x40a) | BD12844E6F0A0ECFD5815D01EDFB8018CE9B4A1044DE8DF96AC740D85E800FD6 |

### <a name="ssdt-for-visual-studio-vs-2012"></a>SSDT for Visual Studio (VS) 2012

このバージョンの SSDT をインストールするには、ISO イメージをダウンロードする必要があります。 この ISO ファイルは、SSDT に必要なすべてのコンポーネントが含まれた自己完結型ファイルであり、再開可能なダウンロード マネージャーを使用してダウンロードできます (ネットワークの帯域幅が限られている場合や信頼性が低い場合に便利です)。 ダウンロードが完了したら、ISO はドライブとしてマウントすることができます。

インストールする手順:

1. **[SSDT for Visual Studio 2012 (11.1.50727.1) をダウンロードします](https://go.microsoft.com/fwlink/?linkid=518814)**

2. ISO イメージを開きます。

3. *SSDTSetup.exe* ファイルを実行します。

    ![ISO イメージ](media/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi/iso-image.png)

**SSDT for Visual Studio 2012** の今回のリリースは、次の言語でインストールできます。

| Language | SHA256 ハッシュ |
|----------|-------------|
| [簡体中国語](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x804) | 78F20325648CFF49D9C58A26186E0AC199D104B3CF634E5663B4B262BEC69C07 |
| [繁体中国語](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x404) | A2722380AF2EE1E8BB52B4FA54A61BAB411E5E5FD5B050108F81ED23DC87366D |
| [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x409) | 748EF78D3F9CC6FE360432C378EA690DE51AEB2C747E87D43E08448D26F93A91 |
| [フランス語](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x40c) | 40E6504169BF618EDC7EB5B62D1215DC96726D6EEC3CA8EC3EEB49044E4B6FB7 |
| [ドイツ語](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x407) | C45C974E6B8F9611BA2AC1EE90C5C507992BCE5693BF46F6C7C138591ED6A123 |
| [イタリア語](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x410) | C1B20CDB41C7B1B5DE76A71F9A091A6FDF5186B12F6AA269DA6338B3CB2D91A6 |
| [日本語](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x411) | BF56958B904C1C5F28084BD0B16928B6CBFEC83EB3F0C913EC364FA335241943 |
| [韓国語](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x412) | 9023B0656785C357A67E39EB76A2806B923C2BD17342D7226A8ADA384A9F4E28 |
| [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x416) | ACAD9FE03729E289ECE821D92C56CFB1D7FCCEA8423ABF1E164BF3C67ABEFEFB |
| [ロシア語](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x419) | E2191D787BA833DF4A85B064C5373DC44099E76214FBF9505728702D4D6B83F0 |
| [スペイン語](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x40a) | 6D81FB572A7003C54C29D2ACF076D2CED4A1CA80F329BFF9D41A806920D64EEE |

> [!Note]
> SSDT では、Visual Studio の 2 つの最新バージョンがサポートされています。 Visual Studio 2019 のリリースでは、Visual Studio 2015 およびそれ以前に対する SSDT バージョンが更新されなくなりました。 SSDT for Visual Studio 2010 は使用できなくなりました。 詳細については、[この SSDT チームのブログ投稿](/archive/blogs/ssdt/sql-server-data-tools-17-0-rc-and-ssdt-in-vs2017)で *FAQ* のセクションをご覧ください。

## <a name="sql-bi-analysis-services-reporting-services-integration-services"></a>SQL BI: Analysis Services、Reporting Services、Integration Services

BI のテンプレートは、SSAS モデル、SSRS レポート、SSIS パッケージの作成に使用されます。 BI デザイナーの各バージョンは、特定のリリースの SQL Server に対応しています。 BI の新しい機能を使うには、新しいバージョンの BI デザイナーをインストールしてください。

## <a name="bi-designers"></a>BI デザイナー

[SSDT-BI for Visual Studio 2013 のダウンロード](https://www.microsoft.com/download/details.aspx?id=42313) (SQL Server 2014、SQL Server 2012、SQL Server 2008、および 2008 R2)

[SSDT-BI for Visual Studio 2012 のダウンロード](https://www.microsoft.com/download/details.aspx?id=36843) (SQL Server 2014、SQL Server 2012、SQL Server 2008、および 2008 R2)

Business Intelligence Development Studio (BIDS) は SQL Server のセットアップを通じてインストールされます。 Web ダウンロードはありません (SQL Server 2008 および 2008 R2)。

SQL Server 2012 または 2014 の場合は、 **Visual Studio 2012 用 SSDT-BI** と **SSDT-BI と Visual Studio 2013**です。 この 2 つの違いは、Visual Studio のバージョンだけです。

## <a name="next-steps"></a>次のステップ

- [SQL Server Data Tools (SSDT) のダウンロード](../ssdt/download-sql-server-data-tools-ssdt.md)
- [SQL Server Data Tools (SSDT) リリース ノート](release-notes-ssdt.md)
- [SQL Server Management Studio (SSMS) のダウンロード](../ssms/download-sql-server-management-studio-ssms.md)
- [Azure Data Studio のダウンロード](../azure-data-studio/download-azure-data-studio.md)
- [SQL ツールとユーティリティ](../tools/overview-sql-tools.md)