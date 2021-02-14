---
title: SequenceType 式 (XQuery) |Microsoft Docs
description: の XQuery SequenceType 式のインスタンスについて説明し、としてキャストします。
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
- SequenceType expressions
- instance of operator [XQuery]
- expressions [XQuery], SequenceType
- cast as operator
ms.assetid: ad3573da-d820-4d1c-81c4-a83c4640ce22
author: rothja
ms.author: jroth
ms.openlocfilehash: 0627d892733f84cb4a8d1b5cf80ad65d9c09f824
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100335848"
---
# <a name="sequencetype-expressions-xquery"></a>SequenceType 式 (XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  XQuery では、値は常にシーケンスです。 値の型は、シーケンス型と呼ばれます。 このシーケンス型は、XQuery 式 **のインスタンス** で使用できます。 XQuery 式で型を参照する必要があるときは、XQuery 仕様に記載されている SequenceType 構文を使用します。  
  
 アトミック型の名前は、 **cast としてキャスト式として** 使用することもできます。 では、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] **のインスタンス** と、sequencetypes の XQuery 式 **としてのキャスト** は部分的にサポートされています。  
  
## <a name="instance-of-operator"></a>演算子のインスタンス  
 **のインスタンス** 演算子を使用すると、指定された式の値の動的な型または実行時の型を判断できます。 次に例を示します。  
  
```  
  
Expression instance of SequenceType[Occurrence indicator]  
```  
  
 演算子、は、結果として `instance of` `Occurrence indicator` 得られるシーケンス内のカーディナリティ、項目数を指定することに注意してください。 このが指定されていない場合、カーディナリティは1と見なされます。 で [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は、疑問符 (**?)** オカレンスインジケーターのみがサポートされています。 **?** 出現インジケーターは、が `Expression` 0 または1個の項目を返すことを示します。 **?** オカレンスインジケーターが指定されている場合、が `instance of` `Expression` `SequenceType` シングルトンまたは空のシーケンスを返すかどうかにかかわらず、型が指定されたと一致する場合は True を返し `Expression` ます。  
  
 **?** オカレンスインジケーターが指定されていません `sequence of` 。型が指定されたと一致する場合にのみ True を返し、 `Expression` `Type` `Expression` シングルトンを返します。  
  
 **メモ** プラス記号 ( **+** ) とアスタリスク (**&#42;**) の出現インジケーターは、ではサポートされていません [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。  
  
 次の例は、XQuery 演算子 **のインスタンス** の使用方法を示しています。  
  
### <a name="example-a"></a>例 A  
 次の例では、 **xml** 型の変数を作成し、その変数に対してクエリを指定します。 クエリ式では、 `instance of` 最初のオペランドによって返される値の動的な型が2番目のオペランドで指定された型と一致するかどうかを判断する演算子を指定します。  
  
 次のクエリは True を返します。125値は指定された型のインスタンス **xs: integer** です。  
  
```  
declare @x xml  
set @x=''  
select @x.query('125 instance of xs:integer')  
go  
```  
  
 次のクエリでは、最初のオペランドの式 /a[1] から返される値が要素なので True が返されます。  
  
```  
declare @x xml  
set @x='<a>1</a>'  
select @x.query('/a[1] instance of element()')  
go  
```  
  
 同様に、次のクエリでは最初の式に含まれている式の値の型が属性型なので、`instance of` から True が返されます。  
  
```  
declare @x xml  
set @x='<a attr1="x">1</a>'  
select @x.query('/a[1]/@attr1 instance of attribute()')  
go  
```  
  
 次の例では、式は、 `data(/a[1]` xdt: untypedAtomic として型指定されたアトミック値を返します。 したがって、は `instance of` True を返します。  
  
```  
declare @x xml  
set @x='<a>1</a>'  
select @x.query('data(/a[1]) instance of xdt:untypedAtomic')  
go  
```  
  
 次のクエリでは、式は、型指定されて `data(/a[1]/@attrA` いないアトミック値を返します。 したがって、は `instance of` True を返します。  
  
```  
declare @x xml  
set @x='<a attrA="X">1</a>'  
select @x.query('data(/a[1]/@attrA) instance of xdt:untypedAtomic')  
go  
```  
  
### <a name="example-b"></a>例 B  
 この例では、AdventureWorks サンプルデータベース内の型指定された XML 列に対してクエリを実行します。 クエリ対象の列に関連付けられている XML スキーマコレクションでは、入力情報が提供されます。  
  
 式では、 **data ()** は、列に関連付けられているスキーマに従って、型が xs: string である ProductModelID 属性の型指定された値を返します。 したがって、は `instance of` True を返します。  
  
```  
SELECT CatalogDescription.query('  
   declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
   data(/PD:ProductDescription[1]/@ProductModelID) instance of xs:string  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 詳細については、「 [型指定された XML と型指定されていない XML の比較](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)」を参照してください。  
  
 次のクエリでは、ブール式を使うことで `instance of` 、LocationID 属性が xs: integer 型であるかどうかを判断します。  
  
```  
SELECT Instructions.query('  
   declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   /AWMI:root[1]/AWMI:Location[1]/@LocationID instance of attribute(LocationID,xs:integer)  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 次のクエリは、CatalogDescription 型指定された XML 列に対して指定されています。 この列に関連付けられた XML スキーマ コレクションにより、型指定情報が提供されます。  
  
 このクエリでは `element(ElementName, ElementType?)` 、式のテストを使用し `instance of` て、が `/PD:ProductDescription[1]` 特定の名前と型の要素ノードを返すことを確認します。  
  
```  
SELECT CatalogDescription.query('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /PD:ProductDescription[1] instance of element(PD:ProductDescription, PD:ProductDescription?)  
    ') as Result  
FROM  Production.ProductModel  
where ProductModelID=19  
```  
  
 このクエリは True を返します。  
  
### <a name="example-c"></a>例 C  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の `instance of` 式は共用体型を使用する場合に制限があります。具体的には、要素または属性の型が共用体型の場合、`instance of` で正確な型が判断されません。 したがって、SequenceType で使用されているアトミック型が、simpleType 階層内にある式の実際の型の最上位の親でない限り、クエリから False が返されます。 つまり、SequenceType で指定されたアトミック型は、anySimpleType の直接の子である必要があります。 型階層の詳細については、「 [XQuery での型キャストの規則](../xquery/type-casting-rules-in-xquery.md)」を参照してください。  
  
 次のクエリの例では、次の処理を実行します。  
  
-   整数型や文字列型など、共用体型を使用して XML スキーマコレクションを作成します。  
  
-   XML スキーマコレクションを使用して、型指定された **xml** 変数を宣言します。  
  
-   サンプル XML インスタンスを変数に割り当てます。  
  
-   変数にクエリして、共用体型を処理するときの `instance of` の動作を示します。  
  
 クエリは次のとおりです。  
  
```  
CREATE XML SCHEMA COLLECTION MyTestSchema AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns" xmlns:ns="http://ns">  
<simpleType name="MyUnionType">  
<union memberTypes="integer string"/>  
</simpleType>  
<element name="TestElement" type="ns:MyUnionType"/>  
</schema>'  
Go  
```  
  
 次のクエリでは、`instance of` 式に指定している SequenceType が、指定した式の実際の型の最上位の親ではないので  False が返されます。 つまり、<> の値 `TestElement` は整数型です。 最上位の親は xs: decimal です。 しかし、この型が `instance of` 演算子の 2 つ目のオペランドとして指定されていません。  
  
```  
SET QUOTED_IDENTIFIER ON  
DECLARE @var XML(MyTestSchema)  
  
SET @var = '<TestElement xmlns="http://ns">123</TestElement>'  
  
SELECT @var.query('declare namespace ns="http://ns"   
   data(/ns:TestElement[1]) instance of xs:integer')  
go  
```  
  
 Xs: integer の最上位の親は xs: decimal であるため、クエリを変更し、クエリの SequenceType として xs: decimal を指定すると、True が返されます。  
  
```  
SET QUOTED_IDENTIFIER ON  
DECLARE @var XML(MyTestSchema)  
SET @var = '<TestElement xmlns="http://ns">123</TestElement>'  
SELECT @var.query('declare namespace ns="http://ns"     
   data(/ns:TestElement[1]) instance of xs:decimal')  
go  
```  
  
### <a name="example-d"></a>例 D  
 この例では、まず XML スキーマコレクションを作成し、それを使用して **xml** 変数を入力します。 次に、型指定された **xml** 変数を照会して、機能を説明し `instance of` ます。  
  
 次の XML スキーマコレクションは、単純型、myType、および `root` myType 型の要素 <> を定義します。  
  
```  
drop xml schema collection SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="myNS" xmlns:ns="myNS"  
xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">  
      <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
      <simpleType name="myType">  
           <restriction base="s:varchar">  
                  <maxLength value="20"/>  
            </restriction>  
      </simpleType>  
      <element name="root" type="ns:myType"/>  
</schema>'  
Go  
```  
  
 次に、型指定された **xml** 変数を作成してクエリを実行します。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "https://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
   data(/ns:root[1]) instance of ns:myType')  
go  
```  
  
 MyType 型は、sqltypes スキーマで定義されている varchar 型からの制限によって派生するため、 `instance of` も True を返します。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "https://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
data(/ns:root[1]) instance of sqltypes:varchar?')  
go  
```  
  
### <a name="example-e"></a>例 E  
 次の例では、式で IDREFS 属性のいずれかの値を取得し、`instance of` を使用して値が IDREF 型かどうかを判断しています。 この例では、次の処理を実行します。  
  
-   <`Customer`> 要素に **orderlist** IDREFS 型属性があり、<`Order`> 要素に **OrderID** ID 型属性がある XML スキーマコレクションを作成します。  
  
-   型指定された **xml** 変数を作成し、その変数にサンプル xml インスタンスを割り当てます。  
  
-   変数に対してクエリを指定します。 クエリ式は、最初の <> の OrderList IDRERS 型属性から最初の注文 ID 値を取得し `Customer` ます。 取得される値は IDREF 型です。 したがって、は `instance of` True を返します。  
  
```  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:Customers="Customers" targetNamespace="Customers">  
            <element name="Customers" type="Customers:CustomersType"/>  
            <complexType name="CustomersType">  
                        <sequence>  
                            <element name="Customer" type="Customers:CustomerType" minOccurs="0" maxOccurs="unbounded" />  
                        </sequence>  
            </complexType>  
             <complexType name="OrderType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="OrderValue" type="integer" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="OrderID" type="ID" />  
            </complexType>  
  
            <complexType name="CustomerType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="spouse" type="string" minOccurs="0" maxOccurs="unbounded"/>  
                                <element name="Order" type="Customers:OrderType" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="CustomerID" type="string" />  
                <attribute name="OrderList" type="IDREFS" />  
            </complexType>  
 </schema>'  
go  
declare @x xml(SC)  
set @x='<CustOrders:Customers xmlns:CustOrders="Customers">  
                <Customer CustomerID="C1" OrderList="OrderA OrderB"  >  
                              <spouse>Jenny</spouse>  
                                <Order OrderID="OrderA"><OrderValue>11</OrderValue></Order>  
                                <Order OrderID="OrderB"><OrderValue>22</OrderValue></Order>  
  
                </Customer>  
                <Customer CustomerID="C2" OrderList="OrderC OrderD" >  
                                <spouse>John</spouse>  
                                <Order OrderID="OrderC"><OrderValue>33</OrderValue></Order>  
                                <Order OrderID="OrderD"><OrderValue>44</OrderValue></Order>  
  
                        </Customer>  
                <Customer CustomerID="C3"  OrderList="OrderE OrderF" >  
                                <spouse>Jane</spouse>  
                                <Order OrderID="OrderE"><OrderValue>55</OrderValue></Order>  
                                <Order OrderID="OrderF"><OrderValue>55</OrderValue></Order>  
                </Customer>  
                <Customer CustomerID="C4"  OrderList="OrderG"  >  
                                <spouse>Tim</spouse>  
                                <Order OrderID="OrderG"><OrderValue>66</OrderValue></Order>  
                        </Customer>  
                <Customer CustomerID="C5"  >  
                </Customer>  
                <Customer CustomerID="C6" >  
                </Customer>  
                <Customer CustomerID="C7"  >  
                </Customer>  
</CustOrders:Customers>'  
  
select @x.query(' declare namespace CustOrders="Customers";   
 data(CustOrders:Customers/Customer[1]/@OrderList)[1] instance of xs:IDREF ? ') as XML_result  
```  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 制限事項は次のとおりです。  
  
-   **スキーマ要素 ()** および **スキーマ属性 ()** のシーケンス型は、演算子との比較ではサポートされていません `instance of` 。  
  
-   たとえば、完全なシーケンス `(1,2) instance of xs:integer*` はサポートされていません。  
  
-   などの型名を指定する **要素 ()** シーケンス型の形式を使用する場合、 `element(ElementName, TypeName)` 型は疑問符 (?) で修飾する必要があります。 たとえば、`element(Title, xs:string?)` は要素が NULL であることを示します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、を使用した **xsi: nil** プロパティの実行時検出はサポートされていません `instance of` 。  
  
-   `Expression` の値が共用体型として型指定された要素または属性の値である場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、派生された型ではなく、値の型の派生元のプリミティブ型しか識別できません。 たとえば、 `e1` 静的な型 (xs: integer | xs: string) を持つように <> が定義されている場合、次のコードは False を返します。  
  
    ```  
    data(<e1>123</e1>) instance of xs:integer  
    ```  
  
     ただし、 `data(<e1>123</e1>) instance of xs:decimal` は True を返します。  
  
-   **処理命令 ()** と **ドキュメントノード ()** のシーケンス型では、引数のないフォームのみが許可されます。 たとえば、`processing-instruction()` は使用できますが、`processing-instruction('abc')` は使用できません。  
  
## <a name="cast-as-operator"></a>cast as 演算子  
 **Cast as** 式は、値を特定のデータ型に変換するために使用できます。 次に例を示します。  
  
```  
  
Expression cast as  AtomicType?  
```  
  
 では、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の後に疑問符 (?) が必要です `AtomicType` 。 たとえば、次のクエリに示すように、は `"2" cast as xs:integer?` 文字列値を整数に変換します。  
  
```  
declare @x xml  
set @x=''  
select @x.query('"2" cast as xs:integer?')  
```  
  
 次のクエリでは、 **data ()** は、ProductModelID 属性の型指定された値 (文字列型) を返します。 `cast as`演算子は、値を xs: integer に変換します。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD)  
SELECT CatalogDescription.query('  
   data(/PD:ProductDescription[1]/@ProductModelID) cast as xs:integer?  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 このクエリでは、 **データ ()** を明示的に使用する必要はありません。 `cast as`式は、入力式に対して暗黙的なアトミック化を実行します。  
  
### <a name="constructor-functions"></a>コンストラクター関数  
 Atomic 型コンストラクター関数を使用できます。 たとえば、演算子を使用する代わりに、 `cast as` `"2" cast as xs:integer?` 次の例に示すように、 **xs: integer ()** コンストラクター関数を使用できます。  
  
```  
declare @x xml  
set @x=''  
select @x.query('xs:integer("2")')  
```  
  
 次の例では、2000-01-01Z に等しい xs:date 型の値が返されます。  
  
```  
declare @x xml  
set @x=''  
select @x.query('xs:date("2000-01-01Z")')  
```  
  
 ユーザー定義の atomic 型には、コンストラクターを使用することもできます。 たとえば、XML データ型に関連付けられている XML スキーマコレクションで単純型を定義する場合、 **myType ()** コンストラクターを使用してその型の値を返すことができます。  
  
#### <a name="implementation-limitations"></a>実装の制限事項  
  
-   XQuery 式の **タイプ** には、"スイッチ"、" **キャスト**" **、および "** 処理" はサポートされていません。  
  
-   **キャスト** には疑問符 (?) が必要ですアトミック型の後。  
  
-   **xs: QName** はキャストの型としてサポートされていません。 代わりに **、拡張 QName** を使用してください。  
  
-   **xs: date**、 **xs: time**、および **xs: datetime** には、Z で示されるタイムゾーンが必要です。  
  
     タイムゾーンが指定されていないため、次のクエリは失敗します。  
  
    ```  
    DECLARE @var XML  
    SET @var = ''  
    SELECT @var.query(' <a>{xs:date("2002-05-25")}</a>')  
    go  
    ```  
  
     値に Z タイムゾーンインジケーターを追加すると、クエリが機能します。  
  
    ```  
    DECLARE @var XML  
    SET @var = ''  
    SELECT @var.query(' <a>{xs:date("2002-05-25Z")}</a>')  
    go  
    ```  
  
     結果を次に示します。  
  
    ```  
    <a>2002-05-25Z</a>  
    ```  
  
## <a name="see-also"></a>参照  
 [XQuery 式](../xquery/xquery-expressions.md)   
 [型システム &#40;XQuery&#41;](../xquery/type-system-xquery.md)  
  
  
