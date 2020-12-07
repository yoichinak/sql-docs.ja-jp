---
description: MDX データ操作 - REFRESH CUBE
title: REFRESH CUBE ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 05ae95c97ae21d3b8ff7b4e457cf3ddf8cc38989
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387056"
---
# <a name="mdx-data-definition---refresh-cube"></a>MDX データ操作 - REFRESH CUBE


  キューブのクライアントキャッシュを更新します。  
  
## <a name="syntax"></a>構文  
  
```  
  
REFRESH CUBECube_Name   
```  
  
## <a name="arguments"></a>引数  
 *Cube_Name*  
 キューブ名を提供する有効な文字列式です。  
  
## <a name="remarks"></a>解説  
 のインスタンスに接続されているクライアントアプリケーションの場合 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 、このステートメントによって、クライアントアプリケーションでキャッシュされたメモリがサーバーと同期されます。 この検出および更新は日常的かつ自動的に行われますが、同期が行われるまでの時間はクライアント接続文字列の設定によって異なります。 REFRESH CUBE ステートメントは、すぐにデータを更新します。  
  
 ローカルキューブに接続されているクライアントアプリケーションの場合、REFRESH CUBE ステートメントを使用すると、ローカルキューブファイルが再構築されます。  
  
> [!IMPORTANT]  
>  サーバーに格納されている名前付きセットは更新されません。  
  
## <a name="see-also"></a>参照  
 [Mdx&#41;&#40;mdx データ定義ステートメント ](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
