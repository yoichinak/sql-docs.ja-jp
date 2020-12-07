---
description: Microsoft Connector for Oracle
title: Microsoft Connector for Oracle | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a5bb5631a398e398b45b84a0ee70b51f49c90988
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88430754"
---
# <a name="microsoft-connector-for-oracle"></a>Microsoft Connector for Oracle

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

Microsoft Connector for Oracle を使用すると、SSIS パッケージ内の Oracle データソースで、データのエクスポートとデータの読み込みを実行できるようになります。

## <a name="version-support"></a>バージョンのサポート

Microsoft Connector for Oracle では、次の Microsoft SQL Server 製品がサポートされています。

- SQL Server 2019 CU1 以降
- Visual Studio 2017 用 SQL Server Data Tools (SSDT) 15.9.3 以降
- Visual Studio 2019 用 Microsoft SQL Server Data Tools (SSDT)

次の Oracle データベース バージョンのデータ ソースがサポートされています。

- Oracle 10.x
- Oracle 11.x
- Oracle 12c
- Oracle 18c (Windows 認証のサポートなし)
- Oracle 19c (Windows 認証のサポートなし)

Oracle データベースは、すべてのオペレーティング システムとプラットフォームでサポートされています。
> [!NOTE]
>
> SQL Server 2019 では、Microsoft Connector for Oracle Database 用の Oracle クライアントは必要ありません。

## <a name="installation"></a>インストール

Oracle データベースのコネクタをインストールするには、[Microsoft Connector for Oracle](https://www.microsoft.com/download/details.aspx?id=58228) の最新版からインストーラーをダウンロードし、実行します。 そのうえでインストール ウィザードの指示に従います。

コネクタをインストールしたら、SQL Server 統合サービスを再起動して、Oracle のソースと変換先が正常に機能することを確認する必要があります。

SQL Server 2017 以前をターゲットとする SSIS パッケージを実行するには、**Microsoft Connector for Oracle** に加え、以下のリンクから **Oracle クライアント**と対応するバージョンの **Microsoft Connector for Oracle by Attunity** をインストールする必要があります。

- [SQL Server 2017:Microsoft Connector Version 5.0 for Oracle by Attunity](https://www.microsoft.com/download/details.aspx?id=55179)
- [SQL Server 2016:Microsoft Connector Version 4.0 for Oracle by Attunity](https://www.microsoft.com/download/details.aspx?id=52950)
- [SQL Server 2014:Microsoft Connector Version 3.0 for Oracle by Attunity](https://www.microsoft.com/download/details.aspx?id=44582)
- [SQL Server 2012:Microsoft Connector Version 2.0 for Oracle by Attunity](https://www.microsoft.com/download/details.aspx?id=29283)

## <a name="limitations-and-known-issues"></a>制限事項と既知の問題

- ビューは、Oracle ソースの "*テーブルまたはビューの名前*" の一覧には表示されません。 回避するには、SQL コマンドを使用して select * from view を実行するか、詳細エディターでプロパティ [Oracle Source].[TableName] にビューの名前を設定します。

## <a name="uninstallation"></a>アンインストール

アンインストール ウィザードを実行して、SQL Server から Microsoft Connector for Oracle Database を削除できます。

## <a name="next-steps"></a>次のステップ

- [Oracle 接続マネージャー](oracle-connection-manager.md)を構成する。
- [Oracle ソース](oracle-source.md)を構成する。
- [Oracle 変換先](oracle-destination.md)を構成する。
- ご質問がある場合は、[技術者コミュニティ](https://aka.ms/AA5u35j)を参照してください。
