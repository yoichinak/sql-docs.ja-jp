---
title: last 関数 (XQuery) |Microsoft Docs
description: シーケンス内の最後の項目の整数インデックスを返す XQuery last () 関数について説明します。
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
- last function [XQuery]
- fn:last function
ms.assetid: dc92086e-3b01-4b0b-9f54-3bbf306cf7ae
author: rothja
ms.author: jroth
ms.openlocfilehash: 3fdc8ce4bf35bb630d0ed0b40892312f89a5285c
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100340527"
---
# <a name="context-functions---last-xquery"></a>コンテキスト関数 - last (XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  現在処理中のシーケンス内のアイテム数を返します。 具体的には、シーケンス内の最後のアイテムの整数インデックスを返します。 シーケンスの最初の項目のインデックス値は1です。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:last() as xs:integer  
```  
  
## <a name="remarks"></a>Remarks  
 SQL Server では、 **fn: last ()** は、コンテキストに依存する述語のコンテキストでのみ使用できます。 具体的には、角かっこ () 内でのみ使用でき `[ ]` ます。  
  
## <a name="examples"></a>使用例  
 このトピックでは、AdventureWorks データベースのさまざまな **xml** 型の列に格納されている xml インスタンスに対して XQuery の例を示します。  
  
### <a name="a-using-the-last-xquery-function-to-retrieve-the-last-two-manufacturing-steps"></a>A. Last () XQuery 関数を使用した最後の2つの製造手順の取得  
 次のクエリでは、特定の製品モデルについて、最後の2つの製造手順を取得します。 最後の2つの製造手順を取得するために、このクエリでは、 **last ()** 関数によって返された製造手順の数である値が使用されます。  
  
```  
SELECT ProductModelID, Instructions.query('   
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  <LastTwoManuSteps>  
   <Last-1Step>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[(last()-1)]/text() }  
   </Last-1Step>  
   <LastStep>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[last()]/text() }  
   </LastStep>  
  </LastTwoManuSteps>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 上記のクエリでは、/の **last ()** 関数は `/AWMI:root//AWMI:Location)[1]/AWMI:step[last()]` 製造手順の数を返します。 この値は、ワークセンターの場所で最後の製造手順を取得するために使用されます。  
  
 結果を次に示します。  
  
```  
ProductModelID Result    
-------------- -------------------------------------  
7      <LastTwoManuSteps>  
         <Last-1Step>  
            When finished, inspect the forms for defects per   
            Inspection Specification .  
         </Last-1Step>  
         <LastStep>Remove the frames from the tool and place them   
            in the Completed or Rejected bin as appropriate.  
         </LastStep>  
       </LastTwoManuSteps>  
```  
  
## <a name="see-also"></a>参照  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
