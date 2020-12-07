---
title: クラスターの構成
titleSuffix: Configure a SQL Server big data cluster
description: SQL Server ビッグ データ クラスターの構成方法概要
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: rahul.ajmera
ms.date: 08/04/2020
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b75f6946af9a13d6a8202c627d4c24a2225a51c1
ms.sourcegitcommit: 4545b502e3cae7136411fd9a7c15450315665f38
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2020
ms.locfileid: "94549992"
---
# <a name="configure-a-sql-server-big-data-cluster"></a>SQL Server ビッグ データ クラスターを構成する

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

展開時、SQL Server 2019 ビッグ データ クラスターで SQL Server マスター インスタンス、Apache Spark、Apache Hadoop のプロパティを構成できます。

展開後、ビッグ データ クラスターでは、構成プロパティを変更できません。

## <a name="configuration-scopes"></a>構成スコープ
ビッグ データ クラスターの構成には、`service` と `resource` という 2 つのスコープ レベルがあります。 設定の階層も、この順序に従って、上位から下位に適用されます。 BDC コンポーネントでは、最下位のスコープで定義された設定の値が使用されます。 特定のスコープで設定が定義されていない場合は、上位の親スコープから値が継承されます。

たとえば、記憶域プールと Sparkhead `resources` で使用される Spark ドライバーの既定のコア数を定義できます。 次の 2 つの方法で行います。 
- `Spark` サービス スコープで既定のコア値を指定する  
- `storage-0` と `sparkhead` リソース スコープで既定のコア値を指定する

最初のシナリオでは、Spark サービス (記憶域プールと Sparkhead) のすべての下位スコープ リソースに、Spark サービスの既定値から既定のコア数が "*継承*" されます。

2 番目のシナリオでは、該当するスコープで定義された値が各リソースで使用されます。

既定の数のコアがサービスとリソースの両方のスコープで構成されている場合、リソースをスコープとする値によってサービスをスコープとする値が上書きされます。これは、特定の設定に対して **ユーザーが構成する** 最下位のスコープであるためです。

構成に関する具体的な情報については、関連記事を参照してください。

方法: 
- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] のマスター インスタンスを構成する](configure-sql-server-master-instance.md)
- [ビッグ データ クラスターで Apache Spark と Apache Hadoop を構成する](configure-spark-hdfs.md)

リファレンス:  
- [SQL Server マスター インスタンスの構成プロパティ](reference-config-master-instance.md)
- [Apache Spark と Apache Hadoop (HDFS) の構成プロパティ](reference-config-spark-hadoop.md)
