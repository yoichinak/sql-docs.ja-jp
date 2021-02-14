---
title: concat 関数 (XQuery) |Microsoft Docs
description: 引数として指定された0個以上の文字列を連結することによって作成された文字列を返す XQuery 関数 concat () について説明します。
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:concat function
- concat function [XQuery]
ms.assetid: d50afd20-a297-445e-be9e-13b48017e7ca
author: rothja
ms.author: jroth
ms.openlocfilehash: 3ad92315e20ae314fb9a22ddea1241f379ecc90f
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100341923"
---
# <a name="functions-on-string-values---concat"></a>文字列値に使用する関数 - concat
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  0個以上の文字列を引数として受け取り、これらの各引数の値を連結することによって作成された文字列を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:concat ($string as xs:string?  
           ,$string as xs:string?  
           [, ...]) as xs:string  
```  
  
## <a name="arguments"></a>引数  
 *$string*  
 連結する文字列 (省略可能)。  
  
## <a name="remarks"></a>Remarks  
 この関数には少なくとも 2 つの引数が必要です。 空のシーケンスを引数として渡した場合、長さゼロの文字列として処理されます。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>補助文字 (サロゲート ペア)  
 XQuery 関数のサロゲートペアの動作は、データベースの互換性レベルと、場合によっては、関数の既定の名前空間 URI に依存します。 詳細については、「 [SQL Server 2016 のデータベースエンジン機能の重大な変更](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)」の「XQuery 関数はサロゲート対応」を参照してください。 「 [ALTER DATABASE Compatibility Level &#40;transact-sql&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) 」と「 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)」も参照してください。  
  
## <a name="examples"></a>使用例  
 このトピックでは、AdventureWorks サンプルデータベースのさまざまな **xml** 型の列に格納されている xml インスタンスに対して XQuery の例を示します。  
  
### <a name="a-using-the-concat-xquery-function-to-concatenate-strings"></a>A. concat() XQuery 関数を使用した文字列の連結  
 このクエリは、特定の製品モデルについて、保証期間と保証の説明を連結して作成された文字列を返します。 カタログの説明ドキュメントでは、<`Warranty`> 要素は <> で構成され、<`WarrantyPeriod` `Description` 子要素も> ます。  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
SELECT CatalogDescription.query('  
    <Product   
        ProductModelID= "{ (/pd:ProductDescription/@ProductModelID)[1] }"  
        ProductModelName = "{ sql:column("PD.Name") }" >  
        {   
          concat( string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:WarrantyPeriod)[1]), "-",  
                  string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:Description)[1]))   
         }   
     </Product>  
 ') as Result  
FROM Production.ProductModel PD  
WHERE  PD.ProductModelID=28  
  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   SELECT 句では、CatalogDescription は **xml** 型の列です。 したがって、 [query () メソッド (XML データ型)](../t-sql/xml/query-method-xml-data-type.md)、命令. query () が使用されます。 XQuery ステートメントは、クエリメソッドの引数として指定されます。  
  
-   クエリの実行対象となるドキュメントは、名前空間を使用します。 そのため、 **名前空間キーワードを** 使用して、名前空間のプレフィックスを定義します。 詳細については、「 [XQuery プロローグ](../xquery/modules-and-prologs-xquery-prolog.md)」を参照してください。  
  
 結果を次に示します。  
  
```  
<Product ProductModelID="28" ProductModelName="Road-450">1 year-parts and labor</Product>  
```  
  
 前のクエリでは、特定の製品の情報を取得します。 次のクエリは、XML のカタログの説明が保存されているすべての製品について同じ情報を取得します。 **Xml** データ型の **exist ()** メソッドは、行の xml ドキュメントに <> 要素がある場合に True を返し `ProductDescription` ます。  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
    <Product   
        ProductModelID= "{ (/pd:ProductDescription/@ProductModelID)[1] }"   
        ProductName = "{ sql:column("PD.Name") }" >  
        {   
          concat( string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:WarrantyPeriod)[1]), "-",  
                  string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:Description)[1]))   
         }   
     </Product>  
 ') as Result  
FROM Production.ProductModel PD  
WHERE CatalogDescription.exist('//pd:ProductDescription ') = 1  
  
```  
  
 **Xml** 型の **exist ()** メソッドによって返されるブール値は1と比較されることに注意してください。  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 制限事項は次のとおりです。  
  
-   SQL Server の **concat ()** 関数は、xs: string 型の値のみを受け取ります。 その他の値は、xs: string または xdt: untypedAtomic に明示的にキャストする必要があります。  
  
## <a name="see-also"></a>参照  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
