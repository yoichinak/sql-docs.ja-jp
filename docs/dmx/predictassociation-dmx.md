---
description: PredictAssociation (DMX)
title: PredictAssociation (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b94af0ab8da71e5bf978852fd884d46b460715bc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426154"
---
# <a name="predictassociation-dmx"></a>PredictAssociation (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  結合メンバーシップを予測します。  
  
たとえば、PredictAssociation 関数を使用すると、顧客の買い物かごの現在の状態に関する一連の推奨事項を取得できます。 
  
## <a name="syntax"></a>構文  
  
```  
  
PredictAssociation(<table column reference>, option1, option2, n ...)  
```  
  
## <a name="applies-to"></a>適用対象  
 関連付けや分類アルゴリズムなど、予測可能な入れ子になったテーブルを含むアルゴリズム。 入れ子になったテーブルをサポートする分類アルゴリズムには、 [!INCLUDE[msCoName](../includes/msconame-md.md)] デシジョンツリー、 [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes、 [!INCLUDE[msCoName](../includes/msconame-md.md)] ニューラルネットワークアルゴリズムが含まれます。  
  
## <a name="return-type"></a>戻り値の型  
 \<table expression>  
  
## <a name="remarks"></a>解説  
 **PredictAssociation**関数のオプションには、EXCLUDE_NULL、INCLUDE_NULL、包含、排他 (既定)、INPUT_ONLY、INCLUDE_STATISTICS、および INCLUDE_NODE_ID があります。  
  
> [!NOTE]  
>  包含、排他、INPUT_ONLY、INCLUDE_STATISTICS はテーブル列参照にのみ適用され、EXCLUDE_NULL と INCLUDE_NULL はスカラー列参照にのみ適用されます。  
  
 INCLUDE_STATISTICS は **$Probability** と **$AdjustedProbability**だけを返します。  
  
 数値パラメーター *n* を指定した場合、 **PredictAssociation** 関数は確率に基づいて、最も可能性の高い上位 n の値を返します。  
  
```  
PredictAssociation(colref, [$AdjustedProbability], n)  
```  
  
 **$AdjustedProbability**を含めた場合、ステートメントは、 **$AdjustedProbability**に基づいて上位*n*の値を返します。  
  
## <a name="examples"></a>例  
 次の例では、 **PredictAssociation** 関数を使用して、一緒に販売される可能性が最も高い Adventure works データベースの4つの製品を返します。  
  
```  
SELECT  
  PredictAssociation([Association].[v Assoc Seq Line Items],4)  
From  
  [Association]  
```  
次の例では、SHAPE 句を使用して、入れ子になったテーブルを予測関数への入力として使用する方法を示します。 SHAPE クエリでは、customerId が1つの行セットと入れ子になったテーブルを2番目の列として作成します。この列には、顧客が既に導入した製品の一覧が含まれています。 

~~~~
SELECT T.[CustomerId], PredictAssociation(MyNestedTable, 5) // returns top 5 associated items
FROM My Model
PREDICTION JOIN
SHAPE {
    OPENQUERY([Adventure Works DW],'SELECT CustomerID, OrderNumber
    FROM vAssocSeqOrders ORDER BY OrderNumber')
} APPEND (
    {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, model FROM 
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}
  RELATE OrderNumber to OrderNumber) AS T
~~~~  

  
## <a name="see-also"></a>参照  
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41;&#40;関数 ](../dmx/functions-dmx.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)  
  
  
