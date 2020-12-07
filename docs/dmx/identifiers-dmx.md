---
description: 識別子 (DMX)
title: 識別子 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3a779e16b06b00cb925f28e8da34ce3959d7dc7e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88352888"
---
# <a name="identifiers-dmx"></a>識別子 (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  内のすべてのオブジェクトには [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 識別子が必要です。 オブジェクトの名前は識別子です。 サーバー、データベース、およびデータベースオブジェクト (データソース、データソースビュー、キューブ、ディメンション、マイニングモデルなど) には識別子があります。  
  
 データマイニング拡張機能 (DMX) には、次の2つの識別子のクラスがあります。  
  
-   [標準識別子](#RegularIdentifiers)  
  
-   [区切られた識別子](#DelimitedIdentifiers)  
  
 オブジェクト識別子は、オブジェクトを定義するときに作成されます。 次に、識別子を使用してオブジェクトを参照します。 識別子は100文字以下でなければなりません。  
  
##  <a name="regular-identifiers"></a><a name="RegularIdentifiers"></a> 標準識別子  
 DMX の標準識別子は、識別子の形式に関する [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] の規則に準拠しています。 DMX の標準識別子には区切り記号は必要ありません。 次に、通常の非区切られた識別子を使用する DMX ステートメントの例を示します。  
  
```  
SELECT * FROM Clustering.CONTENT;  
```  
  
### <a name="rules-for-regular-identifiers"></a>標準識別子に関する規則  
 標準識別子の形式に関する規則は、次のとおりです。  
  
1.  標準識別子の最初の文字は、次のうちのいずれかである必要があります。  
  
    -   Unicode 規格&#xA0;2.0 で定義されている文字。 これには、a ~ z、A ~ Z、および他の言語の文字文字が含まれます。  
  
    -   アンダースコア (_)。  
  
2.  後続の文字は次のようになります。  
  
    -   Unicode 規格&#xA0;2.0 で定義されている文字  
  
    -   Basic Latin スクリプトまたはその他の各国スクリプトの 10 進数  
  
    -   アンダースコア (_)。  
  
3.  DMX 予約語を識別子として使用することはできません。 予約語は、DMX では大文字と小文字が区別されません。 詳細については、「 [DMX&#41;&#40;の予約済みキーワード ](../dmx/reserved-keywords-dmx.md)」を参照してください。  
  
4.  識別子には、空白や特殊文字を埋め込むことはできません。  
  
 これらの規則に準拠していない識別子は、DMX ステートメントで使用するときに、角かっこで区切る必要があります。  
  
##  <a name="delimited-identifiers"></a><a name="DelimitedIdentifiers"></a> 区切られた識別子  
 区切られた識別子は、角かっこ ([]) で囲みます。  これらの規則に準拠した区切られた識別子を使用した DMX ステートメントの例は、次のとおりです。  
  
```  
SELECT * FROM [Marketing_Clusters].CONTENT;  
```  
  
 標準識別子の形式に関する規則に準拠していない識別子は、必ず区切り記号で区切る必要があります。 スペースを含んでいる区切られた識別子を使用した DMX ステートメントの例は、次のとおりです。  
  
```  
SELECT * FROM [Targeted Mailing].CONTENT;  
```  
  
 区切られた識別子は、次のような場合に使用します。  
  
-   予約語をオブジェクト名やオブジェクト名の一部に使用する場合。  
  
     予約されたキーワードをオブジェクト名として使用しないことをお勧めします。 以前のバージョンのからアップグレードしたデータベースには [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 、以前のバージョンので予約されていないものの、に予約されている単語を含む識別子が含まれる場合があり [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ます。 オブジェクトの名前を変更できるようにするには、区切られた識別子を使用して、このようなオブジェクトを参照します。  
  
-   修飾された識別子として示されていない文字を使用する場合。  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、現在のコード ページ内の文字はすべて区切られた識別子に使用することができますが、特殊文字を区別しないでオブジェクト名に使用すると、DMX ステートメントの読み取りおよびメンテナンスが難しくなる場合があります。  
  
### <a name="rules-for-delimited-identifiers"></a>区切られた識別子の規則  
 区切られた識別子の形式に関する規則は、次のとおりです。  
  
1.  区切られた識別子には、標準識別子と同じ文字数を含めることができます (区切り文字を含まない 1 ~ 100 文字)。  
  
2.  識別子の本体には、現在のコードページで使用されている文字の任意の組み合わせを含めることができます (区切り文字自体を含む)。 識別子の本体に区切り文字が含まれている場合は、特別な処理が必要です。  
  
    -   識別子の本体に左角かっこ ([) が含まれている場合は、追加の処理は必要ありません。  
  
    -   識別子の本体に右角かっこ (]) が含まれている場合は、コードページ内で表現するために2つの右角かっこ ([]]) を指定する必要があります。  
  
### <a name="delimiting-identifiers-with-multiple-parts"></a>複数の部分で識別子を区切る  
 修飾されたオブジェクト名を使用する場合、オブジェクト名を構成する識別子の1つ以上を区切る必要がある場合があります。 各識別子は個々に区切ってください。  
  
## <a name="see-also"></a>参照  
 [DMX&#41; リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-reference.md)   
 [DMX&#41; の構文要素を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41; オペレーターリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [DMX&#41; ステートメントリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-statements.md)   
 [DMX&#41; 構文表記規則を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)   
 [構造と DMX 予測クエリの使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
  
