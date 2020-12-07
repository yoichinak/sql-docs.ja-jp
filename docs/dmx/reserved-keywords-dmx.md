---
description: 予約されているキーワード (DMX)
title: 予約済みキーワード (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fa446f07b81707c9476b133a430281057c476dcf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487748"
---
# <a name="reserved-keywords-dmx"></a>予約されているキーワード (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)] は排他的に使用する特定のキーワードが予約されています。 これらのキーワードは、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] dmx 言語リファレンスで定義されている位置を除き、データマイニング拡張機能 (dmx) ステートメントのどこでも使用できません。 これらの制限された DMX キーワードには、次のメンバーが含まれます。  
  
-   トピック「 [DMX データ定義ステートメント](../dmx/dmx-statements-data-definition.md)」に記載されているすべてのデータ定義ステートメント。  
  
-   トピック「 [DMX 関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)」に一覧表示されているすべてのデータマイニングクエリ関数。  
  
-   トピック「 [DMX 演算子リファレンス](../dmx/data-mining-extensions-dmx-operator-reference.md)」に一覧表示されているすべての演算子。  
  
-   多次元式 (MDX) クエリ言語で定義され、DMX ステートメントの一部として含まれるキーワード。  
  
-   データマイニング仕様の OLE DB で定義されているキーワードで、DMX ステートメントの一部として含まれています。  
  
 データベース内のオブジェクトに名前を付ける場合は、予約済みキーワードの使用を回避する名前付け規則を使用することをお勧めします。  
  
 データベースに予約されたキーワードと一致する名前が含まれている場合、これらのオブジェクトを参照するときに区切られた識別子を使用する必要があります。 詳細については、「 [DMX&#41;&#40;識別子 ](../dmx/identifiers-dmx.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [DMX&#41; リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-reference.md)   
 [DMX&#41; ステートメントリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-statements.md)   
 [DMX&#41; 構文表記規則を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [DMX&#41; の構文要素を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
  
