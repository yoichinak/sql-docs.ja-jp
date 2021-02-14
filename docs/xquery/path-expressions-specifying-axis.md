---
title: パス式のステップで軸を指定する |Microsoft Docs
description: XQuery パス式で軸ステップを指定する方法について説明します。
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
- attribute axis [SQL Server]
- axis step [XQuery]
- descendant axis
- self axis
- path expressions [XQuery]
- child axis
- descendant-or-self axis
- parent axis
ms.assetid: c44fb843-0626-4496-bde0-52ca0bac0a9e
author: rothja
ms.author: jroth
ms.openlocfilehash: 2207dcce2787fb6f51668e777b01ce345d1f33ba
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100344659"
---
# <a name="path-expressions---specifying-axis"></a>パス式 - 軸の指定
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  パス式の軸ステップには、次のコンポーネントが含まれます。  
  
-   軸  
  
-   [ノードテスト](../xquery/path-expressions-specifying-node-test.md)  
  
-   [0個以上のステップ修飾子 (省略可能)](../xquery/path-expressions-specifying-predicates.md)  
  
 詳細については、「 [パス式 &#40;XQuery&#41;](../xquery/path-expressions-xquery.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の XQuery 実装では、次の軸ステップがサポートされています。  
  
|軸|[説明]|  
|----------|-----------------|  
|**子供**|コンテキストノードの子を返します。|  
|**descendant**|コンテキスト ノードのすべての子孫を返します。|  
|**parent**|コンテキスト ノードの親を返します。|  
|**attribute**|コンテキストノードの属性を返します。|  
|**自身**|コンテキスト ノード自身を返します。|  
|**descendant-or-self**|コンテキスト ノード自身とその子孫をすべて返します。|  
  
 これらのすべての軸 ( **親** 軸を除く) は、前方軸です。 **親** 軸は、ドキュメント階層内を後方に検索するので、逆軸です。 たとえば、相対パス式 `child::ProductDescription/child::Summary` には 2 つのステップがあり、各ステップが `child` 軸を指定します。 最初のステップでは、 \<ProductDescription> コンテキストノードの子要素を取得します。 2番目のステップでは、要素ノードごとに \<ProductDescription> \<Summary> 子要素ノードを取得します。  
  
 相対パス式では、 `child::root/child::Location/attribute::LocationID` 3 つのステップがあります。 最初の2つの手順では、それぞれ軸を指定し、3番目の手順で軸を指定し `child` `attribute` ます。 製品版の **ProductModel** テーブル内の製造手順の XML ドキュメントに対して実行した場合、式は `LocationID` \<Location> 要素の子要素ノードの属性を返し \<root> ます。  
  
## <a name="examples"></a>使用例  
 このトピックのクエリ例は、 **AdventureWorks** データベースの **xml** 型の列に対して指定されています。  
  
### <a name="a-specifying-a-child-axis"></a>A. 子軸の指定  
 次のクエリでは、特定の製品モデルについて、 \<Features> \<ProductDescription> テーブルに格納されている製品カタログの説明から要素ノードの子要素ノードを取得し `Production.ProductModel` ます。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  /child::PD:ProductDescription/child::PD:Features')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   `query()` **Xml** データ型のメソッドでは、パス式を指定します。  
  
-   パス式の両方のステップが、`child` 軸およびノード名 (`ProductDescription`、`Features`) をノード テストとして指定しています。 ノードテストの詳細については、「 [パス式のステップでのノードテストの指定](../xquery/path-expressions-specifying-node-test.md)」を参照してください。  
  
### <a name="b-specifying-descendant-and-descendant-or-self-axes"></a>B. descendant 軸と descendant-or-self 軸の指定  
 次の例では、子孫軸または子孫軸を使用します。 この例のクエリは、 **xml** 型の変数に対して指定されています。 XML インスタンスは、生成された結果の違いを簡単に示すために簡略化されています。  
  
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
declare @y xml  
set @y = @x.query('  
  /child::a/child::b  
')  
select @y  
```  
  
 次の結果では、式から `<b>` 要素ノードの `<a>` 子要素ノードが返されます。  
  
```  
<b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
</b>  
```  
  
 この式では、パス式の子孫軸を指定すると、  
  
 `/child::a/child::b/descendant::*`では、<> 要素ノードのすべての子孫を求めてい `b` ます。  
  
 ノードテストのアスタリスク (*) は、ノード名をノードテストとして表します。 したがって、子孫軸の主ノード型である element ノードは、返されるノードの種類を決定します。 つまり、式からすべての要素ノードが返されます。 テキストノードは返されません。 プライマリノードの種類とノードテストとの関係の詳細については、「 [パス式のステップでノードテストを指定する](../xquery/path-expressions-specifying-node-test.md) 」を参照してください。  
  
 次の結果に示すように、要素ノード <`c`> と <`d`> が返されます。  
  
```  
<c>text2  
     <d>text3</d>  
</c>  
<d>text3</d>  
```  
  
 子孫軸ではなく、子孫または自己の軸を指定すると、は `/child::a/child::b/descendant-or-self::*` コンテキストノード、要素 <`b`>、およびその子孫を返します。  
  
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
  
 **AdventureWorks** データベースに対する次のサンプルクエリでは、 `Features` <> 要素の <> 要素の子要素ノードがすべて取得され `ProductDescription` ます。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  /child::PD:ProductDescription/child::PD:Features/descendant::*  
')  
FROM  Production.ProductModel  
WHERE ProductModelID=19  
```  
  
### <a name="c-specifying-a-parent-axis"></a>C. parent 軸の指定  
 次のクエリでは、 `Summary` `ProductDescription` テーブルに格納されている製品カタログ XML ドキュメント内の <> 要素の <> 子要素が返され `Production.ProductModel` ます。  
  
 この例では、parent 軸を使用して <> 要素の親に戻り、 `Feature` `Summary` <> 要素の <> 要素の子を取得し `ProductDescription` ます。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  
/child::PD:ProductDescription/child::PD:Features/parent::PD:ProductDescription/child::PD:Summary  
')  
FROM   Production.ProductModel  
WHERE  ProductModelID=19  
  
```  
  
 このクエリ例では、パス式で `parent` 軸が使用されています。 次に示すように、この式を parent 軸を使用せずに書き直すこともできます。  
  
```  
/child::PD:ProductDescription[child::PD:Features]/child::PD:Summary  
```  
  
 次の例では、parent 軸の便利な例を示しています。  
  
 **Productmodel** テーブルの **catalogdescription** 列に格納されている各製品モデルカタログの説明には、 `<ProductDescription>` 次の `ProductModelID` フラグメントに示すように、属性と子要素を持つ要素があり `<Features>` ます。  
  
```  
<ProductDescription ProductModelID="..." >  
  ...  
  <Features>  
    <Feature1>...</Feature1>  
    <Feature2>...</Feature2>  
   ...  
</ProductDescription>  
```  
  
 このクエリでは、 `$f` 要素の子要素を返すために、FLWOR ステートメントで反復子変数を設定し `<Features>` ます。 詳細については、「 [FLWOR Statement And Iteration &#40;XQuery&#41;](../xquery/flwor-statement-and-iteration-xquery.md)」を参照してください。 各機能について、 `return` 句は次の形式で XML を構築します。  
  
```  
<Feature ProductModelID="...">...</Feature>  
<Feature ProductModelID="...">...</Feature>  
```  
  
 `ProductModelID`各> 要素のを追加するには、軸を指定し `<Feature` `parent` ます。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
  for $f in /child::PD:ProductDescription/child::PD:Features/child::*  
  return  
   <Feature  
     ProductModelID="{ ($f/parent::PD:Features/parent::PD:ProductDescription/attribute::ProductModelID)[1]}" >  
          { $f }  
   </Feature>  
')  
FROM  Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 結果の一部を次に示します。  
  
```  
<Feature ProductModelID="19">  
  <wm:Warranty   
   xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
    <wm:Description>parts and labor</wm:Description>  
  </wm:Warranty>  
</Feature>  
<Feature ProductModelID="19">  
  <wm:Maintenance   
   xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <wm:NoOfYears>10 years</wm:NoOfYears>  
    <wm:Description>maintenance contract available through your dealer   
                  or any AdventureWorks retail store.</wm:Description>  
  </wm:Maintenance>  
</Feature>  
<Feature ProductModelID="19">  
  <p1:wheel   
   xmlns:p1="https://www.adventure-works.com/schemas/OtherFeatures">  
      High performance wheels.  
  </p1:wheel>  
</Feature>  
```  
  
 `[1]`シングルトン値が返されるように、パス式の述語が追加されていることに注意してください。  
  
  
