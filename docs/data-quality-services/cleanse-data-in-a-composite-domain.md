---
description: 複合ドメインでのデータのクレンジング
title: 複合ドメインでのデータのクレンジング
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 7d1076e0-7710-469a-9107-e293e4bd80ac
author: swinarko
ms.author: sawinark
ms.openlocfilehash: f35430d590be36bb7ae487d32a9a0fc97c0275ce
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449950"
---
# <a name="cleanse-data-in-a-composite-domain"></a>複合ドメインでのデータのクレンジング

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  このトピックでは、 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) での複合ドメインのクレンジングについて説明します。 複合ドメインは 2 つ以上の単一ドメインで構成され、複数の関連用語で構成されるデータ フィールドにマップされます。 複合ドメイン内の個々のドメインには、ナレッジの共通領域が必要です。 複合ドメインの詳細については、「 [Managing a Composite Domain](../data-quality-services/managing-a-composite-domain.md)」を参照してください。  
  
##  <a name="mapping-a-composite-domain-to-the-source-data"></a><a name="Mapping"></a> ソース データへの複合ドメインのマッピング  
 複合ドメインにソース データをマップするには、次の 2 つの方法があります。  
  
-   ソース データを単一フィールド ("完全名") として、複合ドメインにマップします。  
  
    -   複合ドメインを参照データ サービスにマップすると、ソース データはそのまま参照データ サービスに送信されて修正および解析されます。  
  
    -   複合ドメインを参照データ サービスにマップしない場合、複合ドメインに定義されている解析方法に基づいて解析されます。 複合ドメインの解析方法の指定方法については、「 [Create a Composite Domain](../data-quality-services/create-a-composite-domain.md)」を参照してください。  
  
-   ソース データを複数のフィールド ("名"、"ミドル ネーム"、"姓") で構成し、複合ドメイン内の個々のドメインにマップします。  
  
 複合ドメインをソース データにマップする方法の例については、「[参照データへのドメインまたは複合ドメインのアタッチ](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)」をご覧ください。  
  
##  <a name="data-correction-using-definitive-cross-domain-rules"></a><a name="CDCorrection"></a> 明確なクロス ドメイン ルールを使用したデータの修正  
 複合ドメインのクロス ドメイン ルールを使用して、複合ドメイン内の個々のドメインの間のリレーションシップを示すルールを作成できます。 複合ドメインを含むソース データでクレンジング アクティビティを実行するときに、クロス ドメイン ルールが考慮されます。 明確な *Then* クロス ドメイン ルールの **"値が次の値と等しい"** では、単にクロス ドメイン ルールの有効性について知らせるだけでなく、データ クレンジング アクティビティ中にデータの修正も行います。  
  
 次の例を考えてみます。ProductName、CompanyName、および ProductVersion の 3 つの個別ドメインを含む複合ドメイン Product があります。 次の明確なクロス ドメイン ルールを作成します。  
  
 ドメイン 'CompanyName' 値に *Microsoft* が含まれ、ドメイン 'ProductName' 値が *Office* で 'ProductVersion' 値が *2010* の場合、ドメイン 'ProductName' 値は *Microsoft Office 2010* になる。  
  
 このクロス ドメイン ルールを実行すると、クレンジング アクティビティの後にソース データ (ProductName) が次のように修正されます。  
  
 **ソースデータ**  
  
|ProductName|CompanyName|ProductVersion|  
|-----------------|-----------------|--------------------|  
|Office|Microsoft Inc.|2010|  
  
 **出力データ**  
  
|ProductName|CompanyName|ProductVersion|  
|-----------------|-----------------|--------------------|  
|Microsoft Office 2010|Microsoft Inc.|2010|  
  
 明確な *Then* クロス ドメイン ルール **"値が次の値と等しい"** をテストするときは、 **[複合ドメイン ルールのテスト]** ダイアログ ボックスに、正しいデータを示す新しい列 **[次に修正]** が含まれます。 クレンジングデータ品質プロジェクトでは、この明確なクロスドメインルールによってデータが100% の信頼度で変更され、[ **理由** ] 列に "ルール ' ' によって修正されました" というメッセージが表示されます *\<Cross-Domain Rule Name>* 。 クロス ドメイン ルールの詳細については、「 [Create a Cross-Domain Rule](../data-quality-services/create-a-cross-domain-rule.md)」を参照してください。  
  
> [!NOTE]  
>  明確なクロス ドメイン ルールは、参照データ サービスにアタッチされている複合ドメインでは動作しません。  
  
##  <a name="data-profiling-for-composite-domains"></a><a name="DataProfiling"></a> 複合ドメインのデータ プロファイル  
 DQS プロファイルでは、クレンジング アクティビティ中に、 *完全性* (データがどの程度存在するか) と *正確性* (データがどの程度意図されたとおりに使用できるか) の 2 つのデータ品質ディメンションを提供します。 複合ドメインでは、プロファイリングから得られる完全性の統計情報を必ずしも信頼できません。 完全性の統計情報が必要な場合は、複合ドメインの代わりに単一ドメインを使用します。 複合ドメインを使用する必要がある場合は、プロファイリング用に単一ドメインのナレッジ ベースを作成して完全性を確認し、クレンジング アクティビティ用に複合ドメインのドメインを別途作成します。 たとえば、複合ドメインを使用したプロファイリングで住所レコードの完全性が 95% と示されたとしても、それよりはるかに不完全な列 (郵便番号の列など) がレコードに含まれている可能性があります。 この例では、単一ドメインを使用して郵便番号の列の完全性を測定することができます。  
  
 精度は複数の列でまとめて測定できるため、プロファイリングから得られる複合ドメインの精度の統計情報は信頼できます。 このデータの値は合成集約に含まれるため、複合ドメインで精度を測定できます。  
  
 クレンジング アクティビティの間のデータ プロファイリングについて詳しくは、「[DQS &#40;内部&#41; ナレッジを使用したデータのクレンジング](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)」の「[プロファイラーの統計情報](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Profiler)」をご覧ください。  
  
  
