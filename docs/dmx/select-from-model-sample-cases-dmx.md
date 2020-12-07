---
description: '[モデルから] を選択し &lt; &gt; ます。SAMPLE_CASES (DMX)'
title: '[モデルから] を選択し &lt; &gt; ます。SAMPLE_CASES (DMX) |Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: af927d9c998d245c31511c29450eafac31e1d54b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500886"
---
# <a name="select-from-ltmodelgtsample_cases-dmx"></a>[モデルから] を選択し &lt; &gt; ます。SAMPLE_CASES (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  データ マイニング モデルの学習に使用されるケースを表すサンプル ケースを返します。  
  
 このステートメントを使用するには、マイニングモデルを作成するときにドリルスルーを有効にする必要があります。 ドリルスルーを有効にする方法の詳細については、「 [dmx&#41;&#40;のマイニングモデルの作成 ](../dmx/create-mining-model-dmx.md)」、「 [&#40;dmx&#41;の選択 ](../dmx/select-into-dmx.md)」、「 [マイニング構造の変更 (dmx &#40;](../dmx/alter-mining-structure-dmx.md))」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.SAMPLE_CASES  
[WHERE <condition list>] ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>引数  
 *n*  
 任意。 返す行数を指定する整数値です。  
  
 *式の一覧*  
 関連付けられた列識別子のコンマ区切りのリストです。  
  
 *model*  
 モデル識別子。  
  
 *条件一覧*  
 任意。 列リストから返される値を制限する条件。  
  
 *式 (expression)*  
 任意。 スカラー値を返す式。  
  
## <a name="remarks"></a>解説  
 サンプルケースは生成される場合があり、実際にはトレーニングデータに存在しない可能性があります。 返されたケースは、指定されたコンテンツ ノードを表します。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)]シーケンスクラスターアルゴリズムは、 [!INCLUDE[msCoName](../includes/msconame-md.md)] SELECT FROM の使用をサポートする唯一のアルゴリズムです \<model> 。SAMPLE_CASES サードパーティ製のアルゴリズムでもサポートされている場合があります。  
  
## <a name="examples"></a>例  
 次の例では、Target Mail マイニング モデルの学習に使用されるサンプル ケースを返しています。 **WHERE**句で[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)関数を使用すると、' 000000003 内 ' ノードに関連付けられているケースのみが返されます。 ノード文字列は、スキーマ行セットの NODE_UNIQUE_NAME 列にあります。  
  
```  
Select * from [Sequence Clustering].SAMPLE_Cases  
WHERE IsInNode('000000003')  
```  
  
## <a name="see-also"></a>参照  
 [DMX&#41;を選択 &#40;](../dmx/select-dmx.md)   
 [DMX&#41; データ定義ステートメント &#40;のデータマイニング拡張機能](../dmx/dmx-statements-data-definition.md)   
 [DMX&#41; データ操作ステートメントを &#40;データマイニング拡張機能](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
