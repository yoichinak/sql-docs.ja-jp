---
description: データマイニング拡張機能 (DMX) ステートメントリファレンス
title: データマイニング拡張機能 (DMX) ステートメントリファレンス |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ce95adec18bd17dce45fdc988b6db92d66383c74
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88414098"
---
# <a name="data-mining-extensions-dmx-statements"></a>データ マイニング拡張機能 (DMX) ステートメント
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  でデータマイニングモデルを使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] するには、次の主要なタスクが必要です。  
  
-   マイニング構造とマイニングモデルの作成  
  
-   マイニング構造とマイニングモデルの処理  
  
-   マイニング構造またはマイニング モデルの削除あるいはドロップ  
  
-   マイニングモデルのコピー  
  
-   マイニングモデルの参照  
  
-   マイニングモデルに対する予測  
  
 データマイニング拡張機能 (DMX) ステートメントを使用して、これらの各タスクをプログラムで実行できます。  
  
 マイニング構造とマイニングモデルの作成  
 [CREATE マイニング structure &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md)ステートメントを使用して、新しいマイニング構造をデータベースに追加します。 その後、 [ALTER マイニング構造 &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md) ステートメントを使用して、マイニングモデルをマイニング構造に追加できます。  
  
 [CREATE マイニング model &#40;DMX&#41;](../dmx/create-mining-model-dmx.md)ステートメントを使用して、新しいマイニングモデルと関連するマイニング構造を作成します。  
  
 マイニング構造とマイニングモデルの処理  
 [INSERT INTO &#40;DMX&#41;](../dmx/insert-into-dmx.md)ステートメントを使用して、マイニング構造とマイニングモデルを処理します。  
  
 マイニング構造またはマイニング モデルの削除あるいはドロップ  
 [DELETE &#40;DMX&#41;](../dmx/delete-dmx.md)ステートメントを使用して、マイニングモデルまたはマイニング構造からすべてのトレーニング済みデータを削除します。 マイニング構造 [&#40;dmx&#41;](../dmx/drop-mining-structure-dmx.md) を使用するか、 [dmx&#41;ステートメント &#40;](../dmx/drop-mining-model-dmx.md) 削除して、データベースからマイニング構造またはマイニングモデルを完全に削除します。  
  
 マイニングモデルのコピー  
 [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md)ステートメントを使用して、既存のマイニングモデルの構造を新しいマイニングモデルにコピーし、同じデータを使用して新しいモデルをトレーニングします。  
  
 マイニングモデルの参照  
 [Select &#40;DMX&#41;](../dmx/select-dmx.md)ステートメントを使用して、データマイニングアルゴリズムによって計算され、モデルのトレーニング中にデータマイニングモデルに格納される情報を参照します。 と同様に、 [!INCLUDE[tsql](../includes/tsql-md.md)] SELECT ステートメントで複数の句を使用して、その機能を拡張することができます。 これらの句には、からの[DISTINCT \<model> ](../dmx/select-distinct-from-model-dmx.md)が含ま[れて \<model> います。ケース](../dmx/select-from-model-cases-dmx.md) [ \<model> 。SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md)、[から \<model> です。コンテンツ](../dmx/select-from-model-content-dmx.md)および[からの \<model> 。DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md)。  
  
 マイニングモデルに対する予測  
 既存のマイニングモデルに基づいた予測を作成するには、SELECT ステートメントの [予測結合](../dmx/select-from-model-prediction-join-dmx.md) 句を使用します。  
  
 また、モデルのインポートとエクスポートには、 [&#40;dmx&#41;のインポート ](../dmx/import-dmx.md) と [エクスポート &#40;dmx&#41;](../dmx/export-dmx.md) ステートメントを使用して行うこともできます。  
  
 これらのタスクは、次の表に示す、データ定義ステートメントとデータ操作ステートメントの 2 つのカテゴリに分類されます。  
  
|トピック|説明|  
|-----------|-----------------|  
|[データ マイニング拡張機能 (DMX) データ定義ステートメント](../dmx/dmx-statements-data-definition.md)|データ定義言語 (DDL) の一部。 新しいマイニング モデルの定義 (学習を含む)、またはデータベースからの既存のマイニング モデルのドロップに使用されます。|  
|[DMX&#41; データ操作ステートメントを &#40;データマイニング拡張機能](../dmx/dmx-statements-data-manipulation.md)|データ操作言語 (DML) の一部。 モデルの参照または予測の作成を含む、既存のマイニング モデルでの作業に使用されます。|  
  
## <a name="see-also"></a>参照  
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41; オペレーターリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [DMX&#41; 構文表記規則を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [DMX&#41; の構文要素を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-elements.md)  
  
  
