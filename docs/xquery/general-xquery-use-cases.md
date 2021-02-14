---
title: 一般的な XQuery ユースケース |Microsoft Docs
description: 製品カタログの特定のデータの検索、取得、一覧表示など、一般的な XQuery の使用例をいくつか紹介します。
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
- XQuery, general usage cases
ms.assetid: 5187c97b-6866-474d-8bdb-a082634039cc
author: rothja
ms.author: jroth
ms.openlocfilehash: 62fa5c7bba9133c9a8b0098142d97fdd422c47ba
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100341913"
---
# <a name="general-xquery-use-cases"></a>XQuery の一般的な使用例
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  このトピックでは、XQuery の使用例について説明します。  
  
## <a name="examples"></a>例  
  
### <a name="a-query-catalog-descriptions-to-find-products-and-weights"></a>A. 製品と重量を検索するためのカタログ説明のクエリ  
 次のクエリでは、製品カタログの説明に製品モデル ID と重量が含まれている場合、これらの情報を返します。 このクエリでは、次の形式の XML が構築されます。  
  
```  
<Product ProductModelID="...">  
  <Weight>...</Weight>  
</Product>  
```  
  
 クエリは次のとおりです。  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  <Product  ProductModelID="{ (/p1:ProductDescription/@ProductModelID)[1] }">  
     {   
       /p1:ProductDescription/p1:Specifications/Weight   
     }   
  </Product>  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not null  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   XQuery プロローグ内の **namespace** キーワードは、クエリ本文で使用される名前空間プレフィックスを定義します。  
  
-   クエリ本文で、必要な XML が構築されます。  
  
-   WHERE 句では、 **exist ()** メソッドを使用して、製品カタログの説明を含む行のみを検索します。 つまり、<> 要素を含む XML です `ProductDescription` 。  
  
 結果を次に示します。  
  
```  
<Product ProductModelID="19"/>  
<Product ProductModelID="23"/>   
<Product ProductModelID="25"/>   
<Product ProductModelID="28"><Weight>Varies with size.</Weight></Product>  
<Product ProductModelID="34"/>  
<Product ProductModelID="35"/>  
```  
  
 次のクエリでは、同じ情報を取得しますが、カタログの説明に重み、<`Weight`> 要素、仕様、<> 要素を含む製品モデルに対してのみ取得し `Specifications` ます。 この例では、WITH XMLNAMESPACES を使用して、pd プレフィックスとその名前空間バインドを宣言しています。 この方法では、binding は **query ()** メソッドと **exist ()** メソッドの両方で記述されていません。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT CatalogDescription.query('  
          <Product  ProductModelID="{ (/pd:ProductDescription/@ProductModelID)[1] }">  
                 {   
                      /pd:ProductDescription/pd:Specifications/Weight   
                 }   
          </Product>  
') as x  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription/pd:Specifications//Weight ') = 1  
```  
  
 上記のクエリでは、WHERE 句で **xml** データ型の **exist ()** メソッドが、 `Weight` <> 要素に <> 要素があるかどうかを確認し `Specifications` ます。  
  
### <a name="b-find-product-model-ids-for-product-models-whose-catalog-descriptions-include-front-angle-and-small-size-pictures"></a>B. カタログの説明に正面からの小さな製品写真が含まれる製品モデルの製品モデル ID の検索  
 XML 製品カタログの説明には、製品の画像、<> 要素が含まれてい `Picture` ます。 各写真には、いくつかのプロパティがあります。 これには、画像の角度、<`Angle`> 要素、サイズ、<> 要素が含まれ `Size` ます。  
  
 カタログの説明に正面と小さいサイズの画像が含まれる製品モデルの場合、クエリでは次の形式の XML が構築されます。  
  
```  
< Product ProductModelID="...">  
  <Picture>  
    <Angle>front</Angle>  
    <Size>small</Size>  
  </Picture>  
</Product>  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT CatalogDescription.query('  
   <pd:Product  ProductModelID="{ (/pd:ProductDescription/@ProductModelID)[1] }">  
      <Picture>  
         {  /pd:ProductDescription/pd:Picture/pd:Angle }   
         {  /pd:ProductDescription/pd:Picture/pd:Size }   
      </Picture>  
   </pd:Product>  
') as Result  
FROM  Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription/pd:Picture') = 1  
AND   CatalogDescription.value('(/pd:ProductDescription/pd:Picture/pd:Angle)[1]', 'varchar(20)')  = 'front'  
AND   CatalogDescription.value('(/pd:ProductDescription/pd:Picture/pd:Size)[1]', 'varchar(20)')  = 'small'  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   WHERE 句では、 **exist ()** メソッドを使用して、<> 要素を持つ製品カタログの説明を含む行のみを取得し `Picture` ます。  
  
-   WHERE 句では **value ()** メソッドを2回使用して、<`Size`> と <> 要素の値を比較し `Angle` ます。  
  
 結果の一部を次に示します。  
  
```  
<p1:Product   
  xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
  ProductModelID="19">  
  <Picture>  
    <p1:Angle>front</p1:Angle>  
    <p1:Size>small</p1:Size>  
  </Picture>  
</p1:Product>  
...  
```  
  
### <a name="c-create-a-flat-list-of-the-product-model-name-and-feature-pairs-with-each-pair-enclosed-in-the-features-element"></a>C. 製品モデルの名前と特徴のペアの単純なリストを作成します。各ペアは要素で囲まれています。 \<Features>  
 製品モデルカタログの説明では、XML にいくつかの製品機能が含まれています。 これらの機能はすべて <> 要素に含まれてい `Features` ます。 このクエリでは、 [Xml 構築 (XQuery)](../xquery/xml-construction-xquery.md) を使用して、必要な xml を構築します。 中かっこ内の式は、結果に置き換えられます。  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  for $pd in /p1:ProductDescription,  
   $f in $pd/p1:Features/*  
  return  
   <Feature>  
     <ProductModelName> { data($pd/@ProductModelName) } </ProductModelName>  
     { $f }  
  </Feature>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   $pd/p1: Features/* は、<> の子要素ノードだけを返します `Features` が、$pd/p1: features/node () はすべてのノードを返します。 返されるノードには、要素ノード、テキスト ノード、処理命令、コメントがあります。  
  
-   2つの FOR ループによって、製品名と個々の特徴が返されるデカルト積が生成されます。  
  
-   **ProductName** は属性です。 このクエリで構築された XML では、この属性を要素として返します。  
  
 結果の一部を次に示します。  
  
```  
<Feature>  
 <ProductModelName>Mountain 100</ProductModelName>  
 <ProductModelID>19</ProductModelID>  
 <p1:Warranty   
   xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
 </p1:Warranty>  
</Feature>  
<Feature>  
 <ProductModelName>Mountain 100</ProductModelName>  
 <ProductModelID>19</ProductModelID>  
 <p2:Maintenance xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p2:NoOfYears>10</p2:NoOfYears>  
    <p2:Description>maintenance contact available through your dealer   
           or any AdventureWorks retail store.</p2:Description>  
    </p2:Maintenance>  
</Feature>  
...  
...      
```  
  
### <a name="d-from-the-catalog-description-of-a-product-model-list-the-product-model-name-model-id-and-features-grouped-inside-a-product-element"></a>D. 製品モデルのカタログの説明から製品モデルの名前、モデル ID、および要素内にグループ化された機能を一覧表示します。 \<Product>  
 次のクエリでは、製品モデルのカタログの説明に格納されている情報を使用して、製品モデルの名前、モデル ID、および要素内にグループ化された機能を一覧表示し \<Product> ます。  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
     declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>  
         <ProductModelName>   
           { data(/pd:ProductDescription/@ProductModelName) }   
         </ProductModelName>  
         <ProductModelID>   
           { data(/pd:ProductDescription/@ProductModelID) }   
         </ProductModelID>  
         { /pd:ProductDescription/pd:Features/* }  
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 結果の一部を次に示します。  
  
```  
<Product>  
  <ProductModelName>Mountain 100</ProductModelName>  
  <ProductModelID>19</ProductModelID>  
  <p1:Warranty>... </p1:Warranty>  
  <p2:Maintenance>...  </p2:Maintenance>  
  <p3:wheel xmlns:p3="https://www.adventure-works.com/schemas/OtherFeatures">High performance wheels.</p3:wheel>  
  <p4:saddle xmlns:p4="https://www.adventure-works.com/schemas/OtherFeatures">  
    <p5:i xmlns:p5="http://www.w3.org/1999/xhtml">Anatomic design</p5:i> and made from durable leather for a full-day of riding in comfort.</p4:saddle>  
  <p6:pedal xmlns:p6="https://www.adventure-works.com/schemas/OtherFeatures">  
    <p7:b xmlns:p7="http://www.w3.org/1999/xhtml">Top-of-the-line</p7:b> clipless pedals with adjustable tension.</p6:pedal>  
   ...  
```  
  
### <a name="e-retrieve-product-model-feature-descriptions"></a>E. 製品モデルの特徴の説明の取得  
 次のクエリでは、<の> 要素を含む XML を構築し `Product` ます。この要素に **は**、 **ProductModelName** 属性と、最初の2つの製品機能が含まれています。 具体的には、最初の2つの製品機能は、<> 要素の最初の2つの子要素 `Features` です。 その他の機能がある場合は、空の <`There-is-more/`> 要素を返します。  
  
```  
SELECT CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /pd:ProductDescription/@ProductModelID }  
          { /pd:ProductDescription/@ProductModelName }   
          {  
            for $f in /pd:ProductDescription/pd:Features/*[position()<=2]  
            return  
            $f   
          }  
          {  
            if (count(/pd:ProductDescription/pd:Features/*) > 2)  
            then <there-is-more/>  
            else ()  
          }   
     </Product>          
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not NULL  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   ...RETURN ループ構造は、最初の2つの製品の特徴を取得します。 **Position ()** 関数は、シーケンス内の要素の位置を検索するために使用されます。  
  
### <a name="f-find-element-names-from-the-product-catalog-description-that-end-with-ons"></a>F. 製品カタログの説明からの "ons" で終わる要素名の検索  
 次のクエリでは、カタログの説明を検索し、名前の `ProductDescription` 末尾が "on" である <> 要素内のすべての要素を返します。  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
     declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $pd in /p1:ProductDescription/*[substring(local-name(.),string-length(local-name(.))-2,3)="ons"]  
      return   
          <Root>  
             { $pd }  
          </Root>  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not NULL  
```  
  
 結果の一部を次に示します。  
  
```  
ProductModelID   Result  
-----------------------------------------  
         19        <Root>         
                     <p1:Specifications xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">          
                          ...         
                     </p1:Specifications>         
                   </Root>          
```  
  
### <a name="g-find-summary-descriptions-that-contain-the-word-aerodynamic"></a>G. "航空力学" という語を含む概要説明を検索します。  
 次のクエリでは、カタログの説明の概要説明に "Aerodynamic" という語を含む製品モデルを取得します。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
          <Prod >  
             { /pd:ProductDescription/@ProductModelID }  
             { /pd:ProductDescription/pd:Summary }  
          </Prod>  
 ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.value('  
     contains( string( (/pd:ProductDescription/pd:Summary)[1] ),"Aerodynamic")','bit') = 1  
```  
  
 SELECT クエリでは、 **xml** データ型の **query ()** メソッドと **value ()** メソッドが指定されていることに注意してください。 このため、2 つの異なるクエリ プロローグ内でそれぞれ名前空間の宣言を繰り返す手間を省き、クエリ内で使用されるプレフィックス pd を WITH XMLNAMESPACES を使用して一度だけ定義しています。  
  
 上のクエリに関して、次の点に注意してください。  
  
-   WHERE 句は、カタログの説明に <> 要素に "航空力学" という単語が含まれている行のみを取得するために使用され `Summary` ます。  
  
-   **Contains ()** 関数は、単語がテキストに含まれているかどうかを確認するために使用されます。  
  
-   **Xml** データ型の **value ()** メソッドは、 **contains ()** によって返された値を1に比較します。  
  
 結果を次に示します。  
  
```  
ProductModelID Result        
-------------- ------------------------------------------  
28     <Prod ProductModelID="28">  
        <pd:Summary xmlns:pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
       <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
         A TRUE multi-sport bike that offers streamlined riding and a  
         revolutionary design. Aerodynamic design lets you ride with the   
         pros, and the gearing will conquer hilly roads.</p1:p>  
       </pd:Summary>  
      </Prod>    
```  
  
### <a name="h-find-product-models-whose-catalog-descriptions-do-not-include-product-model-pictures"></a>H. カタログの説明に製品モデルの画像が含まれていない製品モデルを検索する  
 次のクエリでは、カタログの説明に <> 要素が含まれていない製品モデルの ProductModelIDs を取得し `Picture` ます。  
  
```  
SELECT  ProductModelID  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not NULL  
AND     CatalogDescription.exist('declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /p1:ProductDescription/p1:Picture  
') = 0  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   WHERE 句の **exist ()** メソッドが False (0) を返す場合、製品モデル ID が返されます。 それ以外の場合は返されません。  
  
-   すべての製品の説明には <の> 要素が含まれているため `Picture` 、この場合、結果セットは空になります。  
  
## <a name="see-also"></a>参照  
 [階層に関連する XQueries](../xquery/xqueries-involving-hierarchy.md)   
 [注文に関連する XQueries](../xquery/xqueries-involving-order.md)   
 [XQueries リレーショナルデータを処理する](../xquery/xqueries-handling-relational-data.md)   
 [XQuery での文字列検索](../xquery/string-search-in-xquery.md)   
 [XQuery での名前空間の処理](../xquery/handling-namespaces-in-xquery.md)   
 [WITH XMLNAMESPACES を使用したクエリへの名前空間の追加](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [XML データ &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 言語リファレンス &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
