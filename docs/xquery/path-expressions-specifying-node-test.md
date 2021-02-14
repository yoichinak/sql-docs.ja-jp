---
title: パス式のステップでノードテストを指定する |Microsoft Docs
description: XQuery パス式の軸ステップでノードテストを指定する方法について説明します。
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
- node test [XQuery]
ms.assetid: ffe27a4c-fdf3-4c66-94f1-7e955a36cadd
author: rothja
ms.author: jroth
ms.openlocfilehash: 578d10bc078edf886eb7980c3b7a099c99ef59a5
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100338543"
---
# <a name="path-expressions---specifying-node-test"></a>パス式 - ノード テストの指定
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  パス式の軸ステップには、次のコンポーネントが含まれます。  
  
-   [軸](../xquery/path-expressions-specifying-axis.md)  
  
-   ノードテスト  
  
-   [0個以上のステップ修飾子 (省略可能)](../xquery/path-expressions-specifying-predicates.md)  
  
 詳細については、「 [パス式 &#40;XQuery&#41;](../xquery/path-expressions-xquery.md)」を参照してください。  
  
 ノードテストは条件であり、パス式の軸ステップの2番目のコンポーネントです。 ステップによって選択されたすべてのノードは、この条件を満たしている必要があります。 パス式 `/child::ProductDescription` の場合、ノード テストは `ProductDescription` です。 この手順では、名前が ProductDescription である要素ノードの子のみを取得します。  
  
 ノード テストの条件には、次の情報を含めることができます。  
  
-   ノード名。 指定した名前を持つ、主ノード種別に属するノードのみが返されます。  
  
-   ノード型。 指定された種類のノードのみが返されます。  
  
> [!NOTE]  
>  XQuery パス式に指定されているノード名は、Transact-sql クエリの場合と同じ照合順序に依存しないルールの対象にならず、常に大文字と小文字が区別されます。  
  
## <a name="node-name-as-node-test"></a>ノード テストとしてのノード名  
 パス式のステップでノード名をノード テストとして指定する場合は、主ノード種別の概念を理解しておく必要があります。 すべての軸、子、親、または属性には、プリンシパルノードの種類があります。 次に例を示します。  
  
-   attribute 軸には、属性のみを含めることができます。 したがって、属性ノードが attribute 軸の主ノード種別になります。  
  
-   その他の軸の場合、軸で選択されるノードに要素ノードを含めることができる場合は、要素がその軸の主ノード種別になります。  
  
 ノード名をノード テストとして指定すると、ステップから次の型のノードが返されます。  
  
-   軸の主ノード種別であるノード。  
  
-   ノード テストに指定したのと同じ名前のノード。  
  
 たとえば、次のパス式について考えてみます。  
  
```  
child::ProductDescription   
```  
  
 この 1 ステップの式では、`child` 軸とそのノード名 `ProductDescription` をノード テストとして指定しています。 この式は、子軸の主ノード種別である要素ノードだけを返し、ProductDescription を名前として持つノードのみを返します。  
  
 パス式に `/child::PD:ProductDescription/child::PD:Features/descendant::*,` は3つのステップがあります。 これらのステップでは、child 軸と descendant 軸を指定しています。 各ステップでは、ノード名がノードテストとして指定されています。 3番目のステップのワイルドカード文字 () は、 `*` 子孫軸の主要ノード種別のすべてのノードを示します。 軸の主ノード種別によって選択されるノードの種類が決まり、ノード名によって選択されたノードのフィルターが決まります。  
  
 結果として、この式を **Productmodel** テーブルの製品カタログ XML ドキュメントに対して実行すると、その要素の子である要素ノードの子要素ノードがすべて取得され \<Features> \<ProductDescription> ます。  
  
 パス式は、次 `/child::PD:ProductDescription/attribute::ProductModelID` の2つの手順で構成されます。 どちらのステップでも、ノード名をノード テストとして指定しています。 また、2番目の手順では、属性軸を使用します。 したがって、各ステップでは、ノードテストとして指定された名前を持つ、その軸の主ノード種別のノードが選択されます。 このため、式は要素ノードの **Productmodelid** 属性ノードを返し \<ProductDescription> ます。  
  
 ノードテストにノード名を指定する場合は、次の例に示すように、ワイルドカード文字 (*) を使用してノードのローカル名または名前空間プレフィックスを指定することもできます。  
  
```  
declare @x xml  
set @x = '  
<greeting xmlns="ns1">  
   <salutation>hello</salutation>  
</greeting>  
<greeting xmlns="ns2">  
   <salutation>welcome</salutation>  
</greeting>  
<farewell xmlns="ns1" />'  
select @x.query('//*:greeting')  
select @x.query('declare namespace ns="ns1"; /ns:*')  
```  
  
## <a name="node-type-as-node-test"></a>ノード テストとしてのノード型  
 要素ノード以外のノード型を照会するには、ノード型のテストを使用します。 次の表に示すように、4つのノードタイプのテストを使用できます。  
  
|ノード型|戻り値|例|  
|---------------|-------------|-------------|  
|`comment()`|コメント ノードの場合 True です。|`following::comment()` コンテキストノードの後に表示されるすべてのコメントノードを選択します。|  
|`node()`|任意の種類のノードの場合は True。|`preceding::node()` コンテキストノードの前に表示されるすべてのノードを選択します。|  
|`processing-instruction()`|処理命令ノードの場合 True です。|`self::processing instruction()` コンテキストノード内のすべての処理命令ノードを選択します。|  
|`text()`|テキスト ノードの場合は True を返します。|`child::text()` コンテキストノードの子であるテキストノードを選択します。|  
  
 text() や comment() などのノード型がノード テストに指定された場合は、軸の主ノード種別にかかわらず、ステップでは指定された種類のノードが返されます。 たとえば、次のパス式は、コンテキストノードの子のコメントノードのみを返します。  
  
```  
child::comment()  
```  
  
 同様に、は、 `/child::ProductDescription/child::Features/child::comment()` \<Features> 要素ノードの子要素ノードの子のコメントノードを取得し \<ProductDescription> ます。  
  
## <a name="examples"></a>使用例  
 次の例では、ノード名とノードの種類を比較します。  
  
### <a name="a-results-of-specifying-the-node-name-and-the-node-type-as-node-tests-in-a-path-expression"></a>A. ノード名とノード型をノードテストとしてパス式に指定した結果  
 次の例では、単純な XML ドキュメントが **xml** 型の変数に割り当てられています。 別のパス式を使用してドキュメントを照会します。 その後、結果が比較されます。  
  
```  
declare @x xml  
set @x='  
<a>  
 <b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
 </b>  
</a>'  
select @x.query('  
/child::a/child::b/descendant::*  
')  
```  
  
 この式では、`<b>` 要素ノードの子孫にあたる要素ノードが要求されます。  
  
 ノード テストのアスタリスク (`*`) は、ノード名のワイルドカード文字を示しています。 descendant 軸の主ノード種別は要素ノードです。 このため、式は要素ノードのすべての子孫要素ノードを返し `<b>` ます。 つまり、次の結果に示すように、要素ノード `<c>` と `<d>` が返されます。  
  
```  
<c>text2  
     <d>text3</d>  
</c>  
<d>text3</d>  
```  
  
 次のように、descendant 軸ではなく descendent-or-self 軸を指定すると、コンテキスト ノードとその子孫が返されます。  
  
```  
/child::a/child::b/descendant-or-self::*  
```  
  
 この式は、要素ノード `<b>` とその子孫にあたる要素ノードを返します。 子孫ノードを返すと、子孫または自己の軸のプライマリノードの種類である element ノード型によって、返されるノードの種類が決まります。  
  
 結果を次に示します。  
  
```  
<b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
</b>  
  
<c>text2  
     <d>text3</d>  
</c>  
  
<d>text3</d>   
```  
  
 前の式では、ワイルドカード文字がノード名として使用されていました。 代わりに、次の式に示すように `node()` 関数を使用できます。  
  
```  
/child::a/child::b/descendant::node()  
```  
  
 はノード型であるため、 `node()` 子孫軸のすべてのノードを受け取ります。 結果を次に示します。  
  
```  
text1  
<c>text2  
     <d>text3</d>  
</c>  
text2  
<d>text3</d>  
text3  
```  
  
 さらに、descendant-or-self 軸と `node()` をノード テストに指定した場合は、すべての子孫、要素、テキスト ノード、およびコンテキスト ノードである `<b>` 要素が返されます。  
  
```  
<b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
</b>  
text1  
<c>text2  
     <d>text3</d>  
</c>  
text2  
<d>text3</d>  
text3  
```  
  
### <a name="b-specifying-a-node-name-in-the-node-test"></a>B. ノードテストでのノード名の指定  
 次の例では、すべてのパス式でノード名をノード テストとして指定します。 結果として、すべての式により、ノード テストに指定したノード名を持つ、軸の主ノード種別に属するノードが返されます。  
  
 次のクエリ式は、 `Warranty` テーブルに格納されている製品カタログ XML ドキュメントから <> 要素を返し `Production.ProductModel` ます。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::wm:Warranty  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   XQuery プロローグ内の `namespace` キーワードにより、クエリ本文で使用するプレフィックスが定義されています。 XQuery プロローグの詳細については、「 [Xquery プロローグ](../xquery/modules-and-prologs-xquery-prolog.md) 」を参照してください。  
  
-   パス式の3つの手順はすべて、子軸とノード名をノードテストとして指定します。  
  
-   軸ステップの省略可能なステップ修飾子の部分は、式のどのステップでも指定されていません。  
  
 このクエリでは、 `Warranty` `Features` <> 要素の <> 要素の子の <> 子要素が返され `ProductDescription` ます。  
  
 結果を次に示します。  
  
```  
<wm:Warranty xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
  <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
  <wm:Description>parts and labor</wm:Description>  
</wm:Warranty>     
```  
  
 次のクエリでは、パス式によって、ノードテストでワイルドカード文字 () が指定されて `*` います。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::*  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 ノード名にはワイルドカード文字が指定されています。 このクエリでは、 `Features` <> 要素ノードの子である <> 要素ノードの子要素ノードがすべて返され `ProductDescription` ます。  
  
 次のクエリは、ワイルドカード文字と共に名前空間が指定されている点を除けば、前のクエリと同じです。 結果として、その名前空間に含まれるすべての子要素ノードが返されます。 <> 要素には、 `Features` 異なる名前空間の要素を含めることができることに注意してください。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::wm:*  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 次のクエリに示すように、ワイルドカード文字を名前空間プレフィックスとして使用できます。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::*:Maintenance  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 このクエリは、 `Maintenance` 製品カタログの XML ドキュメントのすべての名前空間にある、<> 要素ノードの子を返します。  
  
### <a name="c-specifying-node-kind-in-the-node-test"></a>C. ノードテストでのノードの種類の指定  
 次の例では、すべてのパス式でノードの種類をノード テストとして指定します。 結果として、すべての式がノード テストに指定した種類のノードを返します。  
  
 次のクエリでは、パス式で、3番目の手順でノードの種類を指定しています。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::text()  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 次のクエリでは、次のものが指定されています。  
  
-   パス式には、スラッシュ (`/`) で区切られた 3 つのステップがあります。  
  
-   これらの各手順では、子軸を指定します。  
  
-   最初の2つの手順ではノード名をノードテストとして指定し、3番目のステップではノードの種類をノードテストとして指定します。  
  
-   式は、 `Features` <> 要素ノードの <> 要素の子であるテキストノードを返し `ProductDescription` ます。  
  
 1つのテキストノードのみが返されます。 結果を次に示します。  
  
```  
These are the product highlights.   
```  
  
 次のクエリでは、<> 要素の子のコメントノードが返され `ProductDescription` ます。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::comment()  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   2番目のステップでは、ノードの種類をノードテストとして指定します。  
  
-   その結果、式は、<> 要素ノードの子のコメントノードを返し `ProductDescription` ます。  
  
 結果を次に示します。  
  
```  
<!-- add one or more of these elements... one for each specific product in this product model -->  
<!-- add any tags in <specifications> -->      
```  
  
 次のクエリでは、最上位レベルの処理命令ノードが取得されます。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::processing-instruction()  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 結果を次に示します。  
  
```  
<?xml-stylesheet href="ProductDescription.xsl" type="text/xsl"?>   
```  
  
 ノードテストには、文字列リテラルパラメーターを渡すことができ `processing-instruction()` ます。 この場合、クエリは、引数に指定された文字列リテラルを name 属性値として持つ処理命令を返します。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::processing-instruction("xml-stylesheet")  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
## <a name="implementation-limitations"></a>実装の制限事項  
 次に、特定の制限事項を示します。  
  
-   拡張された SequenceType ノードテストはサポートされていません。  
  
-   処理命令 (名前) はサポートされていません。 name は引用符で囲む必要があります。  
  
  
