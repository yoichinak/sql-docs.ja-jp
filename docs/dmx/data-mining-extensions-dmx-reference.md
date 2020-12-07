---
description: データ マイニング拡張機能 (DMX) リファレンス
title: データマイニング拡張機能 (DMX) リファレンス |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: bd6830e46f10ba20642d1975f293b72b768f7e5b
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726254"
---
# <a name="data-mining-extensions-dmx-reference"></a>データ マイニング拡張機能 (DMX) リファレンス
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  データマイニング拡張機能 (DMX) は、でデータマイニングモデルを作成および操作するために使用できる言語です [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。 DMX を使用して、新しいデータ マイニング モデルの構造の作成、これらのモデルの学習、およびモデルの参照、管理、予測を行うことができます。 DMX は、データ定義言語 (DDL) ステートメント、データ操作言語 (DML) ステートメント、および関数と演算子で構成されています。  
  
## <a name="microsoft-ole-db-for-data-mining-specification"></a>Microsoft OLE DB for Data Mining 仕様  
 のデータマイニング機能は [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 、 [!INCLUDE[msCoName](../includes/msconame-md.md)] データマイニング仕様の OLE DB に準拠するように構築されています。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)]データマイニング仕様の OLE DB では、次のものを定義します。  
  
-   データ マイニング モデルを定義する情報を保持するための構造。  
  
-   データマイニングモデルを作成および操作するための言語です。  
  
 この仕様では、データ マイニングの基礎がデータ マイニング モデル仮想オブジェクトとして定義されます。 データ マイニング モデル オブジェクトは、特定のマイニング モデルに関する既知の事柄をすべてカプセル化します。 データ マイニング モデル オブジェクトは SQL テーブルのような構造になっており、モデルを説明する列、データ型、およびメタ情報から構成されています。 この構造により、SQL の拡張版である DMX 言語を使用して、モデルを作成、使用することができるようになります。  
  
 **詳細については、「** [マイニング構造 &#40;Analysis Services-データマイニング&#41;](/analysis-services/data-mining/mining-structures-analysis-services-data-mining) 」を参照してください。  
  
##  <a name="dmx-statements"></a><a name="BKMK_DMXStatements"></a> DMX ステートメント  
 DMX ステートメントを使用して、データマイニングモデルの作成、処理、削除、コピー、参照、および予測を行うことができます。 DMX にはデータ定義ステートメントおよびデータ操作ステートメントの 2 種類のステートメントがあります。 それぞれの種類のステートメントを使用して、さまざまな種類のタスクを実行できます。  
  
 以下のセクションでは、DMX ステートメントの使用に関する詳細について説明します。  
  
-   [データ定義ステートメント](#BKMK_DDL)  
  
-   [データ操作ステートメント](#BKMK_DML)  
  
-   [クエリの基礎](#BKMK_Queries)  
  
###  <a name="data-definition-statements"></a><a name="BKMK_DDL"></a> データ定義ステートメント  
 DMX のデータ定義ステートメントを使用して、新しいマイニング構造およびマイニングモデルの作成と定義、マイニングモデルとマイニング構造のインポートとエクスポート、およびデータベースからの既存のモデルの削除を行うことができます。 DMX のデータ定義ステートメントは、データ定義言語 (DDL) の一部です。  
  
 DMX のデータ定義ステートメントを使用して、次のタスクを実行できます。  
  
-   [CREATE マイニング structure](../dmx/create-mining-structure-dmx.md)ステートメントを使用してマイニング構造を作成し、 [ALTER マイニング structure](../dmx/alter-mining-structure-dmx.md)ステートメントを使用してマイニングモデルをマイニング構造に追加します。  
  
-   [CREATE マイニング model](../dmx/create-mining-model-dmx.md)ステートメントを使用して空のデータマイニングモデルオブジェクトを構築することにより、マイニングモデルと関連するマイニング構造を同時に作成します。  
  
-   [エクスポート](../dmx/export-dmx.md)ステートメントを使用して、マイニングモデルおよび関連するマイニング構造をファイルにエクスポートします。 [Import](../dmx/import-dmx.md)ステートメントを使用して、EXPORT ステートメントによって作成されたファイルから、マイニングモデルおよび関連するマイニング構造をインポートします。  
  
-   [SELECT into](../dmx/select-into-dmx.md)ステートメントを使用して、既存のマイニングモデルの構造を新しいモデルにコピーし、同じデータでトレーニングします。  
  
-   [DROP マイニングモデル](../dmx/drop-mining-model-dmx.md)ステートメントを使用して、データベースからマイニングモデルを完全に削除します。 削除 [マイニング構造](../dmx/drop-mining-structure-dmx.md) ステートメントを使用して、マイニング構造とそれに関連付けられているすべてのマイニングモデルをデータベースから完全に削除します。  
  
 DMX ステートメントを使用して実行できるデータマイニングタスクの詳細については、「 [データマイニング拡張機能 &#40;dmx&#41; ステートメントリファレンス](../dmx/data-mining-extensions-dmx-statements.md)」を参照してください。  
  
 [DMX ステートメントに戻る](#BKMK_DMXStatements)  
  
###  <a name="data-manipulation-statements"></a><a name="BKMK_DML"></a> データ操作ステートメント  
 DMX のデータ操作ステートメントを使用して、既存のマイニングモデルを操作し、モデルを参照し、それらに対して予測を作成します。 DMX のデータ操作ステートメントは、データ操作言語 (DML) の一部です。  
  
 DMX のデータ操作ステートメントを使用して、次のタスクを実行できます。  
  
-   [INSERT INTO](../dmx/insert-into-dmx.md)ステートメントを使用して、マイニングモデルをトレーニングします。 これは、実際のソースデータをデータマイニングモデルオブジェクトに挿入するのではなく、アルゴリズムによって作成されるマイニングモデルを記述する抽象化を作成します。 INSERT INTO ステートメントのソースクエリについては、「」を参照 [\<source data query>](../dmx/source-data-query.md) してください。  
  
-   モデルのトレーニング中に計算され、ソースデータの統計情報など、データマイニングモデルに格納されている情報を参照するには、SELECT ステートメントを拡張します。 SELECT ステートメントの機能を拡張するために含めることができる句は次のとおりです。  
  
    -   [DMX&#41;&#62; &#40;&#60;モデルから [DISTINCT] を選択します。 ](../dmx/select-distinct-from-model-dmx.md)  
  
    -   [&#60;モデル&#62; から選択します。DMX&#41;のコンテンツ &#40;](../dmx/select-from-model-content-dmx.md)  
  
    -   [&#60;モデル&#62; から選択します。DMX&#41;&#40;ケース ](../dmx/select-from-model-cases-dmx.md)  
  
    -   [&#60;モデル&#62; から選択します。DMX&#41;&#40;の SAMPLE_CASES ](../dmx/select-from-model-sample-cases-dmx.md)  
  
    -   [&#60;モデル&#62; から選択します。DMX&#41;&#40;の DIMENSION_CONTENT ](../dmx/select-from-model-dimension-content-dmx.md)  
  
-   SELECT ステートメントの [予測結合](../dmx/select-from-model-prediction-join-dmx.md) 句を使用して、既存のマイニングモデルに基づく予測を作成します。 予測結合ステートメントのソースクエリについては、「」を参照して [\<source data query>](../dmx/source-data-query.md) ください。  
  
-   [DELETE &#40;DMX&#41;](../dmx/delete-dmx.md)ステートメントを使用して、モデルまたは構造からすべてのトレーニング済みデータを削除します。  
  
 DMX ステートメントを使用して実行できるデータマイニングタスクの詳細については、「 [データマイニング拡張機能 &#40;dmx&#41; ステートメントリファレンス](../dmx/data-mining-extensions-dmx-statements.md)」を参照してください。  
  
 [DMX ステートメントに戻る](#BKMK_DMXStatements)  
  
###  <a name="dmx-query-fundamentals"></a><a name="BKMK_Queries"></a> DMX クエリの基礎  
 SELECT ステートメントは、ほとんどの DMX クエリの基礎となります。 このようなステートメントで使用する句に応じて、マイニングモデルに対して参照、コピー、または予測を行うことができます。 予測クエリでは、SELECT の形式を使用して、既存のマイニングモデルに基づいて予測を作成します。 関数を使用することで、データ マイニング モデルの固有の機能では行えないマイニング モデルの参照およびクエリを行うことができます。  
  
 DMX 関数を使用すると、モデルの学習中に検出された情報の取得および新しい情報の計算を行うことができます。 これらの関数は、基になるデータまたは予測の精度を示す統計を返す、または予測の拡張された説明を返すなど、さまざまな目的で使用できます。  
  
 **詳細について**は、 [Dmx の Select ステートメントを理解](../dmx/understanding-the-dmx-select-statement.md)する、 [dmx&#41;&#40;の一般的な予測関数](../dmx/general-prediction-functions-dmx.md)、Dmx[予測クエリの構造と使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)、[データマイニング拡張機能 &#40;dmx&#41; 関数リファレンスを参照](../dmx/data-mining-extensions-dmx-function-reference.md)して**ください。**    
  
 [DMX ステートメントに戻る](#BKMK_DMXStatements)  
  
## <a name="see-also"></a>参照  
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41; オペレーターリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [DMX&#41; ステートメントリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-statements.md)   
 [DMX&#41; 構文表記規則を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [DMX&#41; の構文要素を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)   
 [構造と DMX 予測クエリの使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
