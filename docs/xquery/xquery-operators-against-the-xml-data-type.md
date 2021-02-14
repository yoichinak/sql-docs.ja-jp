---
title: Xml データ型に対する XQuery 演算子 |Microsoft Docs
description: Xml データ型に対して使用できる XQuery 演算子について説明します。
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, operators
- operators [XQuery]
- xml data type [SQL Server], XQuery
ms.assetid: 39ca3d2e-e928-4333-872b-75c4ccde8e79
author: rothja
ms.author: jroth
ms.openlocfilehash: c340049fd9655febfe3974a895b9f93e8cf1e2fb
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100352362"
---
# <a name="xquery-operators-against-the-xml-data-type"></a>xml データ型に対する XQuery の演算子
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  XQuery では、次の演算子がサポートされています。  
  
-   数値演算子 (+、-、*、div、mod)  
  
-   値の比較演算子 (eq、ne、lt、gt、le、ge)  
  
-   一般的な比較演算子 (=、! =、 \<, > 、 \<=, > =)  
  
 これらの演算子の詳細については、「 [&#40;XQuery の比較式](../xquery/comparison-expressions-xquery.md)」を参照してください&#41;  
  
## <a name="examples"></a>例  
  
### <a name="a-using-general-operators"></a>A. 一般的な演算子の使用  
 次のクエリでは、シーケンスおよびシーケンスの比較に適用される一般的な演算子の用途について説明します。 このクエリでは、 **Contact** テーブルの **additionalcontactinfo** 列から、各顧客の電話番号のシーケンスを取得します。 このシーケンスは、2つの電話番号 ("111-111-1111"、"222-2222") のシーケンスと比較されます。  
  
 このクエリでは、比較演算子を使用し **=** ます。 演算子の右側にあるシーケンスの各ノードは、 **=** 左側にあるシーケンスの各ノードと比較されます。 ノードが一致する場合、ノードの比較は **TRUE** になります。 その後、int に変換され、1と比較され、クエリから顧客 ID が返されます。  
  
```sql
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS ACI,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS ACT)  
SELECT ContactID   
FROM   Person.Contact  
WHERE  AdditionalContactInfo.value('  
      //ACI:AdditionalContactInfo//ACT:telephoneNumber/ACT:number =   
          ("111-111-1111", "222-2222")',  
      'bit')= cast(1 as bit)  
```  
  
 前のクエリがどのように機能するかを確認するもう1つの方法があります。 **Additionalcontactinfo** 列から取得した各電話番号の値は、2つの電話番号のセットと比較されます。 値がセット内にある場合、その顧客が結果に返されます。  
  
### <a name="b-using-a-numeric-operator"></a>B. 数値演算子の使用  
 このクエリの + 演算子は、1つの項目に適用されるため、値演算子です。 たとえば、クエリによって返されるサイズに値1が追加されます。  
  
```sql
SELECT ProductModelID, Instructions.query('  
     declare namespace   
 AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
     for $i in (/AWMI:root/AWMI:Location)[1]  
     return   
       <Location LocationID="{ ($i/@LocationID) }"  
                   LotSize  = "{  number($i/@LotSize) }"  
                   LotSize2 = "{ number($i/@LotSize) + 1 }"  
                   LotSize3 = "{ number($i/@LotSize) + 2 }" >  
  
       </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
### <a name="c-using-a-value-operator"></a>C. 値演算子の使用  
 次のクエリでは、 `Picture` 画像のサイズが "small" である製品モデルの <> 要素が取得されます。  
  
```sql
SELECT CatalogDescription.query('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     for $P in /PD:ProductDescription/PD:Picture[PD:Size eq "small"]  
     return  
           $P  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 **Eq** 演算子のオペランドは両方ともアトミック値であるため、値演算子がクエリで使用されます。 一般的な比較演算子 () を使用して、同じクエリを記述でき **=** ます。  
  
## <a name="see-also"></a>参照  
 [Xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)   
 [XML データ &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 言語リファレンス &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
