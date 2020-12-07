---
title: リソース ガバナーを使用した管理
description: リソース ガバナーを使用して、SQL Server Machine Learning Services での Python および R のワークロードに対する CPU、物理 IO、およびメモリ リソースの割り当てを管理する方法について説明します。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/06/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 20506baeb0a22e4e32fd1c4b24a7d00f4493b6d5
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956535"
---
# <a name="manage-python-and-r-workloads-with-resource-governor-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services でリソース ガバナーを使用して Python と R のワークロードを管理する
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

[リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)を使用して、SQL Server Machine Learning Services での Python および R のワークロードに対する CPU、物理 IO、およびメモリ リソースの割り当てを管理する方法について説明します。

Python および R の機械学習アルゴリズムは、多くのコンピューティング処理を必要とします。 ワークロードの優先度によっては、Machine Learning Services に使用できるリソースを増減することが必要になる場合があります。

一般情報については、「[リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)」を参照してください。

> [!NOTE] 
> リソース ガバナーは Enterprise Edition の機能です。

## <a name="default-allocations"></a>既定の割り当て

既定では、機械学習の外部スクリプト ランタイムは、合計マシン メモリの 20% 以下に制限されています。 システムによって異なりますが、一般的に、モデルのトレーニングや多数のデータ行の予測などの本格的な機械学習タスクでは、この制限が不十分である可能性があります。 

## <a name="manage-resources-with-resource-governor"></a>リソース ガバナーを使用したリソースの管理
 
既定では、外部プロセスでは、ローカル サーバー上の合計ホスト メモリの最大 20% が使用されます。 既定のリソース プールを変更して、サーバー全体の変更を加えることができます。外部プロセスで使用できるようにする容量を R と Python のプロセスで使用できるように設定できます。

必要に応じて、関連するワークロード グループと分類子を使用してカスタムの**外部リソース プール**を作成し、特定のプログラム、ホスト、またはその他の条件によって送信された要求のリソース割り当てを決定することもできます。 外部リソース プールは、[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] に導入された種類のリソース プールです。データベース エンジン外部の R および Python のプロセスの管理に役立ちます。

1. [リソース ガバナンスを有効にします](../../relational-databases/resource-governor/enable-resource-governor.md) (既定ではオフになっています)。

2. [外部リソース プールを作成する](../../t-sql/statements/create-external-resource-pool-transact-sql.md)を実行してリソース プールを作成および構成し、その後 [ALTER RESOURCE GOVERNOR](../../t-sql/statements/alter-resource-governor-transact-sql.md) を実行してこれを実装します。

3. トレーニングとスコア付けなど、粒度の細かい割り当て用のワークロード グループを作成します。

4. 外部処理の呼び出しをインターセプトする分類子を作成します。

5. 作成したオブジェクトを使用して、クエリとプロシージャを実行します。

チュートリアルについては、「[SQL Server Machine Learning Services のリソース プールを作成する](create-external-resource-pool.md)」の順を追った手順を参照してください。

用語および一般的な概念について詳しくは、「[Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md)」(リソース ガバナーのリソース プール) をご覧ください。

## <a name="processes-under-resource-governance"></a>リソース ガバナンスのプロセス
  
 *外部リソース プール*を使用して、次の実行可能ファイルによって使用されるリソースをデータベース エンジン インスタンスで管理できます。

+ SQL Server からローカルで呼び出したときまたは SQL Server でリモート コンピューティング コンテキストとしてリモートで呼び出したときには Rterm.exe
+ SQL Server からローカルで呼び出したときまたは SQL Server でリモート コンピューティング コンテキストとしてリモートで呼び出したときには Python.exe
+ BxlServer.exe およびサテライト プロセス
+ PythonLauncher.dll などのスタート パッドで起動されたサテライト プロセス
  
> [!NOTE]
> リソース ガバナーによるスタート パッド サービスの直接管理はサポートされません。 スタート パッドは、Microsoft によって提供されるランチャーのみをホストできる信頼されたサービスです。 信頼できるランチャーは、リソースを過度に消費しないように明示的に構成されています。
  
## <a name="next-steps"></a>次のステップ

+ [Machine Learning 用のリソース プールの作成](create-external-resource-pool.md)
+ [リソース ガバナーのリソース プール](../../relational-databases/resource-governor/resource-governor-resource-pool.md)