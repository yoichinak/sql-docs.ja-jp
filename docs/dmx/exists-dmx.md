---
description: 存在 (DMX)
title: 存在 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1f45a4a1d0e709c6b8eb9bb7217d268420f31d07
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726233"
---
# <a name="exists-dmx"></a>存在 (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  指定されたサブクエリが少なくとも1つの行を返す場合に **true** を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
EXISTS(<subquery>)  
```  
  
## <a name="arguments"></a>引数  
 *subquery*  
 Select * FROM [WHERE] 形式の SELECT ステートメント \<column name> \<predicate list> 。  
  
## <a name="result-type"></a>結果の種類  
 サブクエリによって返される結果セットに少なくとも1つの行が含まれている場合に **true** を返します。それ以外の場合は **false**を返します。  
  
## <a name="remarks"></a>解説  
 EXISTS の前に NOT キーワードを使用できます。たとえば、のように `WHERE NOT EXISTS (<subquery>)` なります。  
  
 EXISTS のサブクエリ引数に追加する列の一覧は、関係ありません。関数は、条件を満たす行が存在するかどうかのみをチェックします。  
  
## <a name="examples"></a>例  
 EXISTS と NOT EXISTS を使用して、入れ子になったテーブルの条件を確認することができます。 これは、データマイニングモデルのトレーニングまたはテストに使用されるデータを制御するフィルターを作成する場合に便利です。 詳細については、「[マイニング モデルのフィルター選択 (Analysis Services - データ マイニング)](/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining)」を参照してください。  
  
 次の例は、 `[Association]` 「 [基本的なデータマイニングチュートリアル](/previous-versions/sql/sql-server-2016/ms167167(v=sql.130))」で作成したマイニング構造とマイニングモデルに基づいています。 このクエリでは、顧客が少なくとも1つの patch kit を購入したケースのみが返されます。  
  
```  
SELECT * FROM [Association].CASES  
WHERE EXISTS  
(  
SELECT * FROM [v Assoc Seq Line Numbers]  
WHERE [[Model] = 'Patch kit'  
)  
```  
  
 このクエリによって返される同じデータを表示する別の方法として、アソシエーションビューアーでモデルを開き、[アイテム **セット Patch kit = Existing**] を右クリックし **て [ドリルスルー** ] オプションを選択し、[ **モデルケースのみ**] を選択します。  
  
## <a name="see-also"></a>参照  
 [DMX&#41;&#40;関数 ](../dmx/functions-dmx.md)   
 [モデル フィルターの構文と例 (Analysis Services - データ マイニング)](/analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining)  
  
