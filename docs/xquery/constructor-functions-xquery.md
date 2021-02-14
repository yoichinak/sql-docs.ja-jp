---
title: コンストラクター関数 (XQuery) |Microsoft Docs
description: XSD の組み込みまたはユーザー定義のアトミック型のインスタンスを作成できるようにする XQuery のコンストラクター関数について説明します。
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
- constructor functions [XQuery]
ms.assetid: 98562d0e-d0e0-4f62-b001-90acbac67277
author: rothja
ms.author: jroth
ms.openlocfilehash: 0cc1fe3f4f36191a04973c759474f55a8356abda
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100349335"
---
# <a name="constructor-functions-xquery"></a>コンストラクター関数 (XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  コンストラクター関数は、指定された入力から、XSD の組み込みのアトミック型またはユーザー定義のアトミック型のインスタンスを生成します。  
  
## <a name="syntax"></a>構文  
  
```  
  
TYP($atomicvalue as xdt:anyAtomicType?  
  
) as TYP?  
  
```  
  
## <a name="arguments"></a>引数  
 *$strval*  
 変換される文字列。  
  
 *TYP*  
 任意の組み込み XSD 型。  
  
## <a name="remarks"></a>Remarks  
 コンストラクターは基本データ型、および派生されたアトミック XSD 型に対してサポートされています。 ただし、 **xs: duration** のサブタイプ ( **Xdt: yearMonthDuration、Xdt: daytimeduration**、 **xs: QName**、 **XS: NMTOKEN**、および **xs: NOTATION** を含む) はサポートされていません。 関連するスキーマコレクションで使用可能なユーザー定義のアトミック型は、次の型から直接または間接的に派生している場合にも使用できます。  
  
#### <a name="supported-base-types"></a>サポートされている基本型  
 サポートされている基本型は次のとおりです。  
  
-   xs:string  
  
-   xs:boolean  
  
-   xs:decimal  
  
-   xs:float  
  
-   xs:double  
  
-   xs:duration  
  
-   xs:dateTime  
  
-   xs:time  
  
-   xs:date  
  
-   xs:gYearMonth  
  
-   xs:gYear  
  
-   xs: G当月日  
  
-   xs:gDay  
  
-   xs: gMonth  
  
-   xs: hexBinary  
  
-   xs:base64Binary  
  
-   xs:anyURI  
  
#### <a name="supported-derived-types"></a>サポートされている派生型  
 サポートされている派生型は次のとおりです。  
  
-   xs:normalizedString  
  
-   xs:token  
  
-   xs:language  
  
-   xs: Name  
  
-   xs:NCName  
  
-   xs:ID  
  
-   xs:IDREF  
  
-   xs:ENTITY  
  
-   xs:integer  
  
-   xs:nonPositiveInteger  
  
-   xs:negativeInteger  
  
-   xs:long  
  
-   xs:int  
  
-   xs:short  
  
-   xs: byte  
  
-   xs:nonNegativeInteger  
  
-   xs:unsignedLong  
  
-   xs:unsignedInt  
  
-   xs:unsignedShort  
  
-   xs:unsignedByte  
  
-   xs:positiveInteger  
  
 SQL Server は、次のように、構築関数の呼び出しのための定数の折りたたみもサポートしています。  
  
-   引数が文字列リテラルの場合、式はコンパイル時に評価されます。 値が型に関する制約を満たしていない場合、静的エラーが発生します。  
  
-   引数が別の型のリテラルである場合、式はコンパイル時に評価されます。 値が型制約を満たしていない場合は、空のシーケンスが返されます。  
  
## <a name="examples"></a>使用例  
 このトピックでは、AdventureWorks データベースのさまざまな **xml** 型の列に格納されている xml インスタンスに対して XQuery の例を示します。  
  
### <a name="a-using-the-datetime-xquery-function-to-retrieve-older-product-descriptions"></a>A. dateTime() XQuery 関数を使用して、製品の説明の古いバージョンを取得する  
 この例では、最初にサンプル XML ドキュメントが **xml** 型の変数に割り当てられます。 このドキュメントには、3つのサンプル <> 要素が含まれており `ProductDescription` 、それぞれに <> 子要素が含まれてい `DateCreated` ます。  
  
 次に、その変数がクエリされ、指定された日時より前に作成された製品の説明だけを取得します。 比較のために、クエリでは、 **xs: dateTime ()** コンストラクター関数を使用して日付を入力します。  
  
```  
declare @x xml  
set @x = '<root>  
<ProductDescription ProductID="1" >  
  <DateCreated DateValue="2000-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
<ProductDescription  ProductID="2" >  
  <DateCreated DateValue="2001-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
<ProductDescription ProductID="3" >  
  <DateCreated DateValue="2002-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
</root>'  
  
select @x.query('  
     for $PD in  /root/ProductDescription  
     where xs:dateTime(data( ($PD/DateCreated/@DateValue)[1] )) < xs:dateTime("2001-01-01T00:00:00Z")  
     return  
        element Product  
       {   
        ( attribute ProductID { data($PD/@ProductID ) },  
        attribute DateCreated { data( ($PD/DateCreated/@DateValue)[1] ) } )  
        }  
 ')  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   ...Where loop 構造体は、 \<ProductDescription> where 句で指定された条件を満たす要素を取得するために使用されます。  
  
-   **Datetime ()** コンストラクター関数は、 **datetime** 型の値を作成して適切に比較できるようにするために使用されます。  
  
-   その後、クエリによって結果の XML が構築されます。 一連の属性を構成しているため、XML の構造にコンマとかっこが使用されています。  
  
 結果を次に示します。  
  
```  
<Product   
   ProductID="1"   
   DateCreated="2000-01-01T00:00:00Z"/>  
```  
  
## <a name="see-also"></a>参照  
 [XML 構築 &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)   
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
