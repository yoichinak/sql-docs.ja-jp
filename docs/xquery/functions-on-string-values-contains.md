---
title: contains 関数 (XQuery) |Microsoft Docs
description: XQuery の contains 関数を使用して、指定した文字列値に指定した部分文字列値が含まれているかどうかを確認する方法について説明します。
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
- contains function (XQuery)
- fn:contains function
ms.assetid: 2c88c015-04fc-429b-84b2-835596a28b65
author: rothja
ms.author: jroth
ms.openlocfilehash: 18f57d57e1a944a1be66a880231533e6cf34493e
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100344973"
---
# <a name="functions-on-string-values---contains"></a>文字列値に使用する関数 - contains
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  *$Arg 1* の値に *$arg 2* によって指定された文字列値が含まれているかどうかを示す xs: boolean 型の値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:contains ($arg1 as xs:string?, $arg2 as xs:string?) as xs:boolean?  
```  
  
## <a name="arguments"></a>引数  
 *$arg 1*  
 テストする文字列値。  
  
 *$arg 2*  
 検索するサブストリング。  
  
## <a name="remarks"></a>Remarks  
 *$Arg 2* の値が長さ0の文字列の場合、この関数は **True** を返します。 *$Arg 1* の値が長さ0の文字列で、 *$arg 2* の値が長さ0の文字列ではない場合、関数は **False** を返します。  
  
 *$Arg 1* または *$arg 2* の値が空のシーケンスの場合、引数は長さ0の文字列として扱われます。  
  
 contains() 関数では、文字列の比較に XQuery の既定の Unicode コード ポイントの照合順序が使用されます。  
  
 *$Arg 2* に指定された部分文字列の値は、4000文字以下である必要があります。 指定された値が4000文字を超える場合、動的エラー条件が発生し、contains () 関数は、ブール値の **True** または **False** ではなく、空のシーケンスを返します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では XQuery 式に対して動的なエラーは発生しません。  
  
 大文字と小文字を区別しない比較を行う [には、大文字または](../xquery/functions-on-string-values-upper-case.md) 小文字の関数を使用できます。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>補助文字 (サロゲート ペア)  
 XQuery 関数のサロゲートペアの動作は、データベースの互換性レベルと、場合によっては、関数の既定の名前空間 URI に依存します。 詳細については、「 [SQL Server 2016 のデータベースエンジン機能の重大な変更](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)」の「XQuery 関数はサロゲート対応」を参照してください。 「 [ALTER DATABASE Compatibility Level &#40;transact-sql&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) 」と「 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)」も参照してください。  
  
## <a name="examples"></a>使用例  
 このトピックでは、AdventureWorks データベースのさまざまな xml 型の列に格納されている XML インスタンスに対して XQuery の例を示します。  
  
### <a name="a-using-the-contains-xquery-function-to-search-for-a-specific-character-string"></a>A. contains() XQuery 関数を使用した特定の文字列の検索  
 次のクエリでは、概要説明に Aerodynamic という単語が含まれている製品を検索します。 このクエリでは、ProductID と、その `Summary` ような製品の <> 要素が返されます。  
  
```  
--The product model description document uses  
--namespaces. The WHERE clause uses the exit()  
--method of the xml data type. Inside the exit method,  
--the XQuery contains()function is used to  
--determine whether the <Summary> text contains the word  
--Aerodynamic.   
  
USE AdventureWorks  
GO  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
      <Prod>  
         { /pd:ProductDescription/@ProductModelID }  
         { /pd:ProductDescription/pd:Summary }  
      </Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
   /pd:ProductDescription/pd:Summary//text()  
    [contains(., "Aerodynamic")]') = 1  
```  
  
 結果  
  
 `ProductModelID Result`  
  
 `-------------- ---------`  
  
 `28     <Prod ProductModelID="28">`  
  
 `<pd:Summary xmlns:pd=`  
  
 `"https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">`  
  
 `<p1:p xmlns:p1="http://www.w3.org/1999/xhtml">`  
  
 `A TRUE multi-sport bike that offers streamlined riding and`  
  
 `a revolutionary design. Aerodynamic design lets you ride with`  
  
 `the pros, and the gearing will conquer hilly roads.</p1:p>`  
  
 `</pd:Summary>`  
  
 `</Prod>`  
  
## <a name="see-also"></a>参照  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
