---
title: position 関数 (XQuery) |Microsoft Docs
description: 項目のシーケンス内のコンテキスト項目の位置を示す整数値を返す XQuery 関数の位置 () について説明します。
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
- position function
- fn:position function
ms.assetid: f1bab9e4-1715-4c06-9cb0-06c7e0c9c97f
author: rothja
ms.author: jroth
ms.openlocfilehash: dd2be5cf246bd625e63c31975effa59fb1b919d0
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100345029"
---
# <a name="context-functions---position-xquery"></a>コンテキスト関数 - position (XQuery)
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  現在処理されているアイテムのシーケンス内のコンテキスト アイテムの位置を示す整数値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:position() as xs:integer  
```  
  
## <a name="remarks"></a>Remarks  
 では [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 、 **fn: position ()** は、コンテキストに依存する述語のコンテキストでのみ使用できます。 具体的には、角かっこ ([]) 内でのみ使用できます。この関数と比較しても、静的な型の推論時にカーディナリティが減少することはありません。  
  
## <a name="examples"></a>使用例  
 このトピックでは、データベースのさまざまな **xml** 型の列に格納されている xml インスタンスに対して XQuery の例を示し [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] ます。  
  
### <a name="a-using-the-position-xquery-function-to-retrieve-the-first-two-product-features"></a>A. Position () XQuery 関数を使用した最初の2つの製品機能の取得  
 次のクエリでは、製品モデルカタログの説明から、最初の2つの機能、<> 要素の最初の2つの子要素を取得し `Features` ます。 その他の機能がある場合は、<`there-is-more/`> 要素を結果に追加します。  
  
```  
SELECT CatalogDescription.query('  
     declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /pd:ProductDescription/@ProductModelID }  
          { /pd:ProductDescription/@ProductModelName }   
          {  
            for $f in /pd:ProductDescription/pd:Features/*[position()<=2]  
            return  
            $f   
          }  
          {  
            if (count(/pd:ProductDescription/pd:Features/*) > 2)  
            then <there-is-more/>  
            else ()  
          }   
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE CatalogDescription is not null  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   [XQuery プロローグ](../xquery/modules-and-prologs-xquery-prolog.md)内の **namespace** キーワードは、クエリ本文で使用される名前空間プレフィックスを定義します。  
  
-   クエリ本文は、 \<Product> **Productmodelid** 属性と **ProductModelName** 属性を持つ要素を持ち、子要素として返される製品機能を持つ XML を構築します。  
  
-   **Position ()** 関数は、コンテキスト内での子要素の位置を決定するために、述語で使用され \<Features> ます。 最初または2番目の機能の場合は、それが返されます。  
  
-   IF ステートメントは、 \<there-is-more/> 製品カタログに3つ以上の機能がある場合に、結果に要素を追加します。  
  
-   カタログの記述がテーブルに保持されていない製品モデルもあるので、WHERE 句を使用して CatalogDescriptions が NULL の行を破棄しています。  
  
 結果の一部を次に示します。  
  
```  
<Product ProductModelID="19" ProductModelName="Mountain 100">  
  <p1:Warranty xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
  </p1:Warranty>  
  <p2:Maintenance xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p2:NoOfYears>10</p2:NoOfYears>  
    <p2:Description>maintenance contact available through your dealer or  
                    any AdventureWorks retail store.</p2:Description>  
  </p2:Maintenance>  
  <there-is-more/>  
</Product>   
...  
```  
  
## <a name="see-also"></a>参照  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
