---
title: 名前空間 uri 関数 (XQuery) |Microsoft Docs
description: XQuery で名前空間 uri 関数を使用して、指定した QName の名前空間 URI を返す方法について説明します。
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:namespace-uri function
- namespace-uri function
ms.assetid: 9b48d216-26c8-431d-9ab4-20ab187917f4
author: rothja
ms.author: jroth
ms.openlocfilehash: ed19a835b6df605a6ec735a8063a192ea32148fd
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92034835"
---
# <a name="functions-on-nodes---namespace-uri"></a>ノードの関数 - namespace-uri
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  *$Arg*で指定された QName の名前空間 URI を xs: string として返します。  
  
## <a name="syntax"></a>構文  
  
```  
fn:namespace-uri() as xs:string  
fn:namespace-uri($arg as node()?) as xs:string  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 名前空間 URI 部分が取得されるノードの名前。  
  
## <a name="remarks"></a>解説  
  
-   引数が省略された場合、既定値はコンテキスト ノードです。  
  
-   SQL Server では、引数のない **fn: namespace-uri ()** は、コンテキストに依存する述語のコンテキストでのみ使用できます。 具体的には、角かっこ ([]) 内でのみ使用できます。  
  
-   *$Arg*が空のシーケンスの場合は、長さ0の文字列が返されます。  
  
-   *$Arg*が、名前空間に含まれていない展開 QName を持つ要素ノードまたは属性ノードの場合、関数は長さ0の文字列を返します。  
  
## <a name="examples"></a>例  
 このトピックでは、AdventureWorks データベースのさまざまな **xml** 型の列に格納されている xml インスタンスに対して XQuery の例を示します。  
  
### <a name="a-retrieve-namespace-uri-of-a-specific-node"></a>A. 特定のノードの名前空間 URI を取得する  
 次のクエリは、型指定されていない XML インスタンスに対して指定されています。 クエリ式 `namespace-uri(/ROOT[1])` によって、指定されたのノードの名前空間 URI 部分が取得されます。  
  
```  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('namespace-uri(/ROOT[1])')  
```  
  
 指定された QName には名前空間 URI 部分はなく、ローカル名部分のみが含まれているため、結果は長さ0の文字列になります。  
  
 次のクエリは、型指定された **xml** 列に対して指定されています。 式は、 `namespace-uri(/AWMI:root[1]/AWMI:Location[1])` <> 要素の最初の <> 子要素の名前空間 URI を返し `Location` `root` ます。  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     namespace-uri(/AWMI:root[1]/AWMI:Location[1])') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 結果を次に示します。  
  
```  
https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions  
```  
  
### <a name="b-using-namespace-uri-without-argument-in-a-predicate"></a>B. 述語で引数を指定せずに namespace-uri() を使用する  
 次のクエリは、CatalogDescription 型指定された xml 列に対して指定されています。 この式は、名前空間 URI がであるすべての要素ノードを返し `https://www.adventure-works.com/schemas/OtherFeatures` ます。 名前空間**uri ()** 関数は、引数なしで指定され、コンテキストノードを使用します。  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
   /p1:ProductDescription//*[namespace-uri() = "https://www.adventure-works.com/schemas/OtherFeatures"]  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 結果の一部を次に示します。  
  
```  
<p1:wheel xmlns:p1="https://www.adventure-works.com/schemas/OtherFeatures">High performance wheels.</p1:wheel>  
<p2:saddle xmlns:p2="https://www.adventure-works.com/schemas/OtherFeatures">  
  <p3:i xmlns:p3="http://www.w3.org/1999/xhtml">Anatomic design</p3:i> and made from durable leather for a full-day of riding in comfort.</p2:saddle>  
...  
```  
  
 上のクエリの名前空間 URI は `https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain` に変更できます。 次に、展開された `ProductDescription` QName の名前空間 URI 部分がである <> 要素の子要素ノードをすべて受け取り `https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain` ます。  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 制限事項は次のとおりです。  
  
-   **名前空間 uri ()** 関数は、Xs: anyURI の代わりに xs: string 型のインスタンスを返します。  
  
## <a name="see-also"></a>参照  
 [ノードの関数](./xquery-functions-against-the-xml-data-type.md)   
 [ローカル名関数 &#40;XQuery&#41;](../xquery/functions-on-nodes-local-name.md)  
  
