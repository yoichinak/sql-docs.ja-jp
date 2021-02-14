---
title: XML の構築 (XQuery) |Microsoft Docs
description: 直接および計算されたコンストラクターを使用して XQuery で XML 構造を構築する方法について説明します。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- white space [XQuery]
- computed constructor
- construct XML structures [XQuery]
- constructors [XQuery]
- prolog
- direct constructor [SQL Server]
- XML [SQL Server], construction
- XQuery, XML construction
ms.assetid: a6330b74-4e52-42a4-91ca-3f440b3223cf
author: rothja
ms.author: jroth
ms.openlocfilehash: 1c171dab70a909edb197f5a498d2207bcb2e555b
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100352319"
---
# <a name="xml-construction-xquery"></a>XML の構築 (XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  XQuery では、 **直接** コンストラクターと **計算** コンストラクターを使用して、クエリ内に XML 構造を構築できます。  
  
> [!NOTE]  
>  **直接** コンストラクターと **計算** コンストラクターの間に違いはありません。  
  
## <a name="using-direct-constructors"></a>直接コンストラクターの使用  
 直接コンストラクターを使用する場合は、xml を構築するときに XML に似た構文を指定します。 次の例では、直接コンストラクターを使用した XML 構築を示しています。  
  
### <a name="constructing-elements"></a>要素の構築  
 XML の表記法を使用して要素を構築できます。 次の例では、直接要素コンストラクター式を使用して、要素を作成し \<ProductModel> ます。 構築される要素には、次の 3 つの子要素があります。  
  
-   テキストノード。  
  
-   とという2つの要素ノード \<Summary> \<Features> 。  
  
    -   要素には、 \<Summary> 値が "Some description" である1つのテキストノード子があります。  
  
    -   要素には、、、 \<Features> およびという3つの要素ノードがあり \<Color> \<Weight> \<Warranty> ます。 これらの各ノードには、それぞれ1つのテキストノードがあり、赤、25、2年の部分、および労務の値が設定されています。  
  
```sql
declare @x xml;  
set @x='';  
select @x.query('<ProductModel ProductModelID="111">;  
This is product model catalog description.  
<Summary>Some description</Summary>  
<Features>  
  <Color>Red</Color>  
  <Weight>25</Weight>  
  <Warranty>2 years parts and labor</Warranty>  
</Features></ProductModel>')  
  
```  
  
 作成された XML を次に示します。  
  
```xml
<ProductModel ProductModelID="111">  
  This is product model catalog description.  
  <Summary>Some description</Summary>  
  <Features>  
    <Color>Red</Color>  
    <Weight>25</Weight>  
    <Warranty>2 years parts and labor</Warranty>  
  </Features>  
</ProductModel>  
```  
  
 この例で示しているように、定数式から要素を構築すると便利ですが、XQuery 言語機能の真の威力は、データベースから動的にデータを抽出する XML を構築できる点にあります。 中かっこを使用してクエリ式を指定できます。 結果の XML では、式はその値に置き換えられます。 たとえば、次のクエリでは、 `NewRoot` 1 つの子要素 (<>) を持つ <> 要素が構築され `e` ます。 要素 <> の値は、中 `e` かっこ ("{...}") 内にパス式を指定することによって計算されます。  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
SELECT @x.query('<NewRoot><e> { /root } </e></NewRoot>');  
```  
  
 中かっこはコンテキスト切り替えトークンとして機能し、クエリを XML 構築からクエリ評価に切り替えます。 この場合、中かっこ内の XQuery パス式 `/root` が評価され、その結果が代わりに使用されます。  
  
 結果を次に示します。  
  
```xml
<NewRoot>  
  <e>  
    <root>5</root>  
  </e>  
</NewRoot>  
```  
  
 次に示すクエリは先ほどのクエリと似ています。 ただし、中かっこ内の式では、 **data ()** 関数を指定して <> 要素のアトミック値を取得 `root` し、構築された要素 <> に代入し `e` ます。  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('  
                           <NewRoot>  
                             <e> { data(/root) } </e>  
                           </NewRoot>' ));  
SELECT @y;  
```  
  
 結果を次に示します。  
  
```xml
<NewRoot>  
  <e>5</e>  
</NewRoot>  
```  
  
 コンテキスト切り替えトークンではなく、テキストの一部として中かっこを使用する場合は、次の例に示すように、"}}" または "{{" としてエスケープできます。  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('  
<NewRoot> Hello, I can use {{ and  }} as part of my text</NewRoot>'));  
SELECT @y;  
```  
  
 結果を次に示します。  
  
```xml
<NewRoot> Hello, I can use { and  } as part of my text</NewRoot>  
```  
  
 次のクエリは、直接要素コンストラクターを使用して要素を構築するもう1つの例です。 また、<> 要素の値 `FirstLocation` は、中かっこ内の式を実行することによって取得されます。 クエリ式は、最初のワークセンターの場所にある製造手順を、Production モデルテーブルの [命令」列から返します。  
  
```sql
SELECT Instructions.query('  
    declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        <FirstLocation>  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 結果を次に示します。  
  
```xml
<FirstLocation>  
  <AWMI:step xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">  
      Insert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>.   
  </AWMI:step>  
  <AWMI:step xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">  
      Attach <AWMI:tool>Trim Jig TJ-26</AWMI:tool> to the upper and lower right corners of the aluminum sheet.   
  </AWMI:step>  
   ...  
</FirstLocation>  
```  
  
#### <a name="element-content-in-xml-construction"></a>XML の構築での要素の内容  
 次の例は、直接要素コンストラクターを使用して要素コンテンツを構築する際の式の動作を示しています。 次の例では、直接要素コンストラクターで 1 つの式が指定されています。 この式では、構築される XML に 1 つのテキスト ノードが作成されます。  
  
```sql
declare @x xml;  
set @x='  
<root>  
  <step>This is step 1</step>  
  <step>This is step 2</step>  
  <step>This is step 3</step>  
</root>';  
select @x.query('  
<result>  
 { for $i in /root[1]/step  
    return string($i)  
 }  
</result>');  
  
```  
  
 式の評価によって得られるアトミック値のシーケンスは、結果に示されているように、隣接するアトミック値の間にスペースを追加してテキストノードに追加されます。 構築された要素には1つの子があります。 これは、結果に表示される値を含むテキストノードです。  
  
```xml
<result>This is step 1 This is step 2 This is step 3</result>  
```  
  
 1つの式の代わりに、3つのテキストノードを生成する3つの個別の式を指定した場合、隣接するテキストノードは、結果の XML の連結によって1つのテキストノードに結合されます。  
  
```sql
declare @x xml;  
set @x='  
<root>  
  <step>This is step 1</step>  
  <step>This is step 2</step>  
  <step>This is step 3</step>  
</root>';  
select @x.query('  
<result>  
 { string(/root[1]/step[1]) }  
 { string(/root[1]/step[2]) }  
 { string(/root[1]/step[3]) }  
</result>');  
```  
  
 構築された要素ノードには1つの子があります。 これは、結果に表示される値を含むテキストノードです。  
  
```xml
<result>This is step 1This is step 2This is step 3</result>  
```  
  
### <a name="constructing-attributes"></a>属性の構築  
 直接要素コンストラクターを使用して要素を構築する場合は、次の例に示すように、XML に似た構文を使用して要素の属性を指定することもできます。  
  
```sql
declare @x xml;  
set @x='';  
select @x.query('<ProductModel ProductModelID="111">;  
This is product model catalog description.  
<Summary>Some description</Summary>  
</ProductModel>')  
```  
  
 作成された XML を次に示します。  
  
```xml
<ProductModel ProductModelID="111">  
  This is product model catalog description.  
  <Summary>Some description</Summary>  
</ProductModel>  
```  
  
 構築された要素 <`ProductModel`> には、ProductModelID 属性とこれらの子ノードがあります。  
  
-   テキストノード `This is product model catalog description.`  
  
-   要素ノード、<`Summary`>。 このノードには、`Some description` という子テキスト ノードが 1 つあります。  
  
 属性を構築するときは、中かっこで囲まれた式を使用して、その値を指定できます。 この場合、式の結果が属性値として返されます。  
  
 次の例では、 **data ()** 関数は厳密には必要ありません。 式の値を属性に割り当てるため、指定された式の型指定された値を取得するために、 **データ ()** が暗黙的に適用されます。  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('<NewRoot attr="{ data(/root) }" ></NewRoot>'));  
SELECT @y;  
```  
  
 結果を次に示します。  
  
```xml
<NewRoot attr="5" />  
```  
  
 次に示すのは、LocationID と SetupHrs の属性の構築に式が指定されている例です。 これらの式は、命令列の XML に対して評価されます。 式の型指定された値が属性に割り当てられます。  
  
```sql
SELECT Instructions.query('  
    declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        <FirstLocation   
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7;  
```  
  
 結果の一部を次に示します。  
  
```xml
<FirstLocation LocationID="10" SetupHours="0.5" >  
  <AWMI:step ...   
  </AWMI:step>  
  ...  
</FirstLocation>  
```  
  
#### <a name="implementation-limitations"></a>実装の制限事項  
 制限事項は次のとおりです。  
  
-   複数のまたは mixed (string および XQuery 式) 属性式はサポートされていません。 たとえば、次のクエリに示すように、が定数で、 `Item` `5` クエリ式を評価することによって値が取得される XML を構築します。  
  
    ```xml
    <a attr="Item 5" />  
    ```  
  
     次のクエリでは、定数文字列と式 ({/x}) が混在しているため、エラーが返されます。これはサポートされていません。  
  
    ```sql
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    SELECT @x.query( '<a attr="Item {/x}"/>' )   
    ```  
  
     その場合は、次のいずれかの方法で対処します。  
  
    -   2つのアトミック値の連結によって属性値を形成します。 この 2 つのアトミック値は、間に空白が挿入されて 1 つの属性値へとシリアル化されます。  
  
        ```sql
        SELECT @x.query( '<a attr="{''Item'', data(/x)}"/>' )   
        ```  
  
         結果を次に示します。  
  
        ```xml
        <a attr="Item 5" />  
        ```  
  
    -   2つの文字列引数を結果の属性値に連結するには、 [concat 関数](../xquery/functions-on-string-values-concat.md) を使用します。  
  
        ```sql
        SELECT @x.query( '<a attr="{concat(''Item'', /x[1])}"/>' )   
        ```  
  
         この場合、2 つの文字列値の間に空白が追加されません。 2 つの文字列値の間に空白が必要な場合は、明示的に空白を指定する必要があります。  
  
         結果を次に示します。  
  
        ```xml
        <a attr="Item5" />  
        ```  
  
-   属性値としての複数の式はサポートされていません。 たとえば、次のクエリではエラーが返されます。  
  
    ```sql
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    SELECT @x.query( '<a attr="{/x}{/x}"/>' )  
    ```  
  
-   異種シーケンスはサポートされません。 次の例に示すように、1 つの属性値として異種シーケンスを割り当てようとすると、エラーが返されます。 この例では、異種シーケンス、文字列 "Item"、要素 <`x`> が属性値として指定されています。  
  
    ```sql
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    select @x.query( '<a attr="{''Item'', /x }" />')  
    ```  
  
     **Data ()** 関数を適用すると、クエリは、 `/x` 文字列と連結された式のアトミック値を取得するため、機能します。 アトミック値のシーケンスを次に示します。  
  
    ```sql
    SELECT @x.query( '<a attr="{''Item'', data(/x)}"/>' )   
    ```  
  
     結果を次に示します。  
  
    ```xml
    <a attr="Item 5" />  
    ```  
  
-   属性ノードの順序は、静的な型チェックの実行時ではなく、シリアル化中に適用されます。 たとえば、次のクエリは、属性以外のノードの後に属性を追加しようとするため失敗します。  
  
    ```sql
    select convert(xml, '').query('  
    element x { attribute att { "pass" }, element y { "Element text" }, attribute att2 { "fail" } }  
    ')  
    go  
    ```  
  
     上記のクエリは、次のエラーを返します。  
  
    ```  
    XML well-formedness check: Attribute cannot appear outside of element declaration. Rewrite your XQuery so it returns well-formed XML.  
    ```  
  
### <a name="adding-namespaces"></a>名前空間の追加  
 直接コンストラクターを使用して XML を構築する場合、構築された要素名と属性名は、名前空間プレフィックスを使用して修飾できます。 次の方法でプレフィックスを名前空間にバインドできます。  
  
-   名前空間宣言属性を使用する方法。  
  
-   WITH XMLNAMESPACES 句を使用する。  
  
-   XQuery プロローグで。  
  
#### <a name="using-a-namespace-declaration-attribute-to-add-namespaces"></a>名前空間宣言属性を使用した名前空間の追加  
 次の例では、要素 <> の構築で名前空間宣言属性を使用して、 `a` 既定の名前空間を宣言しています。 `b`親要素で宣言された既定の名前空間の宣言を元に戻すために、子要素 <> を構築しています。  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <a xmlns="a">  
    <b xmlns=""/>  
  </a>' )   
```  
  
 結果を次に示します。  
  
```xml
<a xmlns="a">  
  <b xmlns="" />  
</a>  
```  
  
 名前空間にプレフィックスを割り当てることができます。 プレフィックスは、要素 <> の構築で指定され `a` ます。  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <x:a xmlns:x="a">  
    <b/>  
  </x:a>' )  
```  
  
 結果を次に示します。  
  
```xml
<x:a xmlns:x="a">  
  <b />  
</x:a>  
```  
  
 XML の構築では、既定の名前空間を宣言解除できますが、名前空間プレフィックスを宣言解除することはできません。 次のクエリはエラーを返します。これは、要素 <> の構築で指定されているプレフィックスを宣言解除できないため `b` です。  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <x:a xmlns:x="a">  
    <b xmlns:x=""/>  
  </x:a>' )  
```  
  
 新しく構築される名前空間は、クエリ内部で使用できます。 たとえば、次のクエリでは、要素を構築する際に名前空間を宣言し、 `FirstLocation`> <して、LocationID と SetupHrs の属性値の式でプレフィックスを指定しています。  
  
```sql
SELECT Instructions.query('  
        <FirstLocation xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
 この方法で新しい名前空間プレフィックスを作成すると、このプレフィックスの既存の名前空間宣言がオーバーライドされることに注意してください。 たとえば、クエリプロローグ内の名前空間宣言は、 `AWMI="https://someURI"` <> 要素の名前空間宣言によってオーバーライドされ `FirstLocation` ます。  
  
```sql
SELECT Instructions.query('  
declare namespace AWMI="https://someURI";  
        <FirstLocation xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
#### <a name="using-a-prolog-to-add-namespaces"></a>プロローグを使用した名前空間の追加  
 次の例では、構築される XML にどのように名前空間が追加されるのかを示しています。 既定の名前空間は、クエリのプロローグで宣言されます。  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
           declare default element namespace "a";  
            <a><b xmlns=""/></a>' )  
```  
  
 要素 <> の構築では `b` 、名前空間宣言属性が、値として空の文字列で指定されていることに注意してください。 これにより、親要素で宣言されている既定の名前空間の宣言が解除されます。  
  

結果を次に示します。  

```xml
<a xmlns="a">  
  <b xmlns="" />  
</a>  
```  
  
### <a name="xml-construction-and-white-space-handling"></a>XML の構築と空白文字の処理  
 XML 構築の要素コンテンツには、空白文字を含めることができます。 これらの文字は、次の方法で処理されます。  
  
-   名前空間 Uri 内の空白文字は、XSD 型 **anyURI** として扱われます。 具体的には、空白文字は次のように処理されます。  
  
    -   最初と最後にある空白文字は切り捨てられます。  
  
    -   内部の空白文字の値が1つのスペースに折りたたまれる  
  
-   属性コンテンツ内の改行文字は、スペースで置き換えられます。 その他のすべての空白文字はそのまま残ります。  
  
-   要素内の空白文字は保持されます。  
  
 次の例は、XML の構築における空白の処理を示しています。  
  
```sql
-- line feed is repaced by space.  
declare @x xml  
set @x=''  
select @x.query('  
  
declare namespace myNS="   https://       
 abc/  
xyz  
  
";  
<test attr="    my   
test   attr   
value    " >  
  
<a>  
  
This     is  a  
  
test  
  
</a>  
</test>  
') as XML_Result  
  
```  
  
 結果を次に示します。  
  
```xml
-- result  
<test attr="<test attr="    my test   attr  value    "><a>  
  
This     is  a  
  
test  
  
</a></test>  
"><a>  
  
This     is  a  
  
test  
  
</a></test>  
```  
  
### <a name="other-direct-xml-constructors"></a>その他の直接 XML コンストラクター  
 処理命令や XML コメントのコンストラクターでは、対応する XML の構築と同じ構文を使用します。 テキストノードの計算されるコンストラクターもサポートされていますが、主に XML DML でテキストノードを作成するために使用されます。  
  
 **メモ** 明示的なテキストノードコンストラクターの使用例については、「 [insert &#40;XML DML&#41;](../t-sql/xml/insert-xml-dml.md)」の特定の例を参照してください。  
  
 次のクエリでは、構築された XML に要素、2つの属性、コメント、および処理命令が含まれています。 `FirstLocation`シーケンスが構築されているため、<> の前にコンマが使用されていることに注意してください。  
  
```sql
SELECT Instructions.query('  
  declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   <?myProcessingInstr abc="value" ?>,   
   <FirstLocation   
        WorkCtrID = "{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
        SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
       <!-- some comment -->  
       <?myPI some processing instructions ?>  
       { (/AWMI:root/AWMI:Location[1]/AWMI:step) }  
    </FirstLocation>   
') as Result   
FROM Production.ProductModel  
where ProductModelID=7;  
  
```  
  
 結果の一部を次に示します。  
  
```xml
<?myProcessingInstr abc="value" ?>  
<FirstLocation WorkCtrID="10" SetupHrs="0.5">  
  <!-- some comment -->  
  <?myPI some processing instructions ?>  
  <AWMI:step xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">I  
  nsert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>.   
  </AWMI:step>  
    ...  
</FirstLocation>  
  
```  
  
## <a name="using-computed-constructors"></a>計算コンストラクターの使用  
 . このコンストラクターを使用する場合は、構築するノードの種類を特定するキーワードを指定します。 次のキーワードのみがサポートされています。  
  
-   要素  
  
-   属性 (attribute)  
  
-   text  
  
 要素ノードと属性ノードの場合、これらのキーワードの後には、ノード名と、そのノードのコンテンツを生成する式 (中かっこで囲まれた式) が続きます。 この後に示す例では、次の XML を構築しています。  
  
```xml
<root>  
  <ProductModel PID="5">Some text <summary>Some Summary</summary></ProductModel>  
</root>  
```  
  
 次に示すのは、計算コンストラクターを使用して XML を生成するクエリです。  
  
```sql
declare @x xml  
set @x=''  
select @x.query('element root   
               {   
                  element ProductModel  
     {  
attribute PID { 5 },  
text{"Some text "},  
    element summary { "Some Summary" }  
 }  
               } ')  
  
```  
  
 ノードの内容を生成する式では、クエリ式を指定できます。  
  
```sql
declare @x xml  
set @x='<a attr="5"><b>some summary</b></a>'  
select @x.query('element root   
               {   
                  element ProductModel  
     {  
attribute PID { /a/@attr },  
text{"Some text "},  
    element summary { /a/b }  
 }  
               } ')  
```  
  
 XQuery 仕様で定義されているように、計算される要素と属性のコンストラクターによって、ノード名を計算できることに注意してください。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] で直接コンストラクターを使用している場合は、element や attribute などのノード名を定数リテラルとして指定する必要があります。 したがって、直接コンストラクターと、要素と属性の計算されるコンストラクターに違いはありません。  
  
 次の例では、構築されたノードのコンテンツは、ProductModel テーブルの **xml** データ型の命令列に格納されている xml 製造手順から取得されます。  
  
```sql
SELECT Instructions.query('  
  declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   element FirstLocation   
     {  
        attribute LocationID { (/AWMI:root/AWMI:Location[1]/@LocationID)[1] },  
        element   AllTheSteps { /AWMI:root/AWMI:Location[1]/AWMI:step }  
     }  
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
 結果の一部を次に示します。  
  
```xml
<FirstLocation LocationID="10">  
  <AllTheSteps>  
    <AWMI:step> ... </AWMI:step>  
    <AWMI:step> ... </AWMI:step>  
    ...  
  </AllTheSteps>  
</FirstLocation>    
```  
  
## <a name="additional-implementation-limitations"></a>実装のその他の制限事項  
 属性計算コンストラクターを使用して新しい名前空間を宣言することはできません。 また、次の計算されるコンストラクターはではサポートされていません [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。  
  
-   計算されたドキュメントノードコンストラクター  
  
-   計算される処理命令コンストラクター  
  
-   計算されるコメントコンストラクター  
  
## <a name="see-also"></a>参照  
 [XQuery 式](../xquery/xquery-expressions.md)  
  
  
