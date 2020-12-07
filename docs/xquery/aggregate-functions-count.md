---
description: 集計関数 - count
title: count 関数 (XQuery) |Microsoft Docs
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
- fn:count function
- count function [XQuery]
ms.assetid: a9f7131f-23e1-4d4d-a36c-180447543926
author: rothja
ms.author: jroth
ms.openlocfilehash: 6691ca005de2ceec1de0408e358544292c58704d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88467185"
---
# <a name="aggregate-functions---count"></a>集計関数 - count
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  *$Arg*によって指定されたシーケンスに含まれる項目の数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:count($arg as item()*) as xs:integer  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 カウントするアイテム。  
  
## <a name="remarks"></a>解説  
 *$Arg*が空のシーケンスの場合は0を返します。  
  
## <a name="examples"></a>例  
 このトピックでは、AdventureWorks データベースのさまざまな **xml** 型の列に格納されている xml インスタンスに対して XQuery の例を示します。  
  
### <a name="a-using-the-count-xquery-function-to-count-the-number-of-work-center-locations-in-the-manufacturing-of-a-product-model"></a>A. Count () XQuery 関数を使用して、製品モデルの製造におけるワークセンターの場所の数をカウントする  
 次のクエリは、製品モデルの製造プロセスにおけるワークセンターの場所の数をカウントします (ProductModelID = 7)。  
  
```  
SELECT Production.ProductModel.ProductModelID,   
       Production.ProductModel.Name,   
       Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
       <NoOfWorkStations>  
          { count(/AWMI:root/AWMI:Location) }  
       </NoOfWorkStations>  
') as WorkCtrCount  
FROM Production.ProductModel  
WHERE Production.ProductModel.ProductModelID=7  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   [XQuery プロローグ](../xquery/modules-and-prologs-xquery-prolog.md)の**namespace**キーワードは、名前空間プレフィックスを定義します。 次に、このプレフィックスが XQuery 本体で使用されます。  
  
-   このクエリでは、<> 要素を含む XML が構築され `NoOfWorkStations` ます。  
  
-   XQuery 本文の **count ()** 関数は、<> 要素の数をカウント `Location` します。  
  
 結果を次に示します。  
  
```  
ProductModelID   Name                 WorkCtrCount       
-------------- ---------------------------------------------------  
7             HL Touring Frame  <NoOfWorkStations>6</NoOfWorkStations>     
```  
  
 次のクエリで示すように、製品モデルの ID および名前を含むように XML を構成することもできます。  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
       <NoOfWorkStations  
             ProductModelID= "{ sql:column("Production.ProductModel.ProductModelID") }"   
             ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >  
          { count(/AWMI:root/AWMI:Location) }  
       </NoOfWorkStations>  
') as WorkCtrCount  
FROM Production.ProductModel  
WHERE Production.ProductModel.ProductModelID= 7  
```  
  
 結果を次に示します。  
  
```  
<NoOfWorkStations ProductModelID="7"   
                  ProductModelName="HL Touring Frame">6</NoOfWorkStations>  
```  
  
 XML 以外にも、次のクエリで示すように xml 以外の型で値を返すことができます。 このクエリでは、 [value () メソッド (xml データ型)](../t-sql/xml/value-method-xml-data-type.md) を使用して、ワークセンターの場所の数を取得します。  
  
```  
SELECT  ProductModelID,   
        Name,   
        Instructions.value('declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
           count(/AWMI:root/AWMI:Location)', 'int' ) as WorkCtrCount  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 結果を次に示します。  
  
```  
ProductModelID    Name            WorkCtrCount  
-------------- ---------------------------------  
7              HL Touring Frame        6     
```  
  
## <a name="see-also"></a>参照  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
