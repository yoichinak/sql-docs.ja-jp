---
description: Instr (MDX)
title: Instr (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 877fc4658081108e810e404dfc8d4a368c6964ba
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387358"
---
# <a name="instr-mdx"></a>Instr (MDX)


  ある文字列が別の文字列内で最初に出現する位置を返します。  
  
## <a name="syntax"></a>構文  
  
```  
InStr([start, ]searched_string, search_string[, compare])  
```  
  
## <a name="arguments"></a>引数  
 *start*  
 Optional各検索の開始位置を設定する数値式。 この値を省略した場合、検索は最初の文字位置から開始されます。 start が null の場合、関数の戻り値は未定義となります。  
  
 *searched_string*  
 検索範囲となる文字列式。  
  
 *search_string*  
 検索対象の文字列式。  
  
 *比較*  
 (省略可) 整数値です。 この引数は常に無視されます。 他の言語での他の **Instr** 関数との互換性のために定義されています。  
  
## <a name="return-value"></a>戻り値  
 *String1**の開始位置を表す*整数値。  
  
 また、 **InStr** 関数は、条件に応じて、次の表に示す値を返します。  
  
|条件|戻り値|  
|---------------|------------------|  
|String1 の長さが 0|ゼロ (0)|  
|String1 が NULL|undefined|  
|String2 は長さが0です|start|  
|String2 が NULL|undefined|  
|String2 が見つからない|ゼロ (0)|  
|start が Len (String2) を超えています。|ゼロ (0)|  
  
## <a name="remarks"></a>解説  
  
> [!WARNING]  
>  **Instr** は、常に大文字と小文字を区別しない比較を実行します。  
  
## <a name="example"></a>例  
 次の例は、 **Instr** 関数の使用方法を示しています。また、さまざまな結果のシナリオを示しています。  
  
```  
with   
    member [Date].[Date].[Results] as "Results"  
    member measures.[lowercase found in lowercase string] as InStr( "abcdefghijklmnñopqrstuvwxyz", "o")  
    member measures.[uppercase found in lowercase string] as InStr( "abcdefghijklmnñopqrstuvwxyz", "O")  
    member measures.[searched string is empty]            as InStr( "", "o")  
    member measures.[searched string is null]             as iif(IsError(InStr( null, "o")), "Is Error", iif(IsNull(InStr( null, "o")), "Is Null","Is undefined"))  
    member measures.[search string is empty]              as InStr( "abcdefghijklmnñopqrstuvwxyz", "")  
    member measures.[search string is empty start 10]     as InStr(10, "abcdefghijklmnñopqrstuvwxyz", "")  
    member measures.[search string is null]               as iif(IsError(InStr( null, "o")), "Is Error", iif(IsNull(InStr( null, "o")), "Is Null","Is undefined"))  
    member measures.[found from start 10]                 as InStr( 10, "abcdefghijklmnñopqrstuvwxyz", "o")  
    member measures.[NOT found from start 17]             as InStr( 17, "abcdefghijklmnñopqrstuvwxyz", "o")  
    member measures.[NULL start]                          as iif(IsError(InStr( null, "abcdefghijklmnñopqrstuvwxyz", "o")), "Is Error", iif(IsNull(InStr( null, "abcdefghijklmnñopqrstuvwxyz", "o")), "Is Null","Is undefined"))  
    member measures.[start greater than searched length]  as InStr( 170, "abcdefghijklmnñopqrstuvwxyz", "o")  
  
select  [Results] on columns,  
       { measures.[lowercase found in lowercase string]  
       , measures.[uppercase found in lowercase string]  
       , measures.[searched string is empty]  
       , measures.[searched string is null]  
       , measures.[search string is empty]  
       , measures.[search string is empty start 10]  
       , measures.[search string is null]  
       , measures.[found from start 10]  
       , measures.[NOT found from start 17]  
       , measures.[NULL start]   
       , measures.[start greater than searched length]  
       } on rows  
  
from [Adventure Works]  
```  
  
 取得した結果を次の表に示します。  
  
|メジャーのフィールド|結果|  
|-|-|  
|小文字の文字列で小文字が見つかりました|16|  
|小文字の文字列で大文字が見つかりました|16|  
|検索した文字列が空|0|  
|検索された文字列が null です|未定義|  
|検索文字列が空です|1|  
|検索する文字列が開始位置 10 から空|10|  
|検索する文字列が NULL|未定義|  
|開始位置 10 から検索|16|  
|開始17から見つかりませんでした|0|  
|NULL で開始|未定義|  
|検索される長さを超えて開始|0|  
  
  
