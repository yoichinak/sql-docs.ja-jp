---
title: 文字列長関数 (XQuery) |Microsoft Docs
description: XQuery 関数の文字列長 () の使用方法について説明します。
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
- string-length function
- fn:string-length function
ms.assetid: 7cd69c8b-cf2c-478c-b9a3-e0e14e1aa8aa
author: rothja
ms.author: jroth
ms.openlocfilehash: 588e3a4dc19d502da07d23971aea7b987e49a8ea
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100344997"
---
# <a name="functions-on-string-values---string-length"></a>文字列値に使用する関数 - string-length
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  文字列の長さを文字数で返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:string-length() as xs:integer  
fn:string-length($arg as xs:string?) as xs:integer  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 長さが計算されるソース文字列。  
  
## <a name="remarks"></a>Remarks  
 *$Arg* の値が空のシーケンスの場合、 **xs: integer** 値0が返されます。  
  
 XQuery 関数におけるサロゲート ペアの動作は、データベースの互換性レベルに左右されます。 互換性レベルが110以上の場合は、各サロゲートペアが1文字としてカウントされます。 互換性レベルがこれ未満の場合は、2 文字としてカウントされます。 詳細については、「 [ALTER DATABASE 互換性レベル &#40;transact-sql&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) と [照合順序と Unicode のサポート](../relational-databases/collations/collation-and-unicode-support.md)」を参照してください。  
  
 値にサロゲート文字 2 文字で表される 4 バイトの Unicode 文字が含まれている場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] はサロゲート文字 1 つを 1 文字として計算します。  
  
 パラメーターのない **文字列長 ()** は、述語内でのみ使用できます。 たとえば、次のクエリでは、<`ROOT`> 要素が返されます。  
  
```  
DECLARE @x xml;  
SET @x='<ROOT>Hello</ROOT>';  
SELECT @x.query('/ROOT[string-length()=5]');  
```  
  
## <a name="supplementary-characters-surrogate-pairs"></a>補助文字 (サロゲート ペア)  
 XQuery 関数のサロゲートペアの動作は、データベースの互換性レベルと、場合によっては、関数の既定の名前空間 URI に依存します。 詳細については、「 [SQL Server 2016 のデータベースエンジン機能の重大な変更](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)」の「XQuery 関数はサロゲート対応」を参照してください。 「 [ALTER DATABASE Compatibility Level &#40;transact-sql&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) 」と「 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)」も参照してください。  
  
## <a name="examples"></a>使用例  
 このトピックでは、AdventureWorks データベースのさまざまな **xml** 型の列に格納されている xml インスタンスに対して XQuery の例を示します。  
  
### <a name="a-using-the-string-length-xquery-function-to-retrieve-products-with-long-summary-descriptions"></a>A. 文字列長 () の XQuery 関数を使用して、長い概要の説明を含む製品を取得する  
 概要説明が50文字を超える製品の場合、次のクエリでは、製品 ID、概要説明の長さ、および概要自体、<> 要素が取得され `Summary` ます。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' as pd)  
SELECT CatalogDescription.query('  
      <Prod ProductID= "{ /pd:ProductDescription[1]/@ProductModelID }" >  
       <LongSummary SummaryLength =   
           "{string-length(string( (/pd:ProductDescription/pd:Summary)[1] )) }" >  
           { string( (/pd:ProductDescription/pd:Summary)[1] ) }  
       </LongSummary>  
      </Prod>  
 ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.value('string-length( string( (/pd:ProductDescription/pd:Summary)[1]))', 'decimal') > 200;  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   WHERE 句の条件は、XML ドキュメントに格納されている概要説明が200文字を超える行のみを取得します。 [Value () メソッド (XML データ型)](../t-sql/xml/value-method-xml-data-type.md)を使用します。  
  
-   SELECT 句は、必要な XML のみを構築しています。 [Query () メソッド (xml データ型)](../t-sql/xml/query-method-xml-data-type.md)を使用して xml を構築し、xml ドキュメントからデータを取得するために必要な XQuery 式を指定します。  
  
 結果の一部を次に示します。  
  
```  
Result  
-------------------  
<Prod ProductID="19">  
      <LongSummary SummaryLength="214">Our top-of-the-line competition   
             mountain bike. Performance-enhancing options include the  
             innovative HL Frame, super-smooth front suspension, and   
             traction for all terrain.  
      </LongSummary>  
</Prod>  
...  
```  
  
### <a name="b-using-the-string-length-xquery-function-to-retrieve-products-whose-warranty-descriptions-are-short"></a>B. 文字列長 () の XQuery 関数を使用して、保証の説明が短い製品を取得する  
 保証の説明が20文字未満の製品の場合、次のクエリでは、製品 ID、長さ、保証の説明、および <> 要素自体を含む XML を取得し `Warranty` ます。  
  
 保証は、製品の機能の1つです。 省略可能な <`Warranty`> 子要素は <> 要素の後に続き `Features` ます。  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
      for   $ProdDesc in /pd:ProductDescription,  
            $pf in $ProdDesc/pd:Features/wm:Warranty  
      where string-length( string(($pf/wm:Description)[1]) ) < 20  
      return   
          <Prod >  
             { $ProdDesc/@ProductModelID }  
             <ShortFeature FeatureDescLength =   
                             "{string-length( string(($pf/wm:Description)[1]) ) }" >  
                 { $pf }  
             </ShortFeature>  
          </Prod>  
     ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription')=1;  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   **pd** および **wm** は、このクエリで使用される名前空間プレフィックスです。 これらは、クエリ対象のドキュメントで使用されている同じ名前空間を示します。  
  
-   XQuery は、入れ子になった FOR ループを指定します。 <> 要素の **Productmodelid** 属性を取得する必要があるため、outer for ループが必要です `ProductDescription` 。 内部 FOR ループは、保証機能の説明が20文字未満の製品のみを必要とするため、必須です。  
  
 結果の一部を次に示します。  
  
```  
Result  
-------------------------  
<Prod ProductModelID="19">  
  <ShortFeature FeatureDescLength="15">  
    <wm:Warranty   
       xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
      <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
      <wm:Description>parts and labor</wm:Description>  
    </wm:Warranty>  
   </ShortFeature>  
</Prod>  
...  
```  
  
## <a name="see-also"></a>参照  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
