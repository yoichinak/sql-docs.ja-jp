---
title: min 関数 (XQuery) |Microsoft Docs
description: XQuery min () 関数について説明します。この関数は、シーケンス内の1つの項目を返します。これは、他のすべての項目の値よりも小さくなります。
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
- fn:min function
- min function [XQuery]
ms.assetid: db0b7d94-3fa6-488f-96d6-6a9a7d6eda23
author: rothja
ms.author: jroth
ms.openlocfilehash: 19c4204e84759bab022d0f0765b9d6154d23d003
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100341944"
---
# <a name="aggregate-functions---min"></a>集計関数 - min
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  アトミック値のシーケンス ( *$arg*) から、その値が他の項目よりも小さい値を持つ1つの項目を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:min($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 最小値を返す対象となる項目のシーケンス。  
  
## <a name="remarks"></a>Remarks  
 **Min ()** に渡されるアトミック値のすべての型は、同じ基本型のサブタイプである必要があります。 許容される基本型は、 **gt** 操作をサポートする型です。 これらの型には、3つの組み込み数値基本型、日付/時刻の基本型、xs: string、xs: boolean、および xdt: untypedAtomic が含まれます。 Xdt: untypedAtomic 型の値は、xs: double にキャストされます。 これらの型が混在している場合、または他の型の他の値が渡された場合は、静的エラーが発生します。  
  
 **Min ()** の結果は、Xdt: untypedAtomic の場合、xs: double など、渡された型の基本型を受け取ります。 入力が静的に空の場合、空のが暗黙的に指定され、静的なエラーが返されます。  
  
 **Min ()** 関数は、入力シーケンス内の他の値より小さいシーケンス内の1つの値を返します。 Xs: string 値の場合、既定の Unicode コードポイント照合順序が使用されます。 Xdt: untypedAtomic 値を xs: double にキャストできない場合、入力シーケンスの値は無視されます ( *$arg*)。 入力が動的に計算された空のシーケンスである場合は、空のシーケンスが返されます。  
  
## <a name="examples"></a>使用例  
 このトピックでは、AdventureWorks データベースのさまざまな **xml** 型の列に格納されている xml インスタンスに対して XQuery の例を示します。  
  
### <a name="a-using-the-min-xquery-function-to-find-the-work-center-location-that-has-the-fewest-labor-hours"></a>A. min() XQuery 関数を使用した、労働時間が最も短いワーク センター拠点の検索  
 次のクエリでは、労働時間が最も少ない製品モデル (ProductModelID = 7) の製造プロセスに含まれるすべてのワークセンターの場所を取得します。 通常、次に示すように 1 つの拠点が返されます。 複数の場所に最低労働時間が同じである場合は、すべてが返されます。  
  
```  
select ProductModelID, Name, Instructions.query('  
  declare namespace AWMI=  
    "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  for   $Location in /AWMI:root/AWMI:Location  
  where $Location/@LaborHours =  
          min( /AWMI:root/AWMI:Location/@LaborHours )  
return  
  <Location WCID=     "{ $Location/@LocationID }"   
              LaborHrs= "{ $Location/@LaborHours }" />  
  ') as Result   
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   XQuery プロローグの **namespace** キーワードは、名前空間プレフィックスを定義します。 このプレフィックスは、XQuery の本文で使用されます。  
  
 XQuery 本文は、 \<Location> WCID 属性と **LaborHrs** 属性を持つ要素を持つ XML を構築します。  
  
-   このクエリでは、ProductModelID と名前の値も取得します。  
  
 結果を次に示します。  
  
```  
ProductModelID   Name              Result  
---------------  ----------------  ---------------------------------  
7                HL Touring Frame  <Location WCID="45" LaborHrs="0.5"/>   
```  
  
## <a name="implementation-limitations"></a>実装の制限事項  
 制限事項は次のとおりです。  
  
-   **Min ()** 関数は、すべての整数を xs: decimal にマップします。  
  
-   Xs: duration 型の値に対する **min ()** 関数はサポートされていません。  
  
-   基本データ型の境界を超えて複数の型が混在するシーケンスはサポートされません。  
  
-   照合順序を提供する構文オプションはサポートされていません。  
  
## <a name="see-also"></a>参照  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
