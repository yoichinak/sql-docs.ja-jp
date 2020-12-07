---
description: Microsoft Connector for Teradata
title: Microsoft Connector for Teradata | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a866d7d1083435acffeb157edf9fe4a0bb725d3e
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88425764"
---
# <a name="microsoft-connector-for-teradata"></a>Microsoft Connector for Teradata

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

Microsoft Connector for Teradata を使用すると、SSIS パッケージ内の Teradata データベースとの間でデータをエクスポートしたり、データを読み込んだりできます。

この新しいコネクタでは、1MB 対応のテーブルを持つデータベースがサポートされます。

## <a name="version-support"></a>バージョンのサポート

Microsoft Connector for Teradata では、次の Microsoft SQL Server 製品がサポートされています。

- Microsoft SQL Server 2019
- Visual Studio 2017 用 Microsoft SQL Server Data Tools (SSDT) 15.8.1 以降
- Visual Studio 2019 用 Microsoft SQL Server Data Tools (SSDT)

Microsoft Connector for Teradata では、Teradata Parallel Transporter Application Programming Language Interface を利用し、Teradata データベースとの間でデータを読み込んだり、エクスポートしたりします。 次のバージョンがサポートされています。

- Teradata Parallel Transporter (Teradata PT) 16.10
- Teradata Parallel Transporter (Teradata PT) 16.20

次の Teradata データベース バージョンのデータ ソースがサポートされています。

- Teradata Database 16.20
- Teradata Database 16.10
- Teradata Database 15.10
- Teradata Database 15.00

Teradata Parallel Transporter Application プログラミング インターフェイス プログラマー ガイドの詳細については、[Teradata ドキュメント](https://docs.teradata.com/)を確認してください。

## <a name="installation"></a>インストール

32 ビット コンピューターの場合、[Teradata Tools and Utilities - Windows Installation Package](https://downloads.teradata.com/download/tools/teradata-tools-and-utilities-windows-installation-package) から次のドライバーをインストールします。

- Teradata ODBC ドライバー (32 ビット)
- Teradata PT API (32 ビット)

64 ビットコンピューターの場合、次のドライバーをインストールします。

- Teradata ODBC ドライバー (64 ビット)
- Teradata PT API (64 ビット)

Teradata データベースのコネクタをインストールするには、[Microsoft Connector for Teradata](https://www.microsoft.com/download/details.aspx?id=100599) の最新版からインストーラーをダウンロードし、実行します。 そのうえでインストール ウィザードの指示に従います。

コネクタをインストールしたら、SQL Server 統合サービスを再起動して、Teradata のソースと変換先が正常に機能することを確認する必要があります。

## <a name="design-and-execute-ssis-packages"></a>SSIS パッケージのデザインと実行

Microsoft Connector for Teradata は、Attunity Teradata Connector と同様のユーザー エクスペリエンスを提供します。 ユーザーは、SSDT for VS 2017 または VS 2019 を使用して *SQL Server 2019 をターゲット* にすることで、以前のエクスペリエンスに基づいて新しいパッケージをデザインできます。

Teradata のソースと変換先は、[共通] カテゴリにあります。

![Teradata コンポーネント](media/teradata-component.png)

Teradata 接続マネージャーは、"TERADATA" として表示されます。

![Teradata 接続マネージャーの種類](media/teradata-connection-manager-type.png)

Attunity Teradata Connector を使用してデザインされた既存の SSIS パッケージは、Microsoft Connector for Teradata を使用するように自動的にアップグレードされます。 アイコンも変更されます。

*SQL Server 2017 以前をターゲットとする* SSIS パッケージを実行するには、以下のリンクから対応するバージョンの **Microsoft Connector for Teradata by Attunity** をインストールする必要があります。

- [SQL Server 2017:Microsoft Connector Version 5.0 for Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=55179)
- [SQL Server 2016:Microsoft Connector Version 4.0 for Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=52950)
- [SQL Server 2014:Microsoft Connector Version 3.0 for Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=44582)
- [SQL Server 2012:Microsoft Connector Version 2.0 for Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=29283)

SSDT で *SQL Server 2017 以前をターゲットとする* SSIS パッケージをデザインするには、**Microsoft Connector for Teradata** があり、対応するバージョンの **Microsoft Connector for Teradata by Attunity** をインストールする必要があります。

## <a name="limitations-and-known-issues"></a>制限事項と既知の問題

- Teradata ソース/変換先エディター、 **[既定のデータベース]** プロパティは有効になりません。  回避策として、テーブルまたはビューをフィルター処理するためのドロップダウン ボックスにデータベース名を入力します。

- Teradata ソース/変換先エディター、\<database>.<table/view> と入力した場合、マッピング手順が機能しません。 回避策として、\<database>.<table/view> と入力してからドロップダウン ボタンをクリックします。

- Teradata ソースエディター、データ アクセス モードが "テーブル名 – TPT Export" の場合、ビューを表示できません。 回避策として、Teradata ソースの詳細エディターを使用します。

- Teradata 変換先、属性 'PackMaximum' を 'True' に設定できません。  それ以外の場合、エラーが発生します。

## <a name="uninstallation"></a>アンインストール

アンインストール ウィザードを実行し、**Microsoft Connector for Teradata** を削除できます。

## <a name="next-steps"></a>次のステップ

- [Teradata 接続マネージャー](teradata-connection-manager.md)を構成する
- [Teradata ソース](teradata-source.md)を構成する
- [Teradata 変換先](teradata-destination.md)を構成する
- ご質問がある場合は、[技術者コミュニティ](https://aka.ms/AA6iwdw)を参照してください。
