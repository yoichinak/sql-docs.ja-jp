---
description: KPIValue (MDX)
title: KPIValue (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 24189ffb3e9a550fd4819b15cfbd8ae41a48a64f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471814"
---
# <a name="kpivalue-mdx"></a>KPIValue (MDX)


  指定された主要業績評価指標 (KPI) の値を計算するメンバーを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
KPIValue(KPI_Name)  
```  
  
## <a name="arguments"></a>引数  
 *KPI_Name*  
 KPI の名前を指定する有効な文字列式です。  
  
## <a name="remarks"></a>解説  
  
## <a name="example"></a>例  
 次の例では、会計年度の属性階層の3つのメンバーの子孫について、チャネル収益メジャーの KPI 値、KPI 目標、KPI の状態、および KPI の傾向が返されます。  
  
```  
SELECT  
   { KPIValue("Channel Revenue"),   
     KPIGoal("Channel Revenue"),  
     KPIStatus("Channel Revenue"),   
     KPITrend("Channel Revenue")  
   } ON Columns,  
Descendants  
   ( { [Date].[Fiscal].[Fiscal Year].&[2002],  
       [Date].[Fiscal].[Fiscal Year].&[2003],  
       [Date].[Fiscal].[Fiscal Year].&[2004]   
     }, [Date].[Fiscal].[Fiscal Quarter]  
   ) ON Rows  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
