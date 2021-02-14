---
title: XQuery での名前空間の処理 |Microsoft Docs
description: 新しい名前空間と既定の名前空間を宣言する方法を含む、XQuery での名前空間の処理例を示します。
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- declaring namespaces
- namespaces [XQuery]
- XQuery, namespaces
ms.assetid: 542b63da-4d3d-4ad5-acea-f577730688f1
author: rothja
ms.author: jroth
ms.openlocfilehash: acb1595ca2e7032d0363df3a1dd81740b7bcbf2d
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100341883"
---
# <a name="handling-namespaces-in-xquery"></a>XQuery での名前空間の処理
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  このトピックでは、クエリで名前空間を処理するためのサンプルを提供します。  
  
## <a name="examples"></a>例  
  
### <a name="a-declaring-a-namespace"></a>A. 名前空間の宣言  
 次のクエリでは、特定の製品モデルの製造手順を取得します。  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        /AWMI:root/AWMI:Location[1]/AWMI:step  
    ') as x  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 結果の一部を次に示します。  
  
```  
<AWMI:step xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">Insert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>. </AWMI:step>  
...  
```  
  
 **名前空間** キーワードを使用して、新しい名前空間プレフィックス "awmi:" が定義されていることに注意してください。 このプレフィックスは、その名前空間のスコープ内にあるすべての要素に対してクエリで使用する必要があります。  
  
### <a name="b-declaring-a-default-namespace"></a>B. 既定の名前空間の宣言  
 前のクエリでは、新しい名前空間プレフィックスが定義されています。 そのプレフィックスをクエリで使用して、目的の XML 構造を選択する必要がありました。 または、次の変更後のクエリに示すように、名前空間を既定の名前空間として宣言することもできます。  
  
```  
SELECT Instructions.query('  
     declare default element namespace "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        /root/Location[1]/step  
    ') as x  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 結果  
  
```  
<step xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">Insert <material>aluminum sheet MS-2341</material> into the <tool>T-85A framing tool</tool>. </step>  
...  
```  
  
 この例で、定義されている名前空間、`"https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"` は、既定または空の名前空間をオーバーライドするように作成されています。 このため、のクエリに使用されるパス式には名前空間プレフィックスがなくなりました。 また、結果に表示される要素名にも、名前空間プレフィックスはありません。 既定の名前空間は、すべての要素に適用されますが、属性には適用されません。  
  
### <a name="c-using-namespaces-in-xml-construction"></a>C. XML 構築時の名前空間の使用  
 新しい名前空間を定義すると、クエリだけでなく、構築用にもスコープに取り込まれます。 たとえば、XML を構築するときに、"" 宣言を使用して新しい名前空間を定義 `declare namespace ...` し、その名前空間を使用して、クエリの結果内に表示するように構成する任意の要素と属性を指定することができます。  
  
```  
SELECT CatalogDescription.query('  
     declare default element namespace "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     declare namespace myNS="uri:SomeNamespace";<myNS:Result>  
          { /ProductDescription/Summary }  
       </myNS:Result>  
  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 結果を次に示します。  
  
```  
  
      <myNS:Result xmlns:myNS="uri:SomeNamespace">  
  <Summary xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
     Our top-of-the-line competition mountain bike. Performance-enhancing   
     options include the innovative HL Frame, super-smooth front   
     suspension, and traction for all terrain.</p1:p>  
  </Summary>  
</myNS:Result>  
```  
  
 代わりに、次のクエリのように、XML 構築の一部として、名前空間を使用する各所で明示的に定義することもできます。  
  
```  
SELECT CatalogDescription.query('  
     declare default element namespace "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
       <myNS:Result xmlns:myNS="uri:SomeNamespace">  
          { /ProductDescription/Summary }  
       </myNS:Result>  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
### <a name="d-construction-using-default-namespaces"></a>D. 既定の名前空間を使用した構築  
 構築後の XML で既定の名前空間が使用されるように定義することもできます。 たとえば、次のクエリでは、既定の名前空間 "uri: SomeNamespace" を指定して、要素など、 \\ 構築されるローカルの名前付き要素の既定値として使用する方法を示して `<Result>` います。  
  
```  
SELECT CatalogDescription.query('  
      declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      declare default element namespace "uri:SomeNamespace";<Result>  
          { /PD:ProductDescription/PD:Summary }  
       </Result>  
  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 結果を次に示します。  
  
```  
  
      <Result xmlns="uri:SomeNamespace">  
  <PD:Summary xmlns:PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
         Our top-of-the-line competition mountain bike. Performance-  
         enhancing options include the innovative HL Frame, super-smooth   
         front suspension, and traction for all terrain.</p1:p>  
  </PD:Summary>  
</Result>  
```  
  
 既定の要素の名前空間または空の名前空間をオーバーライドすることにより、構築された XML 内のローカルで名前が付けられたすべての要素は、その後、オーバーライドする既定の名前空間にバインドされます。 したがって、空の名前空間を利用して XML を柔軟に構築する必要がある場合は、要素の既定の名前空間をオーバーライドしないようにします。  
  
## <a name="see-also"></a>参照  
 [WITH XMLNAMESPACES を使用したクエリへの名前空間の追加](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [XML データ &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 言語リファレンス &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
