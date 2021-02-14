---
title: data 関数 (XQuery) |Microsoft Docs
description: XQuery 関数の data () を使用して、指定した項目のシーケンス内の各項目に対して型指定された値を返す方法について説明します。
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
- fn:data function
- data function [XQuery]
ms.assetid: 511b5d7d-c679-4cb2-a3dd-170cc126f49d
author: rothja
ms.author: jroth
ms.openlocfilehash: 4e20c00d93082994cd5dc230bfe1b4356b3ed031
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100338507"
---
# <a name="data-accessor-functions---data-xquery"></a>データ アクセサー関数 - data (XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  *$Arg* によって指定された各項目の型指定された値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:data ($arg as item()*) as xdt:untypedAtomic*  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 型指定された値を返す対象となるアイテムのシーケンス。  
  
## <a name="remarks"></a>Remarks  
 型指定された値には、次のことが当てはまります。  
  
-   アトミック値の型指定された値はアトミック値です。  
  
-   テキスト ノードの型指定された値は、そのテキスト ノードの文字列値になります。  
  
-   コメントの型指定された値は、コメントの文字列値です。  
  
-   処理命令の型指定された値は、その処理命令の内容になります。このとき、処理命令の操作対象名は含まれません。  
  
-   ドキュメントノードの型指定された値は、その文字列値です。  
  
 属性ノードと要素ノードには、次のことが当てはまります。  
  
-   属性ノードが XML スキーマ型を使用して型指定されている場合、その型指定された値は、それに応じて型指定された値になります。  
  
-   属性ノードが型指定されていない場合、型指定された値は **xdt: untypedAtomic** のインスタンスとして返される文字列値と同じになります。  
  
-   要素ノードが型指定されていない場合、型指定された値は **xdt: untypedAtomic** のインスタンスとして返される文字列値と同じになります。  
  
 型指定された要素ノードには、次のものが適用されます。  
  
-   要素に単純コンテンツ型がある場合、 **data ()** は要素の型指定された値を返します。  
  
-   ノードが xs: anyType を含む複合型の場合、 **data ()** は静的エラーを返します。  
  
 次の例に示すように、 **data ()** 関数を使用することは、多くの場合、省略可能ですが、 **data ()** 関数を明示的に指定すると、クエリの読みやすさが向上します。 詳細については、「 [XQuery の基本](../xquery/xquery-basics.md)」を参照してください。  
  
 次に示すように、構築された XML で **データ ()** を指定することはできません。  
  
```  
declare @x xml  
set @x = ''  
select @x.query('data(<SomeNode>value</SomeNode>)')  
```  
  
## <a name="examples"></a>使用例  
 このトピックでは、AdventureWorks データベースのさまざまな **xml** 型の列に格納されている xml インスタンスに対して XQuery の例を示します。  
  
### <a name="a-using-the-data-xquery-function-to-extract-typed-value-of-a-node"></a>A. data() XQuery 関数によるノードの型指定された値の抽出  
 次のクエリは、 **data ()** 関数を使用して、属性、要素、およびテキストノードの値を取得する方法を示しています。  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query(N'  
 for $pd in //p1:ProductDescription  
 return   
    <Root   
      ProductID = "{ data( ($pd//@ProductModelID)[1] ) }"   
      Feature =   "{ data( ($pd/p1:Features/wm:Warranty/wm:Description)[1] ) }" >  
    </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 結果を次に示します。  
  
```  
<Root ProductID="19" Feature="parts and labor"/>  
```  
  
 前述のように、属性を構築する場合、 **data ()** 関数は省略可能です。 **Data ()** 関数を指定しなかった場合、暗黙的に想定されます。 次のクエリでは、前のクエリと同じ結果が生成されます。  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
      for $pd in //p1:ProductDescription  
         return   
          <Root    
                ProductID = "{ ($pd/@ProductModelID)[1] }"    
                Feature =   "{ ($pd/p1:Features/wm:Warranty/wm:Description)[1] }" >  
           </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 次の例は、 **data ()** 関数が必要なインスタンスを示しています。  
  
 次のクエリでは、 **$pd/p1: 仕様/マテリアル** が <`Material`> 要素を返します。 また、 **データ ($pd/p1: 仕様/マテリアル)** は、xdt: untypedAtomic として型指定された文字データを返し `Material` ます。これは、<> が型指定されていないためです。 入力が型指定されていない場合、 **data ()** の結果は **Xdt: untypedAtomic** として型指定されます。  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $pd in //p1:ProductDescription  
         return   
          <Root>  
             { $pd/p1:Specifications/Material }  
             { data($pd/p1:Specifications/Material) }  
           </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 結果を次に示します。  
  
```  
<Root>  
  <Material>Almuminum Alloy</Material>Almuminum Alloy  
</Root>  
```  
  
 次のクエリでは、 **データ ($pd/p1: Features/wm: 保証)** は静的なエラーを返し `Warranty` ます。これは <> が複合型の要素であるためです。  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
 <Root>  
   {     /p1:ProductDescription/p1:Features/wm:Warranty }  
   { data(/p1:ProductDescription/p1:Features/wm:Warranty) }  
 </Root>  
 ') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID = 23  
```  
  
## <a name="see-also"></a>参照  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
