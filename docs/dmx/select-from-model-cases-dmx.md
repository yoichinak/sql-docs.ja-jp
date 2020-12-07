---
description: '[モデルから] を選択し &lt; &gt; ます。ケース (DMX)'
title: '[モデルから] を選択し &lt; &gt; ます。ケース (DMX) |Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 289a25088c61988382093f50526546bf5036a510
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727663"
---
# <a name="select-from-ltmodelgtcases-dmx"></a>[モデルから] を選択し &lt; &gt; ます。ケース (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  ドリルスルーをサポートし、モデルのトレーニングに使用されたケースを返します。 マイニング構造とマイニング モデルについてドリルスルーを有効にした場合、ユーザーが適切な権限を持っているときは、モデルに含まれていない構造列も返すことができます。  
  
 マイニングモデルでドリルスルーが有効になっていない場合、このステートメントは失敗します。  
  
> [!NOTE]  
>  データ マイニング拡張機能 (DMX) では、ドリルスルーはモデルの作成時にのみ可能です。 を使用して既存のモデルにドリルスルーを追加することはでき [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ますが、ケースを表示または照会する前にモデルを再処理する必要があります。  
  
 ドリルスルーを有効にする方法の詳細については、「 [dmx&#41;&#40;のマイニングモデルの作成 ](../dmx/create-mining-model-dmx.md)」、「dmx [&#41;の &#40;の選択 ](../dmx/select-into-dmx.md)」、および「 [DMX &#40;&#41;のマイニング構造の変更 ](../dmx/alter-mining-structure-dmx.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.CASES  
[WHERE <condition expression>][ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>引数  
 *n*  
 省略可能。 返す行数を指定する整数値です。  
  
 *式の一覧*  
 式のコンマ区切りのリストです。 式には、列識別子、ユーザー定義関数、Udf、および VBA 関数などを含めることができます。  
  
 マイニング モデルに含まれていない構造列を含めるには、関数 `StructureColumn('<structure column name>')` を使用します。  
  
 *model*  
 モデル識別子。  
  
 *条件式*  
 列リストから返される値を制限する条件。  
  
 *式 (expression)*  
 省略可能。 スカラー値を返す式。  
  
## <a name="remarks"></a>解説  
 マイニングモデルとマイニング構造の両方でドリルスルーが有効になっている場合、モデルおよび構造に対するドリルスルー権限を持つロールのメンバーであるユーザーは、マイニングモデルに含まれていないマイニング構造の列にアクセスできます。 したがって、機密データや個人情報を保護するには、個人情報をマスクするデータソースビューを作成し、必要な場合にのみ、マイニング構造に対する **Allowdrillthrough スルー** 権限を付与する必要があります。  
  
 [Lag &#40;DMX&#41;](../dmx/lag-dmx.md)関数をタイムシリーズモデルと共に使用して、各ケースと初期時間の間のタイムラグを返したりフィルター処理したりできます。  
  
 **WHERE**句で[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)関数を使用すると、スキーマ行セットの NODE_UNIQUE_NAME 列によって指定されたノードに関連付けられているケースのみが返されます。  
  
## <a name="examples"></a>例  
 次の例は、 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] データベースとそれに関連付けられているマイニングモデルに基づいた、マイニング構造を対象としたメーリングに基づいています。 詳細については、「 [基本的なデータマイニングチュートリアル](/previous-versions/sql/sql-server-2016/ms167167(v=sql.130))」を参照してください。  
  
### <a name="example-1-drillthrough-to-model-cases-and-structure-columns"></a>例 1: モデルケースおよび構造列へのドリルスルー  
 次の例では、対象となるメーリングモデルのテストに使用されたすべてのケースの列が返されます。 モデルが作成されているマイニング構造に、提示されたテストデータセットがない場合、このクエリは0ケースを返します。 必要な列のみを返す式のリストを使用できます。  
  
```  
SELECT * FROM [TM Decision Tree].Cases  
WHERE IsTestCase();  
```  
  
### <a name="example-2-drillthrough-to-training-cases-in-a-specific-node"></a>例 2 : 特定のノードのトレーニング ケースにドリルスルーする  
 次の例では、クラスター2のトレーニングに使用されたケースのみが返されます。 Cluster 2 のノードの NODE_UNIQUE_NAME 列の値は '002' です。 また、この例では、マイニングモデルの一部ではない1つの構造列 [Customer Key] が返され、列の別名が指定されてい `CustomerID` ます。 構造列の名前は文字列値として渡されるため、角かっこではなく引用符で囲む必要があることに注意してください。  
  
```  
SELECT StructureColumn('Customer Key') AS CustomerID, *   
FROM [TM_Clustering].Cases  
WHERE IsTrainingCase()  
AND IsInNode('002')  
```  
  
 構造列を返すには、マイニング モデルとマイニング構造の両方についてドリルスルー権限を有効にする必要があります。  
  
> [!NOTE]  
>  一部のマイニングモデルの種類では、ドリルスルーがサポートされていません。 ドリルスルーをサポートするモデルの詳細については、「 [ドリルスルークエリ &#40;データマイニング&#41;](/analysis-services/data-mining/drillthrough-queries-data-mining)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [DMX&#41;を選択 &#40;](../dmx/select-dmx.md)   
 [DMX&#41; データ定義ステートメント &#40;のデータマイニング拡張機能](../dmx/dmx-statements-data-definition.md)   
 [DMX&#41; データ操作ステートメントを &#40;データマイニング拡張機能](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
