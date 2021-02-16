---
title: PolyBase とは | Microsoft Docs
description: PolyBase を使用すると、Hadoop や Azure Blob Storage など、外部データ ソースからデータを読み取る Transact-SQL クエリを SQL Server インスタンスで処理できるようになります。
ms.date: 12/14/2019
ms.prod: sql
ms.technology: polybase
ms.topic: overview
f1_keywords:
- PolyBase
- PolyBase, guide
helpviewer_keywords:
- PolyBase
- PolyBase, overview
- Hadoop import
- Hadoop export
- Hadoop export, PolyBase overview
- Hadoop import, PolyBase overview
ms.custom: contperf-fy21q2
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||>=aps-pdw-2016||=azure-sqldw-latest'
ms.openlocfilehash: e4f0bfbac2fe4e49261f9940a97fd73e05676661
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100062227"
---
# <a name="what-is-polybase"></a>PolyBase とは

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]

PolyBase を使用すると、外部データ ソースからデータを読み取る Transact-SQL クエリを SQL Server インスタンスで処理できるようになります。 同じクエリで SQL Server のインスタンスに含まれるリレーショナル テーブルにアクセスすることもできます。 また、PolyBase を使用すると、同じクエリで外部ソースと SQL Server のデータを結合させることもできます。

PolyBase を使用するには SQL Server のインスタンスで次のようにします。

1. [Windows への PolyBase のインストール](polybase-installation.md)
1. [外部データ ソース](../../t-sql/statements/create-external-data-source-transact-sql.md)を作成する
1. [外部テーブル](../../t-sql/statements/create-external-table-transact-sql.md)を作成する

これらの組み合わせることで、外部データソースに接続できるようになります。

SQL Server 2016 では、Hadoop および Azure Blob Storage への接続をサポートする PolyBase が導入されました。

SQL Server 2019 では、SQL Server、Oracle、Teradata、MongoDB などの追加のコネクタが導入されました。

![PolyBase 論理](../../relational-databases/polybase/media/polybase-logical.png "PolyBase 論理")

PolyBase により、クエリ全体を最適化するために計算の一部が外部ソースにプッシュされます。 PolyBase の外部アクセスは Hadoop だけではありません。 その他の構造化されていない非リレーショナル テーブルもサポートしています (区切られたテキスト ファイルなど)。

外部コネクタの例を次に示します。

- [SQL Server](polybase-configure-sql-server.md)
- [Oracle](polybase-configure-oracle.md)
- [Teradata](polybase-configure-teradata.md)
- [MongoDB](polybase-configure-mongodb.md)

### <a name="supported-sql-products-and-services"></a>サポートされる SQL 製品とサービス

PolyBase では、次の Microsoft の SQL 製品にこれらと同じ機能を提供します。

- SQL Server 2016 以降のバージョン (Windows のみ)
- Analytics Platform System (旧称 Parallel Data Warehouse)
- Azure Synapse Analytics

### <a name="azure-integration"></a>Azure との統合

下層 の PolyBase のサポートにより、T-SQL クエリでは Azure Blob Storage のデータをインポートおよびエクスポートすることもできます。 さらに、PolyBase によって、Azure Synapse Analytics で Azure Data Lake Store および Azure Blob Storage のデータをインポートおよびエクスポートできるようになります。

## <a name="why-use-polybase"></a>PolyBase を使用する理由

PolyBase を使用すると、SQL Server インスタンスのデータを外部データと結合できます。 PolyBase によってデータが外部データ ソースに結合される前に、次のいずれかを実行できます。

- すべてのデータが 1 つの場所に配置されるように、データの半分を転送します。
- 両方のデータのソースに対してクエリを実行した後、クライアント レベルでデータを結合および統合するためにカスタムのクエリ ロジックを記述する。

PolyBase を使用すると、Transact-SQL を使用してデータを結合するだけで済みます。

PolyBase を使用するうえで Hadoop 環境に追加のソフトウェアをインストールする必要はありません。 外部データを照会するには、データベース テーブルの照会に使用したのと同じ T-SQL 構文を使用します。 PolyBase が実装する補助的なアクションは、すべて透過的に実行されます。 クエリの作成者には、外部ソースに関する知識が必要ありません。

### <a name="polybase-uses"></a>PolyBase の使用

PolyBase を使用すると、SQL Server で次のシナリオに対応できます。

- **SQL Server インスタンスまたは PDW から Hadoop に格納されているデータのクエリを実行します。** ユーザーは、たとえば Hadoop など、コスト効果の高いスケーラブルな分散システムにデータを格納しています。 PolyBase を使用すると、T-SQL で簡単にデータを照会できます。

- **Azure Blob Storage に格納されたデータのクエリを実行する。** Azure BLOB ストレージは、Azure サービスによって使用されるデータを格納するのに便利な場所です。  PolyBase を使用すると、T-SQL で簡単にデータにアクセスできます。

- **Hadoop、Azure Blob Storage、Azure Data Lake Store からデータをインポートする。** Hadoop、Azure Blob Storage、または Azure Data Lake Store からリレーショナル テーブルにデータをインポートすることで、Microsoft SQL の高速な列ストア テクノロジおよび分析機能を活用できます。 ETL ツールやインポート ツールを個別に用意する必要はありません。

- **Hadoop、Azure BLOB ストレージ、Azure Data Lake Store にデータをエクスポートする。** データを Hadoop、Azure BLOB ストレージ、Azure Data Lake Store にアーカイブすることで、コスト効果の高いストレージを実現し、アクセスしやすいようにそのストレージをオンライン状態にしておくことができます。

- **BI ツールと統合する。** PolyBase を Microsoft のビジネス インテリジェンスや分析スタックと一緒に使用したり、SQL Server と互換性のあるサード パーティ ツールを使用したりすることができます。

## <a name="performance"></a>パフォーマンス

- **Hadoop に計算をプッシュする。** クエリ オプティマイザーでは、クエリのパフォーマンスが向上する場合は Hadoop への計算のプッシュを行うためのコスト ベースの決定が行われます。  クエリ オプティマイザーでは、コスト ベースの決定に外部テーブルの統計が使用されます。 計算のプッシュでは、MapReduce ジョブが作成され、Hadoop の分散コンピューティング リソースが活用されます。

- **コンピューティング リソースをスケーリングする。** クエリのパフォーマンスを向上させるために、SQL Server [PolyBase スケールアウト グループ](../../relational-databases/polybase/polybase-scale-out-groups.md)を使用できます。 これにより、SQL Server インスタンスと Hadoop ノードの間の並列データ転送が可能になります。また、外部データに対する操作のためのコンピューティング リソースが追加されます。

## <a name="next-steps"></a>次のステップ

PolyBase を使用する前に [PolyBase 機能をインストールする](polybase-installation.md)必要があります。 その後、使用するデータ ソースに応じて、次の構成ガイドを参照してください。

- [Hadoop](polybase-configure-hadoop.md)
- [Azure Blob Storage](polybase-configure-azure-blob-storage.md)
- [SQL Server](polybase-configure-sql-server.md)
- [Oracle](polybase-configure-oracle.md)
- [Teradata](polybase-configure-teradata.md)
- [MongoDB](polybase-configure-mongodb.md)
- [ODBC ジェネリック型](polybase-configure-odbc-generic.md)