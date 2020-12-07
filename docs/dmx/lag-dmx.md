---
description: ラグ (DMX)
title: Lag (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4e7aa504c3afd236ddd748a7ee81cbbb6cf90b7c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466572"
---
# <a name="lag-dmx"></a>ラグ (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  現在のケースの日付とトレーニングセットの最後の日付の間のタイムスライスを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Lag()  
```  
  
## <a name="return-type"></a>戻り値の型  
 整数型のスカラー値です。  
  
## <a name="remarks"></a>解説  
 入れ子になったテーブル内に KEY TIME 列が配置されているモデルで **Lag** 関数を使用する場合、関数は、ステートメントのサブ選択内に配置する必要があります。  
  
## <a name="examples"></a>例  
 次の例では、モデルのトレーニングに使用されたデータの過去12か月以内に該当するケースを返します。  
  
```  
SELECT * FROM [Forecasting].CASES  
WHERE Lag() < 12  
```  
  
## <a name="see-also"></a>参照  
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41;&#40;関数 ](../dmx/functions-dmx.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)  
  
  
