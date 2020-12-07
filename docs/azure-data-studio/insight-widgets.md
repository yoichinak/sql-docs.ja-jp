---
title: 分析情報ウィジェットを使用してサーバーとデータベースを監視する
description: Azure Data Studio の分析情報ウィジェットを使用し、サーバーやデータベースを監視するクエリを視覚化し、分析情報を得る方法について説明します。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, sstein
ms.custom: seodec18, sqlfreshmay19, seo-lt-2019
ms.date: 05/14/2019
ms.openlocfilehash: c93cd3ea16b87a23dac96c1f21f3720d169e8c19
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364015"
---
# <a name="manage-servers-and-databases-with-insight-widgets-in-azure-data-studio"></a>Azure Data Studio の分析情報ウィジェットを使用してサーバーとデータベースを管理する

分析情報ウィジェットでは、お客様がサーバーとデータベースを監視するために使用している Transact-SQL (T-SQL) クエリが取得され、それらが洞察に富んだ視覚エフェクトに変換されます。

分析情報とは、サーバーとデータベースの監視ダッシュボードに追加するカスタマイズ可能なチャートとグラフです。 ご利用のサーバーとデータベースに関するひとめでわかる分析情報を表示し、次に詳細にドリルダウンして、定義した管理アクションを開始します。

次の例のように、サーバーおよびデータベース用の素晴らしい管理ダッシュボードを作成することができます。

![データベース ダッシュボード](media/insight-widgets/database-dashboard.png)

さまざまな種類の分析情報ウィジェットの作成を開始するには、次のチュートリアルをご覧ください。

- [カスタム分析情報ウィジェットのビルド](tutorial-build-custom-insight-sql-server.md)
- *組み込みの分析情報ウィジェットを有効にする*
  - [パフォーマンス監視の分析情報を有効にする](tutorial-qds-sql-server.md)
  - [テーブル領域の使用状況に関する分析情報を有効にする](tutorial-table-space-sql-server.md)

## <a name="sql-queries"></a>SQL クエリ

Azure Data Studio では、別の言語や高負荷のユーザー インターフェイスのさらなる導入を避けるようにしているため、可能な限り最小の JSON 構成で T-SQL を使用することが試みられます。 T-SQL を使用して分析情報ウィジェットを構成すると、洞察に富んだウィジェットに変換できる有用な T-SQL クエリの既存のソースが無数に活用されます。

分析情報ウィジェットは、次に示す 1 つまたは 2 つの T-SQL クエリで構成されます。
* *分析情報ウィジェット クエリ*はウィジェットに表示されるデータを返すクエリであり、これは必須となります。
* *分析情報の詳細のクエリ*は、分析情報の詳細ページを作成する場合にのみ必要です。

分析情報ウィジェット クエリでは、カウント、チャート、またはグラフをレンダリングするデータセットが定義されます。 分析情報の詳細のクエリは、関連する分析情報の詳細情報を分析情報の詳細パネルに表形式で一覧表示するために使用されます。 

Azure Data Studio では、分析情報ウィジェット クエリが実行され、クエリ結果セットがチャートのデータセットにマップされてから、そのレンダリングが行われます。 ユーザーが分析情報の詳細を開くと、分析情報の詳細のクエリが実行され、ダイアログ内のグリッド ビューに結果が出力されます。

基本的な考え方は、T-SQL クエリをカウント、チャート、グラフ ウィジェットのデータセットとして使用できるように、T-SQL クエリを記述することです。 

## <a name="summary"></a>まとめ

T-SQL クエリとその結果セットにより、分析情報ウィジェットの動作が決まります。 グラフの種類に対するクエリを作成すること、または既存のクエリに対して適切なグラフの種類をマップすることは、効果的な分析情報ウィジェットを構築する上で重要な考慮事項です。



## <a name="additional-resources"></a>その他のリソース
- [クエリ エディター](tutorial-sql-editor.md)

