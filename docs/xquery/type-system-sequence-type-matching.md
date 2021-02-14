---
title: シーケンスの型の一致 |Microsoft Docs
description: XQuery 式によって返されるシーケンス型を特定の型と一致させる方法について説明します。
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sequence type matching [XQuery]
- XQuery, sequence type matching
ms.assetid: 8c56fb69-ca04-4aba-b55a-64ae216c492d
author: rothja
ms.author: jroth
ms.openlocfilehash: 11c0eb693468b980db88995713dc6af99180c373
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100352824"
---
# <a name="type-system---sequence-type-matching"></a>型システム - シーケンス型の照合
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  XQuery 式の値は必ず 0 個以上のアイテムのシーケンスになります。 項目は、アトミック値またはノードのいずれかになります。 シーケンス型は、クエリ式によって返されるシーケンス型を特定の型と一致させる機能を表します。 次に例を示します。  
  
-   式の値が atomic の場合、整数、10進数、または文字列型であるかどうかを調べる必要があります。  
  
-   式の値が XML ノードの場合、その値がコメント ノード、処理命令ノード、またはテキスト ノードであるかどうかを確認できます。  
  
-   式が特定の名前と型の XML 要素または属性ノードを返すかどうかを調べることができます。  
  
 ブール演算子は、 `instance of` シーケンス型の照合に使用できます。 式の詳細については `instance of` 、「 [sequencetype 式 &#40;XQuery&#41;](../xquery/sequencetype-expressions-xquery.md)」を参照してください。  
  
## <a name="comparing-the-atomic-value-type-returned-by-an-expression"></a>式から返されるアトミック値の型の比較  
 式がアトミック値のシーケンスを返す場合、シーケンス内の値の型を検索することが必要になる場合があります。 次の例は、シーケンス型の構文を使用して式から返されるアトミック値の型を評価する方法を示しています。  
  
### <a name="example-determining-whether-a-sequence-is-empty"></a>例: シーケンスが空かどうかを確認する  
 **空の ()** シーケンス型は、指定された式によって返されるシーケンスが空のシーケンスであるかどうかを判断するために、シーケンス型の式で使用できます。  
  
 次の例では、XML スキーマを使用して、<`root`> 要素を nilled できます。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" nillable="true" type="byte"/>  
</schema>'  
GO  
```  
  
 ここで、型指定された XML インスタンスが <> 要素の値を指定した場合 `root` 、は `instance of empty()` False を返します。  
  
```  
DECLARE @var XML(SC1)  
SET @var = '<root>1</root>'  
-- The following returns False  
SELECT @var.query('data(/root[1]) instance of  empty() ')  
GO  
```  
  
 `root`インスタンスで <> 要素が nilled の場合、その値は空のシーケンスであり、は `instance of empty()` True を返します。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" />'  
SELECT @var.query('data(/root[1]) instance of  empty() ')  
GO  
```  
  
### <a name="example-determining-the-type-of-an-attribute-value"></a>例 : 属性値の型の判断  
 場合によっては、処理する前に、式によって返されるシーケンスの型を評価することが必要になることがあります。 たとえば、ノードが共用体型として定義されている XML スキーマがあるとします。 次の例では、コレクションの XML スキーマは、 `a` 値が decimal または string 型である共用体型として属性を定義しています。  
  
```  
-- Drop schema collection if it exists.  
-- DROP XML SCHEMA COLLECTION SC.  
-- GO  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
  <element name="root">  
    <complexType>  
       <sequence/>  
         <attribute name="a">  
            <simpleType>  
               <union memberTypes="decimal string"/>  
            </simpleType>  
         </attribute>  
     </complexType>  
  </element>  
</schema>'  
GO  
```  
  
 型指定された XML インスタンスを処理する前に、属性 `a` の値の型を確認できます。 次の例では、属性 `a` の値は小数型です。 したがって `, instance of xs:decimal` 、True が返されます。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root a="2.5"/>'  
SELECT @var.query('data((/root/@a)[1]) instance of xs:decimal')  
GO  
```  
  
 ここで、属性 `a` の値を文字列型に変更します。 は `instance of xs:string` True を返します。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root a="Hello"/>'  
SELECT @var.query('data((/root/@a)[1]) instance of xs:string')  
GO  
```  
  
### <a name="example-cardinality-in-sequence-expressions"></a>例: シーケンス式のカーディナリティ  
 この例は、シーケンス式でのカーディナリティの効果を示しています。 次の XML スキーマでは、 `root` バイト型の <> 要素が nillable に定義されています。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" nillable="true" type="byte"/>  
</schema>'  
GO  
```  
  
 次のクエリでは、式により単一のバイト型が返されるので、`instance of` から True が返されます。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root>111</root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte ')   
GO  
```  
  
 <を `root` 要素 nil> すると、その値は空のシーケンスになります。 つまり、式 `/root[1]` から空のシーケンスが返されます。 したがって、は `instance of xs:byte` False を返します。 この場合の既定のカーディナリティは 1 であることに注意してください。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"></root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte ')   
GO  
-- result = false  
```  
  
 出現インジケーター (`?`) を追加してカーディナリティを指定すると、シーケンス式から True が返されます。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"></root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte? ')   
GO  
-- result = true  
```  
  
 シーケンス型の式でのテストは、次の2つの段階で完了することに注意してください。  
  
1.  まず、テストでは、式の型が指定した型と一致するかどうかを判断します。  
  
2.  その場合、テストは、式によって返される項目の数が、指定された出現インジケーターと一致するかどうかを判断します。  
  
 どちらにも該当する場合、`instance of` 式から True が返されます。  
  
### <a name="example-querying-against-an-xml-type-column"></a>例: xml 型の列に対するクエリ  
 次の例では、データベースの **xml** 型の命令列に対してクエリを指定してい [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] ます。 Instructions 列にはスキーマが関連付けられているので、この列は型指定された XML 列です。 XML スキーマで整数型の `LocationID` 属性が定義されます。 したがって、シーケンス式では、は `instance of xs:integer?` True を返します。  
  
```  
SELECT Instructions.query('   
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
data(/AWMI:root[1]/AWMI:Location[1]/@LocationID) instance of xs:integer?') as Result   
FROM Production.ProductModel   
WHERE ProductModelID = 7  
```  
  
## <a name="comparing-the-node-type-returned-by-an-expression"></a>式によって返されるノードの種類の比較  
 式がノードのシーケンスを返す場合、シーケンス内のノードの型を見つける必要がある場合があります。 次の例は、シーケンス型の構文を使用して、式によって返されるノード型を評価する方法を示しています。 次のシーケンス型を使用できます。  
  
-   **item ()** -シーケンス内の任意の項目と一致します。  
  
-   **node ()** -シーケンスがノードであるかどうかを判断します。  
  
-   **processing-命令 ()** -式が処理命令を返すかどうかを判断します。  
  
-   **comment ()** -式がコメントを返すかどうかを判断します。  
  
-   **document-node ()** -式がドキュメントノードを返すかどうかを判断します。  
  
 これらのシーケンス型の例を次に示します。  
  
### <a name="example-using-sequence-types"></a>例: シーケンス型の使用  
 この例では、型指定されていない XML 変数に対していくつかのクエリを実行します。 これらのクエリは、シーケンス型の使用方法を示しています。  
  
```  
DECLARE @var XML  
SET @var = '<?xml-stylesheet href="someValue" type="text/xsl" ?>  
<root>text node  
  <!-- comment 1 -->   
  <a>Data a</a>  
  <!-- comment  2 -->  
</root>'  
```  
  
 最初のクエリでは、式によって <> 要素の型指定された値が返され `a` ます。 2番目のクエリでは、式は要素 <> を返し `a` ます。 両方とも項目です。 したがって、どちらのクエリも True を返します。  
  
```  
SELECT @var.query('data(/root[1]/a[1]) instance of item()')  
SELECT @var.query('/root[1]/a[1] instance of item()')  
```  
  
 次の3つのクエリのすべての XQuery 式は、<> 要素の子要素ノードを返し `root` ます。 そのため、シーケンス型の式 `instance of node()` から True が返され、他の 2 つの式 `instance of text()` と `instance of document-node()` からは False が返されます。  
  
```  
SELECT @var.query('(/root/*)[1] instance of node()')  
SELECT @var.query('(/root/*)[1] instance of text()')  
SELECT @var.query('(/root/*)[1] instance of document-node()')   
```  
  
 次のクエリでは、 `instance of document-node()` <`root`> 要素の親がドキュメントノードであるため、式は True を返します。  
  
```  
SELECT @var.query('(/root/..)[1] instance of document-node()') -- true  
```  
  
 次のクエリでは、式は XML インスタンスから最初のノードを取得します。 このノードは処理命令ノードなので、`instance of processing-instruction()` 式により True が返されます。  
  
```  
SELECT @var.query('(/node())[1] instance of processing-instruction()')  
```  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 具体的な制限は次のとおりです。  
  
-   コンテンツの種類が構文の **ドキュメント-node ()** はサポートされていません。  
  
-   **処理命令 (name)** 構文はサポートされていません。  
  
## <a name="element-tests"></a>要素のテスト  
 要素テストは、式によって返された要素ノードと、特定の名前および型を持つ要素ノードとを照合するために使用されます。 次のような要素のテストを使用できます。  
  
```  
element ()  
element(ElementName)  
element(ElementName, ElementType?)   
element(*, ElementType?)  
```  
  
## <a name="attribute-tests"></a>属性のテスト  
 属性のテストでは、式から返された属性が属性ノードであるかどうかが判断されます。 これらの属性テストを使用できます。  
  
 `attribute()`  
  
 `attribute(AttributeName)`  
  
 `attribute(AttributeName, AttributeType)`  
  
## <a name="test-examples"></a>テストの例  
 次の例は、要素のテストおよび属性のテストが役立つシナリオを示しています。  
  
### <a name="example-a"></a>例 A  
 次の XML スキーマでは、 `CustomerType` <`firstName`> と <`lastName`> 要素が省略可能な複合型を定義しています。 指定された XML インスタンスでは、特定の顧客に対して最初の名前が存在するかどうかを判断する必要がある場合があります。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
targetNamespace="myNS" xmlns:ns="myNS">  
  <complexType name="CustomerType">  
     <sequence>  
        <element name="firstName" type="string" minOccurs="0"   
                  nillable="true" />  
        <element name="lastName" type="string" minOccurs="0"/>  
     </sequence>  
  </complexType>  
  <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
DECLARE @var XML(SC)  
SET @var = '<x:customer xmlns:x="myNS">  
<firstName>SomeFirstName</firstName>  
<lastName>SomeLastName</lastName>  
</x:customer>'  
```  
  
 次のクエリでは、式を使用して、 `instance of element (firstName)` <> の最初の子要素 `customer` が> <名前を持つ要素であるかどうかを判断し `firstName` ます。 この場合、True が返されます。  
  
```  
SELECT @var.query('declare namespace x="myNS";   
     (/x:customer/*)[1] instance of element (firstName)')  
GO  
```  
  
 インスタンスから <> 要素を削除すると、 `firstName` クエリは False を返します。  
  
 次の項目を使用することもできます。  
  
-   `element(ElementName, ElementType?)`次のクエリに示すように、シーケンス型の構文。 この構文では、名前が `firstName` で型が `xs:string` の NULL 要素ノードまたは NULL 以外の要素ノードが照合されます。  
  
    ```  
    SELECT @var.query('declare namespace x="myNS";   
    (/x:customer/*)[1] instance of element (firstName, xs:string?)')  
    ```  
  
-   `element(*, type?)`次のクエリに示すように、シーケンス型の構文。 型がである場合は、その名前に関係なく、要素ノードと一致し `xs:string` ます。  
  
    ```  
    SELECT @var.query('declare namespace x="myNS"; (/x:customer/*)[1] instance of element (*, xs:string?)')  
    GO  
    ```  
  
### <a name="example-b"></a>例 B  
 次の例は、式によって返されるノードが特定の名前を持つ要素ノードであるかどうかを確認する方法を示しています。 **要素 ()** テストを使用します。  
  
 次の例では、クエリ対象の XML インスタンス内の2つの <`Customer`> 要素に、とという2つの異なる型があり `CustomerType` `SpecialCustomerType` ます。 `Customer`式によって返される <> 要素の型を知りたいとします。 次の XML スキーマ コレクションでは、`CustomerType` 型と `SpecialCustomerType` 型を定義しています。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
          targetNamespace="myNS"  xmlns:ns="myNS">  
  <complexType name="CustomerType">  
    <sequence>  
      <element name="firstName" type="string"/>  
      <element name="lastName" type="string"/>  
    </sequence>  
  </complexType>  
  <complexType name="SpecialCustomerType">  
     <complexContent>  
       <extension base="ns:CustomerType">  
        <sequence>  
            <element name="Age" type="int"/>  
        </sequence>  
       </extension>  
     </complexContent>  
    </complexType>  
   <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
```  
  
 この XML スキーマコレクションは、型指定された **xml** 変数を作成するために使用されます。 この変数に割り当てられた XML インスタンスには、 `customer` 2 つの異なる型の2つの <> 要素があります。 最初の要素は `CustomerType` 型で、2 つ目の要素は `SpecialCustomerType` 型です。  
  
```  
DECLARE @var XML(SC)  
SET @var = '  
<x:customer xmlns:x="myNS">  
   <firstName>FirstName1</firstName>  
   <lastName>LastName1</lastName>  
</x:customer>  
<x:customer xsi:type="x:SpecialCustomerType" xmlns:x="myNS" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
   <firstName> FirstName2</firstName>  
   <lastName> LastName2</lastName>  
   <Age>21</Age>  
</x:customer>'  
```  
  
 次のクエリで、`instance of element (*, x:SpecialCustomerType ?)` 式は False を返します。この式で返されている最初の customer 要素が、`SpecialCustomerType` 型ではないためです。  
  
```  
SELECT @var.query('declare namespace x="myNS";   
    (/x:customer)[1] instance of element (*, x:SpecialCustomerType ?)')  
```  
  
 前のクエリの式を変更し、2番目の <`customer`> 要素 () を取得した場合、は `/x:customer)[2]` True を `instance of` 返します。  
  
### <a name="example-c"></a>例 C  
 この例では、属性のテストを使用します。 次の XML スキーマでは、CustomerID 属性と Age 属性を使用して、顧客の Type 複合型を定義しています。 Age 属性は省略可能です。 特定の XML インスタンスの場合は、Age 属性が <> 要素に存在するかどうかを判断でき `customer` ます。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
       targetNamespace="myNS" xmlns:ns="myNS">  
<complexType name="CustomerType">  
  <sequence>  
     <element name="firstName" type="string" minOccurs="0"   
               nillable="true" />  
     <element name="lastName" type="string" minOccurs="0"/>  
  </sequence>  
  <attribute name="CustomerID" type="integer" use="required" />  
  <attribute name="Age" type="integer" use="optional" />  
 </complexType>  
 <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
```  
  
 次のクエリでは、クエリ対象の XML インスタンスに `Age` という名前の属性ノードが存在するので、True が返されます。 この式では、`attribute(Age)` 属性のテストを使用しています。 属性の順序が決まっていないので、クエリでは FLWOR 式を使用してすべての属性を取得し、`instance of` 式を使用して各属性をテストします。 この例では、まず XML スキーマコレクションを作成して、型指定された **xml** 変数を作成します。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<x:customer xmlns:x="myNS" CustomerID="1" Age="22" >  
<firstName>SomeFName</firstName>  
<lastName>SomeLName</lastName>  
</x:customer>'  
SELECT @var.query('declare namespace x="myNS";   
FOR $i in /x:customer/@*  
RETURN  
    IF ($i instance of attribute (Age)) THEN  
        "true"  
        ELSE  
        ()')     
GO  
  
```  
  
 省略可能な `Age` 属性をインスタンスから削除すると、上記のクエリにより False が返されます。  
  
 属性の名前と型 () は `attribute(name,type)` 、属性のテストで指定できます。  
  
```  
SELECT @var.query('declare namespace x="myNS";   
FOR $i in /x:customer/@*  
RETURN  
    IF ($i instance of attribute (Age, xs:integer)) THEN  
        "true"  
        ELSE  
        ()')  
```  
  
 または、シーケンス型の構文を指定することもでき `attribute(*, type)` ます。 名前に関係なく、属性の型が指定した型と一致する場合、これは属性ノードと一致します。  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 具体的な制限は次のとおりです。  
  
-   要素のテストでは、型名の後に出現インジケーター (**?**) を続ける必要があります。  
  
-   **要素 (ElementName、TypeName)** はサポートされていません。  
  
-   **要素 ( \* 、TypeName)** はサポートされていません。  
  
-   **スキーマ要素 ()** はサポートされていません。  
  
-   **スキーマ属性 (AttributeName)** はサポートされていません。  
  
-   **Xsi: type** または **xsi: nil** の明示的なクエリはサポートされていません。  
  
## <a name="see-also"></a>参照  
 [型システム &#40;XQuery&#41;](../xquery/type-system-xquery.md)  
  
  
