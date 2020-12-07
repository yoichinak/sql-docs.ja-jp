---
title: 'sql: column () 関数 (XQuery) |Microsoft Docs'
description: 'XQuery 関数 sql: column () を使用して xml 内部の XML 以外のリレーショナルデータをバインドし、リレーショナルデータと XML データをまとめる方法について説明します。'
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
- sql:column function
- sql:column() function
ms.assetid: e8f67bdf-b489-49a9-9d0f-2069c1750467
author: rothja
ms.author: jroth
ms.openlocfilehash: 55a38974ec5e85eeec58195c18edd1f6fb8b5cb4
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038068"
---
# <a name="xquery-extension-functions---sqlcolumn"></a>XQuery 拡張関数 - sql:column()
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  「 [Xml 内部のリレーショナルデータのバインド](../t-sql/xml/binding-relational-data-inside-xml-data.md)」で説明されているように、 [xml データ型のメソッド](../t-sql/xml/xml-data-type-methods.md)を使用して XQuery 内にリレーショナル値を公開する場合は、 **sql: column ()** 関数を使用できます。  
  
 たとえば、 [query () メソッド (xml データ型)](../t-sql/xml/query-method-xml-data-type.md) を使用して、 **xml 型の** 変数または列に格納されている xml インスタンスに対してクエリを指定します。 場合によっては、クエリで XML 以外の別の列の値を使用して、リレーショナルデータと XML データを結合することが必要になることもあります。 これを行うには、 **sql: column ()** 関数を使用します。  
  
 SQL 値は、対応する XQuery 値にマップされ、型は、対応する SQL 型に相当する XQuery 基本データ型になります。  
  
## <a name="syntax"></a>構文  
  
```  
  
sql:column("columnName")  
```  
  
## <a name="remarks"></a>解説  
 XQuery 内の **sql: column ()** 関数で指定された列への参照は、処理される行の列を参照することに注意してください。  
  
 では [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 、xml インスタンスを参照する**xml**ことができるのは、xml DML insert ステートメントのソース式のコンテキストだけです。それ以外の場合は **、XML**型または CLR ユーザー定義型の列を参照することはできません。  
  
 **Sql: column ()** 関数は、結合操作ではサポートされていません。 代わりに、適用操作を使用できます。  
  
## <a name="examples"></a>例  
  
### <a name="a-using-sqlcolumn-to-retrieve-the-relational-value-inside-xml"></a>A. sql:column() を使用して XML 内部のリレーショナル値を取得する  
 Xml の構築では、xml 以外のリレーショナル列から値を取得して XML およびリレーショナルデータをバインドする方法を次の例に示します。  
  
 このクエリでは、次の形式の XML が構築されます。  
  
```xml
<Product ProductID="771" ProductName="Mountain-100 Silver, 38" ProductPrice="3399.99" ProductModelID="19"   
  ProductModelName="Mountain 100" />  
```  
  
 構築された XML では、次の点に注意してください。  
  
-   **ProductID**、 **ProductName**、および**Productprice**属性値は、 **Product**テーブルから取得されます。  
  
-   **Productmodelid**属性の値は、 **productmodel**テーブルから取得されます。  
  
-   クエリをさらに興味深いものにするために、 **ProductModelName**属性の値は、 **Xml 型**の**catalogdescription**列から取得されます。 XML 製品モデルのカタログ情報はすべての製品モデルに対して格納されていないので、 `if` ステートメントは、存在する場合にのみ値を取得するために使用されます。  
  
    ```sql
    SELECT P.ProductID, CatalogDescription.query('  
    declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
           <Product   
               ProductID=       "{ sql:column("P.ProductID") }"  
               ProductName=     "{ sql:column("P.Name") }"  
               ProductPrice=    "{ sql:column("P.ListPrice") }"  
               ProductModelID= "{ sql:column("PM.ProductModelID") }" >  
               { if (not(empty(/pd:ProductDescription))) then  
                 attribute ProductModelName { /pd:ProductDescription[1]/@ProductModelName }  
                else   
                   ()  
    }  
            </Product>  
    ') as Result  
    FROM Production.ProductModel PM, Production.Product P  
    WHERE PM.ProductModelID = P.ProductModelID  
    AND   CatalogDescription is not NULL  
    ORDER By PM.ProductModelID  
    ```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   値を 2 つの異なるテーブルから取得するため、FROM 句で 2 つのテーブルを指定しています。 WHERE 句に定義された条件により結果をフィルター選択し、カタログの説明のある製品モデルの製品のみを取得しています。  
  
-   [XQuery プロローグ](../xquery/modules-and-prologs-xquery-prolog.md)内の**namespace**キーワードは、クエリ本文で使用される XML 名前空間プレフィックス "pd" を定義します。 テーブルの別名 "P" と "PM" は、クエリ自体の FROM 句で定義されていることに注意してください。  
  
-   Xml 内の XML 以外の値を取り込むには、 **sql: column ()** 関数を使用します。  
  
 結果の一部を次に示します。  
  
```  
ProductID               Result  
-----------------------------------------------------------------  
771         <Product ProductID="771"                   ProductName="Mountain-100 Silver, 38"   
                  ProductPrice="3399.99" ProductModelID="19"   
                  ProductModelName="Mountain 100" />  
...  
```  
  
 次のクエリでは、製品固有の情報を含む XML を構築します。 この情報には、ある特定の製品モデル (ProductModelID=19) に属するすべての製品について、ProductID、ProductName、ProductPrice、および取得可能な場合は ProductModelName が含まれます。 Xml は @x **xml** 型の変数に割り当てられます。  
  
```sql
declare @x xml  
SELECT @x = CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
       <Product   
           ProductID=       "{ sql:column("P.ProductID") }"  
           ProductName=     "{ sql:column("P.Name") }"  
           ProductPrice=    "{ sql:column("P.ListPrice") }"  
           ProductModelID= "{ sql:column("PM.ProductModelID") }" >  
           { if (not(empty(/pd:ProductDescription))) then  
             attribute ProductModelName { /pd:ProductDescription[1]/@ProductModelName }  
            else   
               ()  
}  
        </Product>  
')   
FROM Production.ProductModel PM, Production.Product P  
WHERE PM.ProductModelID = P.ProductModelID  
And P.ProductModelID = 19  
select @x  
```  
  
## <a name="see-also"></a>参照  
 [XQuery 拡張関数の SQL Server]()   
 [型指定された XML と型指定されていない XML の比較](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML データ &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XML データのインスタンスの作成](../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml データ型メソッド](../t-sql/xml/xml-data-type-methods.md)   
 [XML データ変更言語 &#40;XML DML&#41;](../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
