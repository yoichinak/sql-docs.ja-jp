---
title: not 関数 (XQuery) |Microsoft Docs
description: XQuery の not () 関数をブール値と共に使用する方法について説明します。
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
- effective Boolean value [XQuery]
- fn:not function
- not function [XQuery]
- EBV
ms.assetid: 93dfc377-45f1-4384-9392-560d9331a915
author: rothja
ms.author: jroth
ms.openlocfilehash: f857a8f107b26500bb324584d7d7853e09bbb735
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100353301"
---
# <a name="functions-on-boolean-values---not-function"></a>ブール値に対する関数 - 機能しない 
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  *$Arg* の有効なブール値が false の場合は true を返し、 *$arg* の有効なブール値が TRUE の場合は false を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:not($arg as item()*) as xs:boolean  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 有効なブール値が指定されているアイテムのシーケンス。  
  
## <a name="examples"></a>使用例  
 このトピックでは、AdventureWorks データベースのさまざまな **xml** 型の列に格納されている xml インスタンスに対して XQuery の例を示します。  
  
### <a name="a-using-the-not-xquery-function-to-find-product-models-whose-catalog-descriptions-do-not-include-the-specifications-element"></a>A. Not () XQuery 関数を使用して、カタログの説明に要素が含まれていない製品モデルを検索し \<Specifications> ます。  
 次のクエリでは、カタログの説明に <> 要素が含まれていない製品モデルの製品モデル Id を含む XML を構築し `Specifications` ます。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
       <Product   
           ProductModelID="{ sql:column("ProductModelID") }"  
        />  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[not(pd:Specifications/*)]  '  
     ) = 0  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   ドキュメントでは名前空間を使用するため、このサンプルでは WITH NAMESPACE ステートメントを使用します。 別の方法として、 [XQuery プロローグ](../xquery/modules-and-prologs-xquery-prolog.md)で **declare namespace** キーワードを使用してプレフィックスを定義することもできます。  
  
-   次に、クエリは、<`Product`> 要素とその **Productmodelid** 属性を含む XML を構築します。  
  
-   WHERE 句では、 [exist () メソッド (XML データ型)](../t-sql/xml/exist-method-xml-data-type.md) を使用して行をフィルター処理します。 **Exist ()** メソッドは、子要素を持たない要素がある場合に True を返し \<ProductDescription> \<Specification> ます。 **Not ()** 関数の使用に注意してください。  
  
 各製品モデルカタログの説明には要素が含まれているので、この結果セットは空です \<Specifications> 。  
  
### <a name="b-using-the-not-xquery-function-to-retrieve-work-center-locations-that-do-not-have-a-machinehours-attribute"></a>B. not() XQuery 関数を使用して、MachineHours 属性を持たないワーク センターの場所を取得する  
 次のクエリは、命令列に対して指定されています。 この列には、製品モデルの製造手順が格納されています。  
  
 特定の製品モデルでは、MachineHours を指定していないワークセンターの場所を取得します。 つまり、属性 **Machinehours** は要素に対して指定されていません \<Location> 。  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     for $i in /AWMI:root/AWMI:Location[not(@MachineHours)]  
     return  
       <Location LocationID="{ $i/@LocationID }"   
                   LaborHrs="{ $i/@LaborHours }" >  
        </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7   
```  
  
 上記のクエリでは、次の点に注意してください。  
  
-   [XQuery プロローグ](../xquery/modules-and-prologs-xquery-prolog.md)の **Declarenamespace** は、Adventure works の製造手順の名前空間プレフィックスを定義します。 この定義は、製造手順ドキュメントで使用されているのと同じ名前空間を表しています。  
  
-   クエリでは、 **Machinehours** 属性がない場合、 **not ( @MachineHours )** 述語は True を返します。  
  
 結果を次に示します。  
  
```  
ProductModelID Result   
-------------- --------------------------------------------  
7              <Location LocationID="30" LaborHrs="1"/>  
               <Location LocationID="50" LaborHrs="3"/>  
               <Location LocationID="60" LaborHrs="4"/>  
```  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 制限事項は次のとおりです。  
  
-   **Not ()** 関数は、xs: boolean 型、node () *、または空のシーケンスの引数のみをサポートします。  
  
## <a name="see-also"></a>参照  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
