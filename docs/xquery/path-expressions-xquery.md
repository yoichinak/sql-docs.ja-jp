---
title: パス式 (XQuery) |Microsoft Docs
description: XQuery パス式で、ドキュメント内の要素、属性、テキストノードなどのノードを検索する方法について説明します。
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- axis step [XQuery]
- path expressions [XQuery]
- expressions [XQuery], path
ms.assetid: b93fa36c-bf69-46b9-b137-f597d66fd0c0
author: rothja
ms.author: jroth
ms.openlocfilehash: 6d69a916d19c519e1b313a7244a6a07feba36a67
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100339992"
---
# <a name="path-expressions-xquery"></a>パス式 (XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  XQuery パス式は、ドキュメント内の要素、属性、テキストノードなどのノードを検索します。 パス式の結果は常に、結果シーケンス内でノードが重複することなく、ドキュメント順で生成されます。 パスを指定する場合は、省略形または省略構文を使用できます。 以下の説明では、主に省略しない構文を取り上げます。 省略された構文については、このトピックの後半で説明します。  
  
> [!NOTE]  
>  このトピックのサンプルクエリは、 **xml** 型の列に対して指定されているので、 **Catalogdescription** と **手順**、 **productmodel** テーブルでは、これらの列に格納されている xml ドキュメントの内容と構造を理解しておく必要があります。  
  
 パス式には、相対パスまたは絶対パスを指定できます。 これらの両方の説明を次に示します。  
  
-   相対パス式は、1つまたは2つのスラッシュ記号 (/または//) で区切られた1つ以上のステップで構成されます。 たとえば、 `child::Features` は、 `Child` コンテキストノードの子ノードのみを参照する相対パス式です。 これは現在処理中のノードです。 式は、 \<Features> コンテキストノードの子要素ノードを取得します。  
  
-   絶対パス式は、1つまたは2つのスラッシュ記号 (/または//) で始まり、その後に省略可能な相対パスが続きます。 たとえば、式 `/child::ProductDescription` の先頭のスラッシュ記号は、この式が絶対パス式であることを示しています。 式の先頭のスラッシュ記号は、コンテキストノードのドキュメントルートノードを返します。そのため、式は、 \<ProductDescription> ドキュメントルートの子要素ノードをすべて返します。  
  
     絶対パスが1つのスラッシュ記号で始まる場合は、相対パスの後に指定することもできます。 スラッシュ記号を1つだけ指定した場合、式はコンテキストノードのルートノードを返します。 XML データ型の場合、これはドキュメント ノードになります。  
  
 パス式は、通常、ステップで構成されます。 たとえば、絶対パス式には、 `/child::ProductDescription/child::Summary` スラッシュ記号で区切られた2つのステップが含まれています。  
  
-   最初のステップでは、 \<ProductDescription> ドキュメントルートの子要素ノードを取得します。  
  
-   2番目のステップでは、取得した \<Summary> 各要素ノードの子要素ノードが取得され、そのノードが \<ProductDescription> コンテキストノードになります。  
  
 パス式のステップは、軸ステップまたは一般的なステップにすることができます。  
  
## <a name="axis-step"></a>軸ステップ  
 パス式の軸ステップには、次の部分があります。  
  
 [軸](../xquery/path-expressions-specifying-axis.md)  
 移動の方向を定義します。 コンテキストノードから開始し、軸によって指定された方向に到達可能なノードに移動するパス式の軸ステップ。  
  
 [ノードテスト](../xquery/path-expressions-specifying-node-test.md)  
 選択するノードの型またはノード名を指定します。  
  
 0個以上のオプションの述語  
 一部を選択し、他のノードを破棄してノードをフィルター処理します。  
  
 次の例では、パス式で **軸手順** を使用します。  
  
-   絶対パス式では、 `/child::ProductDescription` 1 つのステップだけが含まれます。 これは、軸 (`child`) とノード テスト (`ProductDescription`) を指定しています。  
  
-   相対パス式 `child::ProductDescription/child::Features` には、1 つのスラッシュ記号で区切られた 2 つのステップがあります。 どちらの手順でも、子軸を指定します。 ProductDescription と Features はノードテストです。  
  
-   相対パス式には、 `child::root/child::Location[attribute::LocationID=10]` スラッシュ記号で区切られた2つのステップが含まれています。 最初のステップでは、軸 ( `child` ) とノードテスト () を指定し `root` ます。 2 番目のステップは、軸ステップの 3 種類のコンポーネントをすべて指定しています。つまり、軸 (child)、ノード テスト (`Location`)、および述語 (`[attribute::LocationID=10]`) です。  
  
 軸ステップのコンポーネントの詳細については、「 [パス式のステップでの軸の指定](../xquery/path-expressions-specifying-axis.md)」、「 [パス式のステップでのノードテストの指定](../xquery/path-expressions-specifying-node-test.md)」、および「 [パス式のステップで述語を指定する](../xquery/path-expressions-specifying-predicates.md)」を参照してください。  
  
## <a name="general-step"></a>一般的な手順  
 汎用ステップは、評価結果がノードのシーケンスになる必要のある式です。  
  
 SQL Server の XQuery 実装では、パス式の最初のステップとして一般的な手順がサポートされています。 一般的な手順を使用するパス式の例を次に示します。  
  
```  
(/a, /b)/c  
id(/a/b)  
```  
  
 Id 関数の詳細については、「 [Id 関数 &#40;XQuery&#41;](../xquery/functions-on-sequences-id.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [パス式のステップでの軸の指定](../xquery/path-expressions-specifying-axis.md)  
 パス式での軸ステップの使用について説明します。  
  
 [パス式のステップでのノードテストの指定](../xquery/path-expressions-specifying-node-test.md)  
 パス式でのノードテストの使用について説明します。  
  
 [パス式のステップでの述語の指定](../xquery/path-expressions-specifying-predicates.md)  
 パス式での述語の使用について説明します。  
  
 [パス式での省略構文の使用](../xquery/path-expressions-using-abbreviated-syntax.md)  
 パス式での省略構文の使い方について説明します。  
  
  
