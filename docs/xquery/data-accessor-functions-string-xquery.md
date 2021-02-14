---
title: string 関数 (XQuery) |Microsoft Docs
description: 文字列として表現された引数の値を返す XQuery 関数文字列 () について説明します。
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- string function
- fn:string function
ms.assetid: 7baa2959-9340-429b-ad53-3df03d8e13fc
author: rothja
ms.author: jroth
ms.openlocfilehash: 9c334f2f78ae79b9a1af3a268728d6fcc5454f05
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100351083"
---
# <a name="data-accessor-functions---string-xquery"></a>データ アクセサー関数 - string (XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  文字列として表される *$arg* の値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:string() as xs:string  
fn:string($arg as item()?) as xs:string  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 ノードまたはアトミック値です。  
  
## <a name="remarks"></a>Remarks  
  
-   *$Arg* が空のシーケンスの場合は、長さ0の文字列が返されます。  
  
-   *$Arg* がノードの場合、関数は、文字列値アクセサーを使用して取得されたノードの文字列値を返します。 これは、W3C XQuery 1.0 および XPath 2.0 データモデル仕様で定義されています。  
  
-   *$Arg* がアトミック値である場合、この関数は、式によって返される文字列を **xs: string**, *$arg* として返します。ただし、特に指定がない場合は例外です。  
  
-   *$Arg* の型が **xs: anyURI** の場合、URI は特殊文字をエスケープせずに文字列に変換されます。  
  
-   この実装では、引数のない **fn: string ()** は、コンテキストに依存する述語のコンテキストでのみ使用できます。 具体的には、角かっこ ([]) 内でのみ使用できます。  
  
## <a name="examples"></a>使用例  
 このトピックでは、AdventureWorks データベースのさまざまな **xml** 型の列に格納されている xml インスタンスに対して XQuery の例を示します。  
  
### <a name="a-using-the-string-function"></a>A. String 関数の使用  
 次のクエリでは、 `Features` <> 要素の <> 子要素ノードが取得され `ProductDescription` ます。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
 /PD:ProductDescription/PD:Features  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 結果の一部を次に示します。  
  
```  
<PD:Features xmlns:PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   These are the product highlights.   
   <p1:Warranty xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 years</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
   </p1:Warranty>  
       ...  
</PD:Features>  
```  
  
 **String ()** 関数を指定すると、指定したノードの文字列値が返されます。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
 string(/PD:ProductDescription[1]/PD:Features[1])  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 次に結果の一部を示します。  
  
```  
These are the product highlights.   
3 yearsparts and labor...    
```  
  
### <a name="b-using-the-string-function-on-various-nodes"></a>B. さまざまなノードでの string 関数の使用  
 次の例では、XML インスタンスが xml 型の変数に割り当てられています。 クエリは、さまざまなノードに **文字列 ()** を適用した結果を示すために指定されます。  
  
```  
declare @x xml  
set @x = '<?xml version="1.0" encoding="UTF-8" ?>  
<!--  This is a comment -->  
<root>  
  <a>10</a>  
just text  
  <b attr="x">20</b>  
</root>  
'  
```  
  
 次のクエリでは、ドキュメントノードの文字列値を取得します。 この値は、そのすべての子孫のテキストノードの文字列値を連結することによって形成されます。  
  
```  
select @x.query('string(/)')  
```  
  
 結果を次に示します。  
  
```  
This is a comment 10  
just text  
 20  
```  
  
 次のクエリは、processing-instruction ノードの文字列値を取得します。 テキストノードが含まれていないため、結果は空のシーケンスになります。  
  
```  
select @x.query('string(/processing-instruction()[1])')  
```  
  
 次のクエリでは、コメントノードの文字列値を取得し、テキストノードを返します。  
  
```  
select @x.query('string(/comment()[1])')  
```  
  
 結果を次に示します。  
  
```  
This is a comment   
```  
  
## <a name="see-also"></a>参照  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
