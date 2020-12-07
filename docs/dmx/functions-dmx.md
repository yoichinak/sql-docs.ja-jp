---
description: 関数 (DMX)
title: 関数 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4b8e5d887195e27f706ef995ff92e32aa41b9149
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726196"
---
# <a name="functions-dmx"></a>関数 (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  データマイニング拡張機能 (DMX) を使用してのオブジェクトのクエリを実行する場合、関数を使用すると、 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データマイニングモデルまたは入力データセットの列の値だけでなく、より多くの情報を返すことができます。 たとえば、DMX クエリを使用して、列の予測値だけでなく、予測が正しい確率も返すことができます。 DMX 関数だけでなく、Microsoft Visual Basic for Applications (VBA)、Microsoft Excel、およびストアドプロシージャの関数も使用できます。  
  
## <a name="dmx-functions"></a>DMX 関数  
 DMX 関数は、次のタスクの実行に使用できます。  
  
-   予測を返します。  
  
-   確率やサポートなどの予測に関する統計を返します。  
  
-   クエリ結果をフィルター処理します。  
  
-   テーブル式の順序を変更します。  
  
 ほとんどの DMX 関数は、予測のサポートなど、スカラー値を返します。しかし、いくつかは表形式の結果を返します。 たとえば、PredictHistogram 関数は、指定された予測可能列の各状態のサポートと確率を含むテーブルを返します。 結果は、新しい表形式の列として表示されます。  
  
 **詳細については、「** [dmx&#41;&#40;の一般的な予測関数](../dmx/general-prediction-functions-dmx.md)」、「 [dmx&#41; 関数リファレンス」 &#40;「データマイニング拡張](../dmx/data-mining-extensions-dmx-function-reference.md)機能」を参照してください。  
  
## <a name="visual-basic-for-applications-vba-and-excel-functions"></a>Visual Basic for Applications (VBA) と Excel 関数  
 DMX 関数に加えて、DMX ステートメントからさまざまな VBA および Excel 関数を呼び出すこともできます。 たとえば、lCase 関数を使用すると、TM_Decision_Tree モデルコンテンツの Attribute_Name 列の表示方法を変更できます。 これを次のコードサンプルに示します。  
  
```  
SELECT lCase([Attribute_Name])   
FROM [TM_Decision_Tree].CONTENT  
```  
  
 VBA と Excel の両方に同じ関数が存在する場合は、DMX ステートメントで **vba** または **excel**を使用して関数名の前に付ける必要があります。 たとえば、またはを使用 `VBA!Log` し `Excel!Log` ます。 使用する VBA または Excel 関数が DMX または多次元式 (MDX) にも存在する場合、または関数にドル記号 ($) が含まれている場合は、角かっこ ([]) を使用して関数をエスケープする必要があります。 たとえば、関数呼び出しは `[VBA!Format]` のようになります。  
  
## <a name="stored-procedures"></a>ストアド プロシージャ  
 共通言語ランタイム プログラミング言語を使用して、DMX の機能を拡張するストアド プロシージャを作成できます。 たとえば、回帰ツリーマイニングモデルは、回帰式を記述する A、B などの係数を返しますが、モデルは + Bx = y などの式自体を返しません。 ただし、データ マイニング モデル オブジェクトを使用して、コンテンツ スキーマを操作し、出力として回帰式を返すストアド プロシージャは記述できます。 したがって、DMX ステートメントは、クエリ結果の一部として回帰式の一覧を返すことができます。  
  
 **詳細については、「** [多次元モデルアセンブリ管理](/analysis-services/multidimensional-models/multidimensional-model-assemblies-management)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [DMX&#41; リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-reference.md)   
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41; オペレーターリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [DMX&#41; ステートメントリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-statements.md)   
 [DMX&#41; 構文表記規則を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [DMX&#41; の構文要素を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)   
 [構造と DMX 予測クエリの使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
