---
title: substring 関数 (XQuery) |Microsoft Docs
description: ソース文字列の指定部分を返す XQuery 関数 substring () について説明します。
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
- substring function [XQuery]
- fn:substring function
ms.assetid: 2b3b8651-de51-46dc-af82-c86c45eac871
author: rothja
ms.author: jroth
ms.openlocfilehash: 7457341a5489485973869e46c2ba721b86352217
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100345017"
---
# <a name="functions-on-string-values---substring"></a>文字列値に使用する関数 - substring
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  *$StartingLoc* の値によって示される位置から開始し、 *$sourceString* の値の一部を返します。 *$length* の値によって示される文字数に対して続行されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc as xs:decimal?) as xs:string?  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc as xs:decimal?,  
                          $length as xs:decimal?) as xs:string?  
```  
  
## <a name="arguments"></a>引数  
 *$sourceString*  
 ソース文字列。  
  
 *$startingLoc*  
 部分文字列の開始位置となるソース文字列内の開始点。 この値が負の値や 0 の場合、0 より後の位置にある文字のみが返されます。 *$SourceString* の長さよりも大きい場合は、長さ0の文字列が返されます。  
  
 *$length*  
 optional取得する文字数。 指定しない場合は、 *$startingLoc* で指定された位置から文字列の末尾までのすべての文字が返されます。  
  
## <a name="remarks"></a>Remarks  
 この関数で引数を 3 つとも指定した場合、`$sourceString` 内で、次の範囲内の位置 `$p` から文字列が返されます。  
  
 `fn:round($startingLoc) <= $p < fn:round($startingLoc) + fn:round($length)`  
  
 *$Length* の値は、開始位置 *$sourceString* の値の文字数よりも大きくすることができます。 この場合、部分文字列は *$sourceString* の末尾までの文字を返します。  
  
 文字列の最初の文字は、位置1にあります。  
  
 *$SourceString* の値が空のシーケンスの場合、長さが0の文字列として処理されます。 それ以外の場合、 *$startingLoc* または *$length* のいずれかが空のシーケンスの場合は、空のシーケンスが返されます。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>補助文字 (サロゲート ペア)  
 XQuery 関数のサロゲートペアの動作は、データベースの互換性レベルと、場合によっては、関数の既定の名前空間 URI に依存します。 詳細については、「 [SQL Server 2016 のデータベースエンジン機能の重大な変更](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)」の「XQuery 関数はサロゲート対応」を参照してください。 「 [ALTER DATABASE Compatibility Level &#40;transact-sql&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) 」と「 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)」も参照してください。  
  
## <a name="implementation-limitations"></a>実装の制限事項  
 SQL Server には、xs: double ではなく、xs: decimal 型の *$startingLoc* および *$length パラメーター* が必要です。  
  
 SQL Server を使用すると、 *$startingLoc* と *$length* を空のシーケンスにすることができます。これは、空のシーケンスが () にマップされる動的エラーの結果として有効な値であるためです。  
  
## <a name="examples"></a>使用例  
 このトピックでは、データベース内のさまざまな **xml** 型の列に格納されている xml インスタンスに対して XQuery の例を示し [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] ます。  
  
### <a name="a-using-the-substring-xquery-function-to-retrieve-partial-summary-product-model-descriptions"></a>A. Substring () XQuery 関数を使用した部分的な概要の製品モデルの説明の取得  
 このクエリでは、製品モデルを説明するテキストの最初の50文字、ドキュメント内の <> 要素が取得され `Summary` ます。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Prod>{ substring(string((/pd:ProductDescription/pd:Summary)[1]), 1, 50) }</Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('/pd:ProductDescription')  = 1;  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   **String ()** 関数は、<> 要素の文字列値を返し `Summary` ます。 この関数は、<の `Summary`> 要素にテキストとサブ要素 (html 書式設定要素) の両方が含まれており、これらの要素をスキップしてすべてのテキストを取得するため、使用されます。  
  
-   **Substring ()** 関数は、**文字列 ()** によって取得された文字列値から最初の50文字を取得します。  
  
 結果の一部を次に示します。  
  
```  
ProductModelID Result  
-------------- ----------------------------------------------------  
19      <Prod>Our top-of-the-line competition mountain bike.</Prod>   
23      <Prod>Suitable for any type of riding, on or off-roa</Prod>  
...  
```  
  
## <a name="see-also"></a>参照  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
