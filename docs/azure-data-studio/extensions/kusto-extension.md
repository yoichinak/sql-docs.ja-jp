---
title: Azure Data Studio 用の Kusto (KQL) 拡張機能
description: この記事では、Azure Data Studio を使用して Azure Data Explorer クラスターに接続し、クエリを実行する方法について説明します。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: jukoesma
ms.custom: ''
ms.date: 10/29/2020
ms.openlocfilehash: 0c77b957f14401aec3130fa5fa4f78f0d34de9b5
ms.sourcegitcommit: 894c1a23e922dc29b82c1d2c34c7b0ff28b38654
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93067204"
---
# <a name="kusto-kql-extension-for-azure-data-studio-preview"></a>Azure Data Studio 用の Kusto (KQL) 拡張機能 (プレビュー)

[Azure Data Studio](../what-is-azure-data-studio.md) 用の Kusto (KQL) 拡張機能を使用すると、[Azure Data Explorer](/azure/data-explorer/data-explorer-overview) クラスターに接続してクエリを実行できます。

ユーザーは、KQL クエリを記述して実行したり、IntelliSense を備えた [Kusto カーネル](../notebooks/notebooks-kusto-kernel.md)を使ってたノートブックを作成したりできるようになりました。

Azure Data Studio でネイティブ Kusto (KQL) エクスペリエンスを有効にすることにより、データ エンジニア、データ科学者、およびデータ アナリストは、Azure Data Explorer に格納されている大量のデータに対して傾向や異常をすばやく観察できます。

この拡張機能は、現在プレビューの段階にあります。

## <a name="prerequisites"></a>前提条件

Azure サブスクリプションをお持ちでない場合は、開始する前に[無料の Azure アカウント](https://azure.microsoft.com/free/)を作成してください。

以下の前提条件も必要です。

- [Azure Data Studio をインストールしていること](../download-azure-data-studio.md)。
- [Azure Data Explorer クラスターとデータベース](/azure/data-explorer/create-cluster-database-portal)。

## <a name="install-the-kusto-kql-extension"></a>Kusto (KQL) 拡張機能をインストールする

Azure Data Studio に Kusto (KQL) 拡張機能をインストールするには、次の手順に従います。

1. Azure Data Studio で拡張機能マネージャーを開きます。 拡張機能アイコンを選択するか、[表示] メニューの **[拡張機能]** を選択できます。

2. 検索バーに「 *Kusto* 」と入力します。

3. **Kusto (KQL)** 拡張機能を選択し、その詳細を表示します。

4. **[インストール]** を選択します。

:::image type="content" source="media/kusto-extension/kusto-extension-icon.png" alt-text="Kusto 拡張機能":::

## <a name="how-to-connect-to-an-azure-data-explorer-cluster"></a>Azure Data Explorer クラスターに接続する方法

### <a name="find-your-azure-data-explorer-cluster"></a>対象の Azure Data Explorer クラスターを検索する

[Azure portal](https://ms.portal.azure.com/#home) で対象の Azure Data Explorer クラスターを検索し、そのクラスターの URI を見つけます。

:::image type="content" source="media/kusto-extension/kusto-extension-adx-cluster-uri.png" alt-text="URI":::

一方で、 *help.kusto.windows.net* クラスターを使用してすぐに開始することができます。

この記事では、サンプルとして help.kusto.windows.net クラスターのデータを使用しています。

### <a name="connection-details"></a>接続の詳細情報

接続する Azure Data Explorer クラスターを設定するには、次の手順に従います。

1. **[接続]** ウィンドウで **[新しい接続]** を選択します。

2. **[接続の詳細]** に情報を入力します。
    1. **[接続の種類]** で *[Kusto]* を選択します。
    2. **[クラスター]** に対象の Azure Data Explorer クラスターを入力します。

        > [!Note]
        > クラスター名を入力するときは、`https://` プレフィックスまたは末尾の `/` は含めないでください。

    3. **[認証の種類]** には、既定値の *[Azure Active Directory - Universal with MFA account]\(Active Directory - MFA アカウントで汎用\)* を指定します。
    4. **[アカウント]** にはご自分のアカウント情報を指定します。
    5. **[データベース]** には *[既定値]* を指定します。
    6. **[サーバー グループ]** には *[既定値]* を指定します。
        1. このフィールドを使用すると、特定のグループ内のサーバーを整理できます。
    7. **[名前 (省略可能)]** は空白のままにします。
        1. このフィールドを使用すると、サーバーに別名を付けることができます。

    :::image type="content" source="media/kusto-extension/kusto-extension-connection-details.png" alt-text="接続の詳細情報":::

## <a name="how-to-query-an-azure-data-explorer-database-in-azure-data-studio"></a>Azure Data Studio で Azure Data Explorer データベースに対してクエリを実行する方法

Azure Data Explorer クラスターへの接続を設定したので、Kusto (KQL) を使用してデータベースに対してクエリを実行できます。

新しいクエリ タブを作成するには、 **[ファイル] > [新しいクエリ]** を選択するか、 *Ctrl + N* を使用するか、データベースを右クリックして **[新しいクエリ]** を選択します。

新しいクエリ タブを開いたら、Kusto クエリを入力します。

KQL クエリのサンプルをいくつか次に示します。

```kusto
StormEvents
| limit 1000
```

```kusto
StormEvents
| where EventType == "Waterspout"
```

KQL クエリの記述に関する詳細については、「[Azure データ エクスプローラーのクエリを記述する](/azure/data-explorer/write-queries#overview-of-the-query-language)」を参照してください

## <a name="view-extension-settings"></a>拡張機能の設定を表示する

Kusto 拡張機能の設定を変更するには、次の手順に従います。

1. Azure Data Studio で拡張機能マネージャーを開きます。 拡張機能アイコンを選択するか、[表示] メニューの **[拡張機能]** を選択できます。

2. **Kusto (KQL)** 拡張機能を検索します。

3. **[管理]** アイコンを選択します。

4. **[拡張機能の設定]** アイコンを選択します。

拡張機能の設定は次のようになります。

:::image type="content" source="media/kusto-extension/kusto-extension-settings.png" alt-text="Kusto (KQL) 拡張機能の設定":::

## <a name="sanddance-visualization"></a>SandDance 視覚化

Azure Data Studio で [SandDance 拡張機能](sanddance-extension.md)を Kusto (KQL) とともに使用すると、リッチな対話型の視覚化も実現できます。 KQL クエリの結果セットから **[ビジュアライザー]** ボタンを選択して [SandDance](https://sanddance.js.org/) を起動します。

:::image type="content" source="media/kusto-extension/kusto-extension-sanddance-demo.gif" alt-text="SandDance 視覚化":::

## <a name="known-issues"></a>既知の問題

| 詳細 | 回避策 |
|---------|------------|
| [Kusto ノートブックにおいて、保存された別名接続でデータベース接続を変更すると、コード セルの実行時エラー後にスタックする](https://github.com/microsoft/azuredatastudio/issues/12384) | ノートブックを閉じて再度開き、そのデータベースを含む適切なクラスターに接続します |
| [Kusto ノートブックにおいて、未保存の別名接続でのデータベース接続の変更が機能しない](https://github.com/microsoft/azuredatastudio/issues/12843) |接続ビューレットから新しい接続を作成し、それを別名で保存します。 次に、新しいノートブックを作成し、新しく保存した接続に接続します | 
| [Kusto ノートブックにおいて、新しい ADX 接続を作成するときにデータベースのドロップダウンが設定されない](https://github.com/microsoft/azuredatastudio/issues/12666) | 接続ビューレットから新しい接続を作成し、それを別名で保存します。 次に、新しいノートブックを作成し、新しく保存した接続に接続します |

製品チームにフィードバックを提供するために、[機能の要求](https://github.com/microsoft/azuredatastudio/issues/new?assignees=&labels=&template=feature_request.md&title=)を提出できます。  
製品チームにフィードバックを提供するために、[バグ](https://github.com/microsoft/azuredatastudio/issues/new?assignees=&labels=&template=bug_report.md&title=)を提出できます。

## <a name="next-steps"></a>次のステップ

- [Kusto ノートブックの作成と実行](../notebooks/notebooks-kusto-kernel.md)
- [Azure Data Studio の Kqlmagic ノートブック](../notebooks/notebooks-kqlmagic.md)
- [SQL から Kusto のチート シート](/azure/data-explorer/kusto/query/sqlcheatsheet)
- [Azure Data Explorerとは](/azure/data-explorer/data-explorer-overview)
- [SandDance 視覚化の使用](https://sanddance.js.org/)
