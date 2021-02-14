---
title: 条件式 (XQuery) |Microsoft Docs
description: XQuery でサポートされている条件式について説明します。
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, conditional expressions
- expressions [XQuery], conditional
- effective Boolean value [XQuery]
- if-then-else statement [XQuery]
- conditional expressions [XQuery]
- EBV
ms.assetid: b280dd96-c80f-4c51-bc06-a88d42174acb
author: rothja
ms.author: jroth
ms.openlocfilehash: 5fdc8703482f570d0ecb749b471af170b62770ba
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100349371"
---
# <a name="conditional-expressions-xquery"></a>条件式 (XQuery)
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  XQuery では、次の条件付きの **if-then-else** ステートメントがサポートされています。  
  
```  
if (<expression1>)  
then  
  <expression2>  
else  
  <expression3>  
```  
  
 の有効なブール値に応じて `expression1` 、またはのいずれか `expression2` `expression3` が評価されます。 次に例を示します。  
  
-   テスト式 `expression1` の結果が空のシーケンスになった場合、結果は False になります。  
  
-   テスト式の `expression1` 結果が単純なブール値になる場合は、この値が式の結果になります。  
  
-   テスト式 `expression1` の結果が複数ノードのシーケンスになった場合、式の結果は True になります。  
  
-   それ以外の場合は、静的なエラーが発生します。  
  
 また、以下の点にも注意してください。  
  
-   テスト式は、かっこで囲む必要があります。  
  
-   **Else** 式は必須です。 このトピックの例に示すように、不要な場合は、"()" を返すことができます。  
  
 たとえば、次のクエリは **xml** 型の変数に対して指定されています。 **If** 条件は、 @v [sql: variable () 関数](../xquery/xquery-extension-functions-sql-variable.md)拡張関数を使用して、XQuery 式内の sql 変数 () の値をテストします。 変数値が "FirstName" の場合は、<`FirstName`> 要素を返します。 それ以外の場合は、<`LastName`> 要素を返します。  
  
```  
declare @x xml  
declare @v varchar(20)  
set @v='FirstName'  
set @x='  
<ROOT rootID="2">  
  <FirstName>fname</FirstName>  
  <LastName>lname</LastName>  
</ROOT>'  
SELECT @x.query('  
if ( sql:variable("@v")="FirstName" ) then  
  /ROOT/FirstName  
 else  
   /ROOT/LastName  
')  
```  
  
 結果を次に示します。  
  
```  
<FirstName>fname</FirstName>  
```  
  
 次のクエリでは、特定の製品モデルの製品カタログの説明から最初の2つの機能の説明を取得します。 ドキュメントにさらに多くの機能がある場合は、 `there-is-more` 空のコンテンツを含む <> 要素が追加されます。  
  
```  
SELECT CatalogDescription.query('  
     declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /p1:ProductDescription/@ProductModelID }  
          { /p1:ProductDescription/@ProductModelName }   
          {  
            for $f in /p1:ProductDescription/p1:Features/*[position()\<=2]  
            return  
            $f   
          }  
          {  
            if (count(/p1:ProductDescription/p1:Features/*) > 2)  
            then \<there-is-more/>  
            else ()  
          }   
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 前のクエリで **は、if** 式の条件によって <> に3つ以上の子要素があるかどうかがチェックされ `Features` ます。 3 つ以上ある場合は、結果に `\<there-is-more/>` 要素が返されます。  
  
 結果を次に示します。  
  
```  
<Product ProductModelID="19" ProductModelName="Mountain 100">  
  \<p1:Warranty xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    \<p1:WarrantyPeriod>3 years\</p1:WarrantyPeriod>  
    \<p1:Description>parts and labor\</p1:Description>  
  \</p1:Warranty>  
  \<p2:Maintenance xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    \<p2:NoOfYears>10 years\</p2:NoOfYears>  
    \<p2:Description>maintenance contract available through your dealer or any AdventureWorks retail store.\</p2:Description>  
  \</p2:Maintenance>  
  \<there-is-more />  
</Product>  
```  
  
 次のクエリでは、 `Location` ワークセンターの場所でセットアップ時間が指定されていない場合に、LocationID 属性を持つ <> 要素が返されます。  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $WC in //AWMI:root/AWMI:Location  
        return  
        if ( $WC[not(@SetupHours)] )  
        then  
          <WorkCenterLocation>  
             { $WC/@LocationID }   
          </WorkCenterLocation>  
         else  
           ()  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 結果を次に示します。  
  
```  
<WorkCenterLocation LocationID="30" />  
<WorkCenterLocation LocationID="45" />  
<WorkCenterLocation LocationID="60" />  
```  
  
 このクエリは、次の例に示すように、 **if** 句を指定せずに記述できます。  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in //AWMI:root/AWMI:Location[not(@SetupHours)]   
        return  
          <Location>  
             { $WC/@LocationID }   
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
## <a name="see-also"></a>参照  
 [XQuery 式](../xquery/xquery-expressions.md)  
  
  
