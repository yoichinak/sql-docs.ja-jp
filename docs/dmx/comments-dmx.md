---
description: コメント (DMX)
title: コメント (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8069241656de868ae2165fa7348b549c8e3308e0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431124"
---
# <a name="comments-dmx"></a>コメント (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  データマイニング拡張機能 (DMX) のコメントは、 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 実行されないプログラムコード内のテキスト文字列です。 コメントは解説とも呼ばれています。 コメントを使用すると、コードの説明を記述したり、コードの診断の際に DMX ステートメントまたはスクリプトの一部分を一時的に無効化することができます。  
  
 コメントを使用してプログラムコードを記述すると、後でコードを簡単に管理できるようになります。 コメントを使用して、プログラムの名前、コードを作成した開発者の名前、および主なコード変更の日付などの詳細を記録することができます。 また、複雑な計算の説明やプログラム方法の説明を記述することもできます。  
  
 コメントを記述する際の基本的なガイドラインは次のとおりです。  
  
-   コメント内には、すべての英数字や記号を使用することができます。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、コメント内の文字はすべて無視されます。  
  
-   ステートメント内またはスクリプト内のコメント長には制限がありません。 1つまたは複数の行からコメントを作成できます。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、次の種類のコメント文字がサポートされています。  
  
-   **(二重スラッシュ)。** 実行するコードと同じ行にコメントを記述したり、コメント自体を行に記述したりするには、これらのコメント文字を使用します。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 二重スラッシュから行末までのすべてをコメントの一部として評価します。 複数行にわたってコメントを記述する場合、すべてのコメント行の先頭に二重スラッシュを使用します。 このコメント文字の詳細については、「 [DMX&#41;&#41; &#40;スラッシュ &#40;コメント ](../dmx/double-slash-comment-dmx.md)」を参照してください。  
  
-   **--(二重ハイフン)。** 実行するコードと同じ行にコメントを記述したり、コメント自体を行に記述したりするには、これらのコメント文字を使用します。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] コメントの一部として、二重ハイフンから行末までのすべてを評価します。 複数行にわたってコメントを記述する場合、すべてのコメント行の先頭に二重ハイフンを使用します。 このコメント文字の詳細については、「 [--&#40;コメント&#41; &#40;DMX&#41; の概要](../dmx/comment-dmx-summary.md)」を参照してください。  
  
-   **/\* ... \*/(スラッシュとアスタリスクの文字のペア)。** 実行コードと同じ行にコメントを記述する、コメント専用の行にコメントを記述する、または実行可能コード内にコメントを記述するには、このコメント文字を使用します。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] コメントの一部として、開いているコメントのペア (/*) から終了コメントのペア (/) までのすべてを評価し \* ます。 複数行のコメントを作成するには、コメントを開始コメント文字のペア (/) で開始し、コメント \* を終了コメント文字のペア (/) で終了し \* ます。 コメントの行に他のコメント文字を含めることはできません。 このコメント文字の詳細については、「 [DMX&#41;&#41; &#40;スラッシュ (Star) &#40;コメント ](../dmx/slash-star-comment-dmx.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [DMX&#41; リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-reference.md)   
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41; オペレーターリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [DMX&#41; ステートメントリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-statements.md)   
 [DMX&#41; 構文表記規則を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [DMX&#41; の構文要素を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)   
 [構造と DMX 予測クエリの使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
  
