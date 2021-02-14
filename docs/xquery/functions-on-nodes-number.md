---
title: number 関数 (XQuery) |Microsoft Docs
description: 指定された引数の数値を返す XQuery 関数の数値 () について説明します。
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
- number function
- fn:number function
ms.assetid: dff6d19b-765c-4df9-afff-9a0e7be9b91b
author: rothja
ms.author: jroth
ms.openlocfilehash: 6aa035be000fbbda12a7205c33925daf656c3da0
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100345025"
---
# <a name="functions-on-nodes---number"></a>ノードの関数 - number
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  *$Arg* によって示されるノードの数値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:number() as xs:double?   
fn:number($arg as node()?) as xs:double?  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 値が数値として返されるノード。  
  
## <a name="remarks"></a>Remarks  
 *$Arg* が指定されていない場合、double に変換されたコンテキストノードの数値が返されます。 SQL Server では、引数のない **fn: number ()** は、コンテキストに依存する述語のコンテキストでのみ使用できます。 具体的には、角かっこ ([]) 内でのみ使用できます。 たとえば、次の式は、<`ROOT`> 要素を返します。  
  
```  
declare @x xml  
set @x='<ROOT>111</ROOT>'  
select @x.query('/ROOT[number()=111]')  
```  
  
 ノードの値が、 **XML スキーマパート 2: データ型、W3C 勧告** で定義されているように、数値単純型の有効な字句表現でない場合、関数は空のシーケンスを返します。 NaN はサポートされません。  
  
## <a name="examples"></a>使用例  
 このトピックでは、AdventureWorks データベースのさまざまな **xml** 型の列に格納されている xml インスタンスに対して XQuery の例を示します。  
  
### <a name="a-using-the-number-xquery-function-to-retrieve-the-numeric-value-of-an-attribute"></a>A. Number () XQuery 関数を使用して属性の数値を取得する  
 次のクエリでは、製品モデル7の製造プロセスの最初のワークセンターの場所から、大量のサイズの属性の数値を取得します。  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     for $i in (//AWMI:root//AWMI:Location)[1]  
     return   
       <Location LocationID="{ ($i/@LocationID) }"   
                   LotSizeA="{  $i/@LotSize }"  
                   LotSizeB="{  number($i/@LotSize) }"  
                   LotSizeC="{ number($i/@LotSize) + 1 }" >  
  
       </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   **Number ()** 関数は、 **LotSizeA** 属性のクエリに示されているように、必須ではありません。 これは XPath 1.0 関数で、主に旧バージョンとの互換性上の理由で含まれています。  
  
-   **LotSizeB** の XQuery は number 関数を指定し、冗長です。  
  
-   **Lotsizec** のクエリは、算術演算で数値を使用する方法を示しています。  
  
 結果を次に示します。  
  
```  
ProductModelID   Result  
----------------------------------------------  
7              <Location LocationID="10"   
                         LotSizeA="100"   
                         LotSizeB="100"   
                         LotSizeC="101" />  
```  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 制限事項は次のとおりです。  
  
-   **Number ()** 関数は、ノードのみを受け入れます。 アトミック値を受け取ることはできません。  
  
-   値を数値として返すことができない場合、 **number ()** 関数は、NaN ではなく空のシーケンスを返します。  
  
## <a name="see-also"></a>参照  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
