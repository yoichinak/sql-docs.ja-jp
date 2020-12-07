---
description: exist() メソッド (xml データ型)
title: exist() メソッド (xml データ型)
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- exist() method
- exist method
ms.assetid: a55b75e0-0a17-4787-a525-9b095410f7af
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1788db3b0baec4f9ab7279f13ff792e6d7764ea6
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "91117216"
---
# <a name="exist-method-xml-data-type"></a>exist() メソッド (xml データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  次のいずれかの状態を表す **bit** 型を返します。  
  
-   クエリ内の XQuery 式により、空以外の結果が返された場合は 1 (True)。 つまり、少なくとも 1 つの XML ノードが返されます。  
  
-   これにより、空の結果が返された場合は 0 (False)。  
  
-   NULL の場合、**xml**クエリの実行対象となるデータ型のインスタンスには、NULL が含まれています。  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
exist (XQuery)   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 XQuery  
 文字列リテラルの XQuery 式です。  
  
## <a name="remarks"></a>解説  
  
> [!NOTE]  
>  **exist()** メソッドは、空でない結果を返す XQuery 式に対して 1 を返します。 **exist()** メソッド内に **true()** 関数または **false()** 関数を指定した場合、**exist()** メソッドは 1 を返します。これは、**true()** 関数および **false()** 関数がブール値の True および False をそれぞれ返すためです (つまり、空でない結果が返されます)。 したがって、次の例に示すように **exist()** は 1 (True) を返します。  
  
```sql
DECLARE @x XML;  
SET @x='';  
SELECT @x.exist('true()');   
```  
  
## <a name="examples"></a>例  
 **exist()** メソッドを指定する例を次に示します。  
  
### <a name="example-specifying-the-exist-method-against-an-xml-type-variable"></a>例:xml 型の変数に対する exist() メソッドの指定  
 次の例の @x は **xml** 型の変数 (型指定されていない xml) です。また、@f は **exist()** メソッドにより返された値を格納する整数型の変数です。 **Exist()** メソッドは、XML インスタンスに格納されている日付の値が `2002-01-01` である場合に True (1) を返します。  
  
```sql  
DECLARE @x XML;  
DECLARE @f BIT;  
SET @x = '<root Somedate = "2002-01-01Z"/>';  
SET @f = @x.exist('/root[(@Somedate cast as xs:date?) eq xs:date("2002-01-01Z")]');  
SELECT @f;  
```  
  
 **exist()** メソッドで日付を比較する際は、次のことに注意してください。  
  
-   コード `cast as xs:date?` は、比較する値を **xs:date** 型にキャストします。  
  
-   **\@Somedate** 属性の値は型指定されません。 この値は、比較するときに右側の比較対象の型である **xs:date** 型に暗黙的にキャストされます。  
  
-   **cast as xs:date()** の代わりに、**xs:date()** コンストラクター関数を使用できます。 詳細については、「[コンストラクター関数 &#40;XQuery&#41;](../../xquery/constructor-functions-xquery.md)」を参照してください。  
  
 次の例は、1 つ前の例と似ていますが、<`Somedate`> 要素が含まれている点が異なります。  
  
```sql
DECLARE @x XML;  
DECLARE @f BIT;  
SET @x = '<Somedate>2002-01-01Z</Somedate>';  
SET @f = @x.exist('/Somedate[(text()[1] cast as xs:date ?) = xs:date("2002-01-01Z") ]')  
SELECT @f;  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   **text()** メソッドは、型指定されていない値 `2002-01-01` が含まれたテキスト ノードを返します (この値の XQuery の型は **xdt:untypedAtomic** です)。この場合、暗黙的なキャストはサポートされないので、この型指定された値は明示的に **x** 型から **xsd:date** 型にキャストする必要があります。  
  
### <a name="example-specifying-the-exist-method-against-a-typed-xml-variable"></a>例:型指定された xml 型の変数に対する exist() メソッドの指定  
 次の例では、**xml** 型の変数に対する **exist()** メソッドの使用方法について説明します。 この例で使用する変数は、スキーマ名前空間コレクション名 `ManuInstructionsSchemaCollection` を指定しているため、型指定された XML 変数です。  
  
 この例では、まず製造手順書ドキュメントを変数に代入してから、**exist()** メソッドを使用して、このドキュメントに **LocationID** 属性の値が 50 の <`Location`> 要素が含まれているかどうかを調べます。  
  
 @x 変数に対して指定された **exist()** メソッドは、製造手順書ドキュメントに `LocationID=50` の <`Location`> 要素が含まれている場合、1 (True) を返します。 それ以外の場合は 0 (False) を返します。  
  
```sql
DECLARE @x XML (Production.ManuInstructionsSchemaCollection);  
SELECT @x=Instructions  
FROM Production.ProductModel  
WHERE ProductModelID=67;  
--SELECT @x  
DECLARE @f INT;  
SET @f = @x.exist(' declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
    /AWMI:root/AWMI:Location[@LocationID=50]  
');  
SELECT @f;  
```  
  
### <a name="example-specifying-the-exist-method-against-an-xml-type-column"></a>例:xml 型の列に対する exist() メソッドの指定  
 次のクエリでは、仕様書である <`Specifications`> 要素がカタログの説明に含まれていない製品モデル ID を取得します。  
  
```sql
SELECT ProductModelID, CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
    declare namespace  pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /pd:ProductDescription[not(pd:Specifications)]'  
    ) = 1;  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   WHERE 句では、xml 型の **CatalogDescription** 列に対して指定された条件を満たす行のみが **ProductDescription** テーブルから選択されます。  
  
-   WHERE 句の **exist()** メソッドは、XML に <`Specifications`> 要素が含まれていない場合、1 (True) を返します。 [not() 関数 (XQuery)](../../xquery/functions-on-boolean-values-not-function.md) が使用されていることに注意してください。  
  
-   [sql:column() 関数 (XQuery)](../../xquery/xquery-extension-functions-sql-column.md) を使用して、XML 以外の列から値を取得しています。  
  
-   このクエリでは、空の行セットが返されます。  
  
 上のクエリでは、xml データ型の **query()** メソッドと **exist()** メソッドが指定されています。また、これら両方のメソッドのクエリのプロローグで、同じ名前空間が宣言されています。 この場合、WITH XMLNAMESPACES を使用してプレフィックスを宣言し、そのプレフィックスをこのクエリに使用できます。  
  
```sql
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[not(pd:Specifications)]'  
    ) = 1;  
```  
  
## <a name="see-also"></a>参照  
 [WITH XMLNAMESPACES を使用したクエリへの名前空間の追加](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [型指定された XML と型指定されていない XML の比較](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML データのインスタンスの作成](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml データ型メソッド](../../t-sql/xml/xml-data-type-methods.md)   
 [XML データ変更言語 &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
