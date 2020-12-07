---
description: MDX データ操作 - CLEAR CALCULATIONS
title: CLEAR の計算ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 06f3fc9d29630f3f69b994c2b4e7cf809b6b9efd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387006"
---
# <a name="mdx-data-manipulation---clear-calculations"></a>MDX データ操作 - CLEAR CALCULATIONS


  キューブからすべての計算を削除し、計算パス0にキューブを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
CLEAR CALCULATIONS [FROMCube_Expression]  
```  
  
## <a name="arguments"></a>引数  
 *Cube_Expression*  
 有効な多次元式 (MDX) キューブ式です。  
  
## <a name="remarks"></a>解説  
 MDX スクリプトなど、キューブのコンテキストがわかっている場合は、 **from** 句を省略できます。  
  
> [!NOTE]  
>  このステートメントは、サーバー管理者やデータベース管理者、またはキューブのソース データにアクセスできるロールのメンバー (つまり、ReadSourceData=true) のみが実行できます。  
  
## <a name="see-also"></a>参照  
 [Mdx&#41;&#40;MDX データ操作ステートメント ](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
