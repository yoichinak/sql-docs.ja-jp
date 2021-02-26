---
title: SQL Server ビッグ データ クラスターの構成の概要
titleSuffix: SQL Server big data clusters
description: ビッグ データ クラスターの構成の概要
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: rahul.ajmera
ms.date: 02/11/2021
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8cda6e61e8f5f13f5fd414879f888c7ed72a1bd0
ms.sourcegitcommit: 8dc7e0ececf15f3438c05ef2c9daccaac1bbff78
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/13/2021
ms.locfileid: "100343987"
---
# <a name="configure-a-sql-server-big-data-cluster"></a>SQL Server ビッグ データ クラスターを構成する

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]
構成管理を使用すると、管理者は、ワークロードのニーズに合わせて、ビッグ データ クラスターを常に準備できます。 この機能を使用すると、クラスター管理者は、配置時または配置後にビッグ データ クラスターのさまざまな部分を変更または調整し、BDC で実行されている構成をより深く把握できます。 

管理者は、構成管理を使用して、SQL Agent を有効にしたり、組織の Spark ジョブのベースライン リソースを定義したり、各スコープで構成可能な設定を確認したりすることができます。 配置時には `bdc.json` 配置ファイルで、配置後には azdata CLI を使用して、構成を行うことができます。

## <a name="configuration-scopes"></a>構成スコープ
ビッグ データ クラスターの構成には、`cluster`、`service`、`resource` という 3 つのスコープ レベルがあります。 設定の階層も、この順序に従って、上位から下位に適用されます。 BDC コンポーネントでは、最下位のスコープで定義された設定の値が使用されます。 特定のスコープで設定が定義されていない場合は、上位の親スコープから値が継承されます。

たとえば、記憶域プールと `Sparkhead` リソースで Spark ドライバーによって利用されるコアの既定数を定義することがあります。 既定のコア数を定義するには、次のいずれかの操作を行うことができます。

- `Spark` サービス スコープで既定のコア値を指定する

- `storage-0` と `sparkhead` リソース スコープで既定のコア値を指定する

最初のシナリオでは、Spark サービス (記憶域プールと `Sparkhead`) のすべての下位スコープ リソースに、Spark サービスの既定値から既定のコア数が "*継承*" されます。

2 番目のシナリオでは、該当するスコープで定義された値が各リソースで使用されます。

既定の数のコアがサービスとリソースの両方のスコープで構成されている場合、リソースをスコープとする値によってサービスをスコープとする値が上書きされます。これは、特定の設定に対して **ユーザーが構成する** 最下位のスコープであるためです。

## <a name="next-steps"></a>次の手順

構成に関する具体的な情報については、関連記事を参照してください。

- [ビッグ データ クラスターの配置をカスタマイズする](deployment-custom-configuration.md)
- [配置後にビッグ データ クラスターを構成する](configure-bdc-postdeployment.md)
- [ビッグ データ クラスターを構成する - CU8 リリース以前](configure-bdc-pre-configuration.md)

リファレンス:  
- [SQL Server ビッグ データ クラスターの構成プロパティ](reference-config-bdc-overview.md)
- [Apache Spark と Apache Hadoop (HDFS) の構成プロパティ](reference-config-spark-hadoop.md)
- [SQL Server マスター インスタンスの構成プロパティ - CU9 より前のリリース](reference-config-master-instance.md)
- [azdata CLI](../azdata/reference/reference-azdata.md)