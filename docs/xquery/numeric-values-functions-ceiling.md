---
title: シーリング関数 (XQuery) |Microsoft Docs
description: XQuery の天井 () 関数を使用して、関数の引数の値より小さくない小数部を含まない最小値を返す方法について説明します。
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:ceiling function
- ceiling function [XQuery]
ms.assetid: 594f1dd0-3c27-41b3-b809-9ce6714c5a97
author: rothja
ms.author: jroth
ms.openlocfilehash: 1ea2dbaab164c57acf9e9bc166ee431e80783648
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100341578"
---
# <a name="numeric-values-functions---ceiling"></a>数値関数 - ceiling 
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  小数部を含まない最小の数値を返します。引数の値よりも小さくありません。 引数が空のシーケンスの場合は、空のシーケンスを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:ceiling ( $arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 関数が適用される番号。  
  
## <a name="remarks"></a>Remarks  
 *$Arg* の型が、 **xs: float**、 **xs: double**、または **xs: decimal** の3つの数値基本データ型のいずれかである場合、戻り値の型は *$arg* の型と同じになります。  
  
 *$Arg* の型が数値型の1つから派生した型である場合、戻り値の型は基本数値型です。  
  
 Fn: floor、fn: シーリング、または fn: round 関数への入力が **xdt: untypedAtomic** の場合、これは暗黙的に **xs: double** にキャストされます。  
  
 その他の型のデータが入力されると、静的エラーが生成されます。  
  
## <a name="examples"></a>使用例  
 このトピックでは、AdventureWorks データベースのさまざまな **xml** 型の列に格納されている xml インスタンスに対して XQuery の例を示します。  
  
### <a name="a-using-the-ceiling-xquery-function"></a>A. ceiling() XQuery 関数の使用  
 製品モデル7の場合、このクエリは、製品モデルの製造プロセスにおけるワークセンターの場所の一覧を返します。 ドキュメントに記載されている場合、ワークセンターの場所ごとに、場所 ID、労働時間、および膨大なサイズが返されます。 このクエリでは、 **天井** 関数を使用して、 **decimal** 型の値として労働時間を返します。  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
     for $i in /AWMI:root/AWMI:Location  
     return   
       <Location LocationID="{ $i/@LocationID }"   
                   LaborHrs="{ ceiling($i/@LaborHours) }" >  
                    {   
                      $i/@LotSize  
                    }    
       </Location>  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   AWMI 名前空間プレフィックスは、Adventure Works の製造手順を表しています。 このプレフィックスは、クエリ対象のドキュメントで使用されているものと同じ名前空間を参照します。  
  
-   **命令** は **xml** 型の列です。 したがって、 [query () メソッド (XML データ型)](../t-sql/xml/query-method-xml-data-type.md) を使用して XQuery を指定します。 XQuery ステートメントは、クエリメソッドの引数として指定されます。  
  
-   **...return** はループ構造です。 クエリでは、 **for** ループは要素のリストを識別し \<Location> ます。 各ワークセンターの場所では、 **for** ループの **return** ステートメントによって、生成される XML が記述されます。  
  
    -   \<Location>LocationID 属性と LaborHrs 属性を持つ要素。 中かっこ ({}) 内の対応する式は、ドキュメントから必要な値を取得します。  
  
    -   {$ i/@LotSize } 式は、ドキュメントから LotSize 属性を取得します (存在する場合)。  
  
    -   結果を次に示します。  
  
```  
ProductModelID Result    
-------------- ------------------------------------------------------  
7      <Location LocationID="10" LaborHrs="3" LotSize="100"/>  
       <Location LocationID="20" LaborHrs="2" LotSize="1"/>     
       <Location LocationID="30" LaborHrs="1" LotSize="1"/>     
       <Location LocationID="45" LaborHrs="1" LotSize="20"/>  
       <Location LocationID="60" LaborHrs="3" LotSize="1"/>     
       <Location LocationID="60" LaborHrs="4" LotSize="1"/>  
```  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 制限事項は次のとおりです。  
  
-   **切り上げ ()** 関数は、すべての整数値を xs: decimal にマップします。  
  
## <a name="see-also"></a>参照  
 [floor 関数 &#40;XQuery&#41;](../xquery/numeric-values-functions-floor.md)   
 [round 関数 &#40;XQuery&#41;](../xquery/numeric-values-functions-round.md)  
  
  
