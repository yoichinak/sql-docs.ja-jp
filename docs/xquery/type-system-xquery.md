---
title: 型システム (XQuery) |Microsoft Docs
description: XML スキーマの組み込み型と、xpath データ型の名前空間で定義されている型を含む、XQuery 型システムについて説明します。
ms.custom: ''
ms.date: 08/10/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sequence [XQuery]
- type system [XQuery]
- typed values [XQuery]
- XQuery, sequence
- string values [XQuery]
- XQuery, XPath data type namespace
- xdt prefix [XML in SQL Server]
- XQuery, type system
- built-in XML schema types [SQL Server]
- xs prefix [XML in SQL Server]
ms.assetid: 22d6f861-d058-47ee-b550-cbe9092dcb12
author: rothja
ms.author: jroth
ms.openlocfilehash: a92b26642f5759044233d5d63b5a432ee5fe426c
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100352840"
---
# <a name="type-system-xquery"></a>型システム (XQuery)
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  XQuery は、スキーマ型の厳密に型指定された言語であり、型指定されていないデータに対して弱い型指定の言語です。 XQuery の定義済みの型には、次のものがあります。  
  
-   名前空間内の XML スキーマの組み込み型 **http://www.w3.org/2001/XMLSchema** 。  
  
-   名前空間で定義されている型 **http://www.w3.org/2004/07/xpath-datatypes** 。  
  
 このトピックでは、次の内容についても説明します。  
  
-   型指定された値とノードの文字列値。  
  
-   [データ関数は xquery&#41;を &#40;](../xquery/data-accessor-functions-data-xquery.md) 、 [String 関数は xquery&#41;&#40;](../xquery/data-accessor-functions-string-xquery.md)ます。  
  
-   式によって返されるシーケンスの型と一致します。  
  
## <a name="built-in-types-of-xml-schema"></a>XML スキーマの組み込み型  
 XML スキーマの組み込み型には、xs という定義済みの名前空間プレフィックスがあります。 これらの型には、 **xs: integer** や **xs: string** などがあります。 これらの組み込み型はすべてサポートされます。 これらの型は、XML スキーマコレクションを作成するときに使用できます。  
  
 型指定された XML のクエリを実行するとき、ノードの静的および動的な型は、クエリの対象の列または変数に関連付けられた XML スキーマ コレクションによって決まります。 静的および動的な型の詳細については、「 [式コンテキスト」と「クエリの評価 &#40;XQuery&#41;](../xquery/expression-context-and-query-evaluation-xquery.md)」を参照してください。 たとえば、次のクエリは、型指定された **xml** 列 () に対して指定され `Instructions` ます。 この式では、を使用し `instance of` て、返される属性の型指定された値が型であることを確認し `LotSize` `xs:decimal` ます。  
  
```  
SELECT Instructions.query('  
   DECLARE namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   data(/AWMI:root[1]/AWMI:Location[@LocationID=10][1]/@LotSize)[1] instance of xs:decimal  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 この入力情報は、列に関連付けられている XML スキーマコレクションによって提供されます。  
  
## <a name="types-defined-in-xpath-data-types-namespace"></a>XPath データ型の名前空間で定義されている型  
 名前空間で定義されている型には、 **http://www.w3.org/2004/07/xpath-datatypes** 定義済みの **xdt** のプレフィックスがあります。 これらの型には次のものが適用されます。  
  
-   XML スキーマ コレクションを作成しているときは、これらの型を使用できません。 これらの型は XQuery 型システムで使用され、 [xquery と静的](../xquery/xquery-and-static-typing.md)な型指定に使用されます。 **Xdt** 名前空間の atomic 型 ( **Xdt: untypedAtomic** など) にキャストできます。  
  
-   型指定されていない XML に対してクエリを実行する場合、要素ノードの静的および動的な型は **xdt:** 型指定されていません。また、属性値の型は **Xdt: untypedAtomic** です。 **Query ()** メソッドの結果により、型指定されていない XML が生成されます。 これは、XML ノードが **xdt: 型** 指定されていないと **Xdt: untypedAtomic** としてそれぞれ返されることを意味します。  
  
-   **Xdt: dayTimeDuration** および **Xdt: yearMonthDuration** 型はサポートされていません。  
  
 次の例では、型指定されていない XML 変数に対してクエリを指定しています。 式、) は、 `data(/a[1]` 1 つのアトミック値のシーケンスを返します。 関数は、 `data()` 要素の型指定された値を返し `<a>` ます。 クエリ対象の XML は型指定されていないので、返される値は `xdt:untypedAtomic` 型です。 したがって、は `instance of` true を返します。  
  
```  
DECLARE @x xml  
SET @x='<a>20</a>'  
SELECT @x.query( 'data(/a[1]) instance of xdt:untypedAtomic' )  
```  
  
 次の例の式 (`/a[1]`) は、型指定された値を取得するのではなく、要素 `<a>` という 1 つの要素のシーケンスを返します。 この式では、 `instance of` 要素テストを使用して、式によって返される値がの要素ノードであることを確認し `xdt:untyped type` ます。  
  
```  
DECLARE @x xml  
SET @x='<a>20</a>'  
-- Is this an element node whose name is "a" and type is xdt:untyped.  
SELECT @x.query( '/a[1] instance of element(a, xdt:untyped?)')  
-- Is this an element node of type xdt:untyped.  
SELECT @x.query( '/a[1] instance of element(*, xdt:untyped?)')  
-- Is this an element node?  
SELECT @x.query( '/a[1] instance of element()')  
```  
  
> [!NOTE]  
>  型指定された XML インスタンスにクエリを実行して、クエリ式に parent 軸が含まれるときは、結果のノードの静的な型情報は使用できなくなります。 ただし、動的な型は引き続きノードに関連付けられています。  
  
## <a name="typed-value-vs-string-value"></a>型指定された値と文字列値  
 すべてのノードには、型指定された値と文字列値があります。 型指定された XML データの場合、クエリ対象の列または変数に関連付けられている XML スキーマコレクションによって、型指定された値の型が提供されます。 型指定されていない XML データの場合、型指定された値の型は **xdt: untypedAtomic** になります。  
  
 **Data ()** 関数または **string ()** 関数を使用すると、ノードの値を取得できます。  
  
-   [データ関数 &#40;XQuery&#41;](../xquery/data-accessor-functions-data-xquery.md)は、ノードの型指定された値を返します。  
  
-   [String 関数 &#40;XQuery&#41;](../xquery/data-accessor-functions-string-xquery.md)は、ノードの文字列値を返します。  
  
 次の XML スキーマコレクションで `root` は、整数型の <> 要素が定義されています。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" type="integer"/>  
</schema>'  
GO  
```  
  
 次の例の式では、最初に `/root[1]` の型指定された値を取得してから、その値に `3` を加算しています。  
  
```  
DECLARE @x xml(SC)  
SET @x='<root>5</root>'  
SELECT @x.query('data(/root[1]) + 3')  
```  
  
 次の例では、式の `string(/root[1])` から文字列型の値が返されるので、式が失敗します。 この値は、オペランドとして数値型の値のみを受け取る算術演算子に渡されます。  
  
```  
-- Fails because the argument is string type (must be numeric primitive type).  
DECLARE @x xml(SC)  
SET @x='<root>5</root>'  
SELECT @x.query('string(/root[1]) + 3')  
```  
  
 次の例では、`LaborHours` 属性の合計を計算しています。 関数は、 `data()` `LaborHours` 製品モデルのすべての <> 要素から属性の型指定された値を取得し `Location` ます。 列に関連付けられている XML スキーマに従って `Instruction` 、 `LaborHours` は **xs: decimal** 型です。  
  
```  
SELECT Instructions.query('   
DECLARE namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
             sum(data(//AWMI:Location/@LaborHours))   
') AS Result   
FROM Production.ProductModel   
WHERE ProductModelID=7  
```  
  
 このクエリでは、結果として12.75 が返されます。  
  
> [!NOTE]  
>  この例での **data ()** 関数の明示的な使用は、例示のみを目的としています。 指定されていない場合、 **sum ()** は、ノードの型指定された値を抽出するために **data ()** 関数を暗黙的に適用します。  
  
## <a name="see-also"></a>参照  
 [SQL Server プロファイラーのテンプレートと権限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [XQuery の基礎](../xquery/xquery-basics.md)  
  
  
