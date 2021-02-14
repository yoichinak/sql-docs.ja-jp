---
title: パス式のステップ | で述語を指定するMicrosoft Docs
description: XML ノードシーケンスをフィルター処理するために、XQuery パス式の軸ステップで述語を指定する方法について説明します。
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
- predicates [XQuery]
- qualifiers [XQuery]
- path expressions [XQuery]
ms.assetid: 2660ceca-b8b4-4a1f-98a0-719ad5f89f81
author: rothja
ms.author: jroth
ms.openlocfilehash: ef2625be70c2af44f4a45ba00302b3d26afc101d
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100339943"
---
# <a name="path-expressions---specifying-predicates"></a>パス式 - 述語の指定
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  トピック「 [XQuery のパス式](../xquery/path-expressions-xquery.md)」で説明したように、パス式の軸ステップには、次のコンポーネントが含まれています。  
  
-   [軸](../xquery/path-expressions-specifying-axis.md)。  
  
-   ノードテスト。 詳細については、「 [パス式のステップでのノードテストの指定](../xquery/path-expressions-specifying-node-test.md)」を参照してください。  
  
-   0個以上の述語。 これは省略可能です。  
  
 省略可能な述語は、パス式の軸ステップの3番目の部分です。  
  
## <a name="predicates"></a>述語  
 述語は、指定されたテストを適用することによってノードシーケンスをフィルター処理するために使用されます。 述語式は、角かっこで囲み、パス式の最後のノードにバインドされます。  
  
 たとえば、次に示すように、 **xml** データ型の SQL パラメーター値 (x) が宣言されているとします。  
  
```  
declare @x xml  
set @x = '  
<People>  
  <Person>  
    <Name>John</Name>  
    <Age>24</Age>  
  </Person>  
  <Person>  
    <Name>Goofy</Name>  
    <Age>54</Age>  
  </Person>  
  <Person>  
    <Name>Daffy</Name>  
    <Age>30</Age>  
  </Person>  
</People>  
'  
```  
  
 この場合、次の式は、述語の値 [1] が 3 つの異なるノード レベルで使用されていますが、いずれも有効です。  
  
```  
select @x.query('/People/Person/Name[1]')  
select @x.query('/People/Person[1]/Name')  
select @x.query('/People[1]/Person/Name')  
```  
  
 各ケースでは、述語は、適用されるパス式のノードにバインドされることに注意してください。 たとえば、最初のパス式は、 `Name` 各/People/Person ノード内の最初の <> 要素を選択し、指定された XML インスタンスを使用して、次の値を返します。  
  
```  
<Name>John</Name><Name>Goofy</Name><Name>Daffy</Name>  
```  
  
 ただし、2番目のパス式は、 `Name` 最初の/People/Person ノードの下にあるすべての <> 要素を選択します。 したがって、次の結果を返します。  
  
```  
<Name>John</Name>  
```  
  
 また、かっこを使用して、述語の評価の順序を変更することもできます。 たとえば、次の式では、述語 [1] と (/People/Person/Name) というパスを分離するために、かっこが使用されています。  
  
```  
select @x.query('(/People/Person/Name)[1]')  
```  
  
 この例では、述語が適用される順序が変更されます。 これは、囲まれたパスが最初に評価された (/People/Person/Name) ため、囲まれたパスに一致したすべてのノードを含むセットに述語 [1] 演算子が適用されるためです。 かっこを使用しない場合、最初のパス式の例と同様に、[1] がノードテストとして適用されるという点で、操作の順序が異なり `child::Name` ます。  
  
### <a name="quantifiers-and-predicates"></a>量指定子と述語  
 量指定子を使用して、述語自体の中かっこ内に複数回追加することができます。 たとえば、前の例を使用すると、次の式は複雑な述語のサブ式内で複数の量化子を使用する有効な式です。  
  
```  
select @x.query('/People/Person[contains(Name[1], "J") and xs:integer(Age[1]) < 40]/Name/text()')  
```  
  
 述語式の結果はブール値に変換され、述語の真偽値として参照されます。 結果で返されるのは、述語の真偽値が True になっているシーケンス内のノードだけです。 その他のすべてのノードは破棄されます。  
  
 たとえば、次のパス式では、2 番目のステップに述語があります。  
  
```  
/child::root/child::Location[attribute::LocationID=10]  
```  
  
 この述語によって指定された条件は、すべての <> 要素ノードの子に適用され `Location` ます。 結果として、LocationID 属性値が 10 であるワーク センターの場所のみが返されます。  
  
 上記のパス式は、次の SELECT ステートメント内で実行されます。  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
 /child::AWMI:root/child::AWMI:Location[attribute::LocationID=10]  
')  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
### <a name="computing-predicate-truth-values"></a>述語の真偽値を計算する  
 述語の真偽値の判定には、XQuery の仕様に従い、次の規則が適用されます。  
  
1.  述語式の値が空のシーケンスの場合、述語の真偽値は False になります。  
  
     次に例を示します。  
  
    ```  
    SELECT Instructions.query('  
    declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
     /child::AWMI:root/child::AWMI:Location[attribute::LotSize]  
    ')  
    FROM Production.ProductModel  
    WHERE ProductModelID=7  
    ```  
  
     このクエリのパス式では、 `Location` LotSize 属性が指定されている <> 要素ノードだけが返されます。 述語が特定の <> に対して空のシーケンスを返す場合 `Location` 、そのワークセンターの場所は結果に返されません。  
  
2.  述語の値には、xs: integer、xs: Boolean、または node のみを指定でき \* ます。 ノードの \* 場合、述語はノードがある場合は True に、空のシーケンスの場合は False に評価されます。 その他の数値型 (double、float 型など) では、静的な型指定エラーが生成されます。 式の述語の真偽値は、結果として得られる整数がコンテキスト位置の値と等しい場合にのみ True になります。 また、整数リテラル値と **last ()** 関数のみが、フィルター処理されたステップ式のカーディナリティを1に減らします。  
  
     たとえば、次のクエリでは、<> 要素の3番目の子要素ノードが取得され `Features` ます。  
  
    ```  
    SELECT CatalogDescription.query('  
    declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
    declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
     /child::PD:ProductDescription/child::PD:Features/child::*[3]  
    ')  
    FROM Production.ProductModel  
    WHERE ProductModelID=19  
    ```  
  
     上のクエリに関して、次の点に注意してください。  
  
    -   式の 3 番目のステップは、値が 3 である述語式を指定しています。 したがって、この式の述語の真偽値は、コンテキストの位置が 3 であるノードに対してのみ True になります。  
  
    -   3番目の手順では、ノードテスト内のすべてのノードを示すワイルドカード文字 (*) も指定します。 ただし、述語により、ノードがフィルター処理され、3 番目の位置にあるノードのみが返されます。  
  
    -   このクエリは、 `Features` ドキュメントルートの <> 要素の子である <> 子要素の3番目の子要素ノードを返し `ProductDescription` ます。  
  
3.  述語式の値が Boolean 型の単純なデータ型値である場合、述語の真偽値は、述語式の値と同じになります。  
  
     たとえば、次のクエリは、顧客調査 XML インスタンスである xml インスタンスを保持する **xml 型の変数に対し** て指定されます。 このクエリは、子供がいる顧客を取得します。 このクエリでは、1に \<HasChildren> なり \</HasChildren> ます。  
  
    ```  
    declare @x xml  
    set @x='  
    <Survey>  
      <Customer CustomerID="1" >  
      <Age>27</Age>  
      <Income>20000</Income>  
      <HasChildren>1</HasChildren>  
      </Customer>  
      <Customer CustomerID="2" >  
      <Age>27</Age>  
      <Income>20000</Income>  
      <HasChildren>0</HasChildren>  
      </Customer>  
    </Survey>  
    '  
    declare @y xml  
    set @y = @x.query('  
      for $c in /child::Survey/child::Customer[( child::HasChildren[1] cast as xs:boolean ? )]  
      return   
          <CustomerWithChildren>  
              { $c/attribute::CustomerID }  
          </CustomerWithChildren>  
    ')  
    select @y  
    ```  
  
     上のクエリに関して、次の点に注意してください。  
  
    -   **For** ループの式には2つのステップがあり、2番目のステップは述語を指定します。 この述語の値はブール型の値です。 この値が True の場合、述語の真偽値も True になります。  
  
    -   このクエリは、 `Customer` \<Survey> ドキュメントルートの子要素の述語値が True である <> 子要素を返します。 結果を次に示します。  
  
        ```  
        <CustomerWithChildren CustomerID="1"/>   
        ```  
  
4.  述語式の値が、少なくとも1つのノードを含むシーケンスの場合、述語の真偽値は True になります。  
  
 たとえば、次のクエリでは、XML カタログの説明に、 `Features` **wm** プレフィックスに関連付けられている名前空間から、少なくとも1つの機能 (<> 要素の子要素) が含まれている製品モデルの productmodelid を取得します。  
  
```  
SELECT ProductModelID  
FROM   Production.ProductModel  
WHERE CatalogDescription.exist('  
             declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
             declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
             /child::PD:ProductDescription/child::PD:Features[wm:*]  
             ') = 1  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   WHERE 句では、 [exist () メソッド (XML データ型)](../t-sql/xml/exist-method-xml-data-type.md)を指定します。  
  
-   **Exist ()** メソッド内のパス式は、2番目のステップで述語を指定します。 述語式が少なくとも 1 つの機能のシーケンスを返す場合、この述語式の真偽値は True になります。 この場合、 **exist ()** メソッドは True を返すため、ProductModelID が返されます。  
  
## <a name="static-typing-and-predicate-filters"></a>静的な型指定フィルターおよび述語フィルター  
 述語は、静的に推定される式の型にも影響する場合があります。 整数リテラル値と **last ()** 関数は、フィルター処理されたステップ式のカーディナリティを最大で1に減らします。  
  
  
