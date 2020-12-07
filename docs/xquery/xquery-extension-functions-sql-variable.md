---
title: 'sql: variable () 関数 (XQuery) |Microsoft Docs'
description: 'Xquery の拡張機能である sql: variable () を使用して、XQuery 式内に SQL のリレーショナル値を含む変数を公開する方法について説明します。'
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sql:variable() function
- sql:variable function
ms.assetid: 6e2e5063-c1cf-4b5a-b642-234921e3f4f7
author: rothja
ms.author: jroth
ms.openlocfilehash: 6ed7dd109906b4cace6ed185b1842f9e9e7dedde
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037039"
---
# <a name="xquery-extension-functions---sqlvariable"></a>XQuery Extension Functions - sql:variable()
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  SQL リレーショナル値を含む変数を XQuery 式内部に公開します。  
  
## <a name="syntax"></a>構文  
  
```  
  
sql:variable("variableName") as xdt:anyAtomicType?  
```  
  
## <a name="remarks"></a>解説  
 「 [Xml 内部のリレーショナルデータのバインド](../t-sql/xml/binding-relational-data-inside-xml-data.md)」で説明したように、 [xml データ型のメソッド](../t-sql/xml/xml-data-type-methods.md) を使用して XQuery 内にリレーショナル値を公開するときに、この関数を使用できます。  
  
 たとえば、 [query () メソッド](../t-sql/xml/query-method-xml-data-type.md) を使用して、 **xml** データ型の変数または列に格納されている xml インスタンスに対してクエリを指定します。 また、場合によっては、リレーショナル データと XML データを一緒にするために、[!INCLUDE[tsql](../includes/tsql-md.md)] 変数の値 (パラメーター) をクエリで使用することもできます。 これを行うには、 **sql: variable** 関数を使用します。  
  
 SQL 値は、対応する XQuery 値にマップされ、型は、対応する SQL 型に相当する XQuery 基本データ型になります。  
  
 **Xml インスタンスは**、xml DML insert ステートメントのソース式のコンテキストでのみ参照できます。それ以外の場合、 **xml**型または共通言語ランタイム (CLR) ユーザー定義型の値を参照することはできません。  
  
## <a name="examples"></a>例  
  
### <a name="a-using-the-sqlvariable-function-to-bring-a-transact-sql-variable-value-into-xml"></a>A. Sql: variable () 関数を使用した Transact-sql 変数の値の XML への移動  
 次の例では、次の要素で構成される XML インスタンスを作成します。  
  
-   XML 以外の列の値 (`ProductID`)。 [Sql: column () 関数](../xquery/xquery-extension-functions-sql-column.md)は、この値を XML にバインドするために使用されます。  
  
-   他のテーブルの XML 以外の列の値 (`ListPrice`)。 この場合 `sql:column()` も、を使用して、この値を XML にバインドします。  
  
-   [!INCLUDE[tsql](../includes/tsql-md.md)] 変数の値 (`DiscountPrice`)。 `sql:variable()`この値を XML にバインドするには、メソッドを使用します。  
  
-   `ProductModelName` **Xml**型の列の値 () を使用して、クエリをさらに興味深いものにします。  
  
 クエリは次のとおりです。  
  
```sql
DECLARE @price money  
  
SET @price=2500.00  
SELECT ProductID, Production.ProductModel.ProductModelID,CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  
       <Product   
           ProductID="{ sql:column("Production.Product.ProductID") }"  
           ProductModelID= "{ sql:column("Production.Product.ProductModelID") }"  
           ProductModelName="{/pd:ProductDescription[1]/@ProductModelName }"  
           ListPrice="{ sql:column("Production.Product.ListPrice") }"  
           DiscountPrice="{ sql:variable("@price") }"  
        />')   
FROM Production.Product   
JOIN Production.ProductModel  
ON Production.Product.ProductModelID = Production.ProductModel.ProductModelID  
WHERE ProductID=771  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   メソッド内の XQuery により、 `query()` XML が構築されます。  
  
-   `namespace`キーワードは、 [XQuery プロローグ](../xquery/modules-and-prologs-xquery-prolog.md)で名前空間プレフィックスを定義するために使用されます。 これは、 `ProductModelName` 属性値が、 `CatalogDescription xml` 関連付けられているスキーマを持つ型列から取得されるためです。  
  
 結果を次に示します。  
  
```xml
<Product ProductID="771" ProductModelID="19"   
         ProductModelName="Mountain 100"   
         ListPrice="3399.99" DiscountPrice="2500" />  
```  
  
## <a name="see-also"></a>参照  
 [XQuery 拡張関数の SQL Server](./xquery-extension-functions-sql-column.md)   
 [型指定された XML と型指定されていない XML の比較](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML データ &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XML データのインスタンスの作成](../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml データ型メソッド](../t-sql/xml/xml-data-type-methods.md)   
 [XML データ変更言語 &#40;XML DML&#41;](../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
