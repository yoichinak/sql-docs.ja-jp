---
description: データマイニング拡張機能 (DMX) の構文表記規則
title: データマイニング拡張機能 (DMX) 構文規則 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 06f6b96a09cdf676d48b29253256b22615f50dcf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491546"
---
# <a name="data-mining-extensions-dmx-syntax-conventions"></a>データマイニング拡張機能 (DMX) の構文表記規則
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  のデータマイニング拡張機能 (dmx) のリファレンスドキュメントでは、 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] dmx 言語を説明するために次の規則を使用します。  
  
|表記|使用法|  
|----------------|-----------|  
|**太字**|表示されたとおりに正確に入力する必要がある DMX キーワードとテキスト。|  
|*斜体*|ユーザーが指定する DMX 構文の引数を示します。|  
|&#124; (垂直線)|角かっこまたは中かっこで囲まれた構文項目を区切るために使用します。 選択できる項目は 1 つだけです。|  
|`[ ]` (角かっこ)|省略可能な構文項目が含まれています。 角かっこは入力しません。|  
|{} (中かっこ)|必須の構文項目が含まれています。 中かっこは入力しないでください。|  
|, ...|コンマの前の項目を任意の回数繰り返すことを示します。 項目はコンマで区切られます。|  
|\<label> ::=|構文のブロックの名前を示します。 この表記規則は、1 つのステートメント内の複数の箇所で使用できる長い構文の一部、または構文の 1 単位について、グループ化してラベルを付ける際に使用します。 構文のブロックを使用できる場所は、など、山かっこで囲まれたラベルで示され \<label> ます。|  
  
## <a name="see-also"></a>参照  
 [データ マイニング拡張機能 &#40;DMX&#41; リファレンス](../dmx/data-mining-extensions-dmx-reference.md)  
  
  

