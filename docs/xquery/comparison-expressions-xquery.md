---
title: 比較式 (XQuery) |Microsoft Docs
description: 一般、値、ノード、およびノード順の比較演算子を含む XQuery 比較式の使用方法について説明します。
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
- node comparison operators [XQuery]
- comparison expressions [XQuery]
- node order comparison operators [XQuery]
- expressions [XQuery], comparison
- comparison operators [XQuery]
- value comparison operators
ms.assetid: dc671348-306f-48ef-9e6e-81fc3c7260a6
author: rothja
ms.author: jroth
ms.openlocfilehash: 4824cd52001305a05c00e197e8c4140598267d4f
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100349340"
---
# <a name="comparison-expressions-xquery"></a>比較式 (XQuery)
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  XQuery には、次の種類の比較演算子が用意されています。  
  
-   一般的な比較演算子  
  
-   値の比較演算子  
  
-   ノードの比較演算子  
  
-   ノード順の比較演算子  
  
## <a name="general-comparison-operators"></a>一般的な比較演算子  
 一般的な比較演算子を使用して、アトミック値、シーケンス、またはその 2 つの組み合わせを比較できます。  
  
 一般的な演算子を次の表に定義します。  
  
|演算子|説明|  
|--------------|-----------------|  
|=|等しい|  
|!=|等しくない|  
|\<|より小さい|  
|>|より大きい|  
|\<=|以下|  
|>=|以上|  
  
 一般的な比較演算子を使用して2つのシーケンスを比較するときに、最初のシーケンスの値と True を比較する2番目のシーケンスに値が存在する場合、全体の結果は True になります。 それ以外の場合は False になります。 たとえば、(1, 2, 3) = (3, 4) は両方のシーケンスに値 3 があるので True になります。  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1,2,3) = (3,4)')    
```  
  
 比較する 2 つの値の型は、比較できる型である必要があります。 具体的には、値の型は静的に確認されます。 数値の比較の場合、数値型の上位変換が発生する場合があります。 たとえば、10の10進値が double 値の1e1 と比較される場合、10進値は double に変更されます。 double 値の比較は正確には行えないので、不正確な結果になる場合があります。  
  
 値の1つが型指定されていない場合は、他の値の型にキャストされます。 次の例では、値7が整数として扱われます。 比較する前に、型指定されていない値 (/a [1]) が整数に変換されます。 整数の比較によって True が返されます。  
  
```  
declare @x xml  
set @x='<a>6</a>'  
select @x.query('/a[1] < 7')  
```  
  
 逆に、型指定されていない値が文字列またはその他の型指定されていない値と比較される場合、xs: string にキャストされます。 次のクエリでは、文字列6が文字列 "17" と比較されます。 このクエリは文字列の比較になるので、False が返されます。  
  
```  
declare @x xml  
set @x='<a>6</a>'  
select @x.query('/a[1] < "17"')  
```  
  
 次のクエリは、AdventureWorks サンプルデータベースで提供されている製品カタログから製品モデルの小さいサイズの画像を返します。 このクエリは、によって返されたアトミック値のシーケンスを `PD:ProductDescription/PD:Picture/PD:Size` シングルトンシーケンス "small" と比較します。 比較が True の場合は、<Picture 要素が返され \> ます。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD)  
SELECT CatalogDescription.query('         
    for $P in /PD:ProductDescription/PD:Picture[PD:Size = "small"]         
    return $P') as Result         
FROM   Production.ProductModel         
WHERE  ProductModelID=19         
```  
  
 次のクエリでは、<数値要素内の電話番号のシーケンスを \> 文字列リテラル "112-111-1111" と比較しています。 このクエリでは、AdditionalContactInfo 列の電話番号要素のシーケンスを比較して、特定の顧客の特定の電話番号がドキュメントに存在するかどうかを判断します。  
  
```  
WITH XMLNAMESPACES (  
  'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
  'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS aci)  
  
SELECT AdditionalContactInfo.value('         
   /aci:AdditionalContactInfo//act:telephoneNumber/act:number = "112-111-1111"', 'nvarchar(10)') as Result         
FROM Person.Contact         
WHERE ContactID=1         
```  
  
 このクエリは True を返します。 これは、その数字がドキュメント内に存在することを示します。 次のクエリは、前のクエリの少し変更されたバージョンです。 このクエリでは、ドキュメントから取得した電話番号の値が、2つの電話番号の値のシーケンスと比較されます。 比較が True の場合、<number \> 要素が返されます。  
  
```  
WITH XMLNAMESPACES (  
  'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
  'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS aci)  
  
SELECT AdditionalContactInfo.query('         
  if (/aci:AdditionalContactInfo//act:telephoneNumber/act:number = ("222-222-2222","112-111-1111"))         
  then          
     /aci:AdditionalContactInfo//act:telephoneNumber/act:number         
  else         
    ()') as Result         
FROM Person.Contact         
WHERE ContactID=1  
  
```  
  
 結果を次に示します。  
  
```  
\<act:number   
  xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
    111-111-1111  
\</act:number>  
\<act:number   
  xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
    112-111-1111  
\</act:number>   
```  
  
## <a name="value-comparison-operators"></a>値の比較演算子  
 値の比較演算子は、アトミック値を比較するために使用されます。 クエリでは、値の比較演算子の代わりに、一般的な比較演算子を使用できます。  
  
 値の比較演算子は、次の表で定義されています。  
  
|演算子|[説明]|  
|--------------|-----------------|  
|eq|等しい|  
|ne|等しくない|  
|lt|より小さい|  
|gt|より大きい|  
|le|以下|  
|ge|以上|  
  
 2つの値が、選択した演算子に従って同じを比較する場合、式は True を返します。 それ以外の場合は False を返します。 いずれかの値が空のシーケンスの場合、式の結果は False になります。  
  
 これらの演算子は、単一のアトミック値でのみ機能します。 つまり、オペランドの 1 つにシーケンスを指定することはできません。  
  
 たとえば、次のクエリは、 \<Picture> 画像のサイズが "small" である製品モデルの要素を取得します。  
  
```  
SELECT CatalogDescription.query('         
              declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";         
              for $P in /PD:ProductDescription/PD:Picture[PD:Size eq "small"]         
              return         
                    $P         
             ') as Result         
FROM Production.ProductModel         
WHERE ProductModelID=19         
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   `declare namespace` 後でクエリで使用される名前空間プレフィックスを定義します。  
  
-   \<Size>要素の値は、指定された atomic 値 "small" と比較されます。  
  
-   値演算子はアトミック値でのみ機能するので、 **data ()** 関数はノード値を取得するために暗黙的に使用されることに注意してください。 つまり、`data($P/PD:Size) eq "small"` も同じ結果になります。  
  
 結果を次に示します。  
  
```  
\<PD:Picture   
  xmlns:PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
  \<PD:Angle>front\</PD:Angle>  
  \<PD:Size>small\</PD:Size>  
  \<PD:ProductPhotoID>31\</PD:ProductPhotoID>  
\</PD:Picture>  
```  
  
 値の比較でのデータ型の上位変換の規則は、一般的な比較でのデータ型の上位変換の規則と同じです。 また、は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 一般的な比較時に使用される値の比較時に、型指定されていない値に対して同じキャスト規則を使用します。 それに対して、XQuery 仕様の規則では、値の比較時に型指定されていない値は xs:string に常にキャストされます。  
  
## <a name="node-comparison-operator"></a>ノードの比較演算子  
 ノード比較演算子 **は** で、ノード型にのみ適用されます。 返される結果は、オペランドとして渡される2つのノードが、ソースドキュメント内の同じノードを表すかどうかを示します。 この演算子は、2つのオペランドが同じノードである場合に True を返します。 それ以外の場合は False を返します。  
  
 次のクエリでは、ワークセンターの場所10が、特定の製品モデルの製造プロセスの最初の場所であるかどうかを確認します。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions' AS AWMI)  
  
SELECT ProductModelID, Instructions.query('         
    if (  (//AWMI:root/AWMI:Location[@LocationID=10])[1]         
          is          
          (//AWMI:root/AWMI:Location[1])[1] )          
    then         
          <Result>equal</Result>         
    else         
          <Result>Not-equal</Result>         
         ') as Result         
FROM Production.ProductModel         
WHERE ProductModelID=7           
```  
  
 結果を次に示します。  
  
```  
ProductModelID       Result          
-------------- --------------------------  
7              <Result>equal</Result>      
```  
  
## <a name="node-order-comparison-operators"></a>ノード順の比較演算子  
 ノード順の比較演算子は、ドキュメント内の位置に基づいて、ノードのペアを比較します。  
  
 ドキュメントの順序に基づいて、次のような比較が行われます。  
  
-   `<<` : ドキュメント順で、オペランド **1** が **オペランド 2** の前に配置されます。  
  
-   `>>` : ドキュメント順で、 **オペランド 1** が **オペランド 2** に従います。  
  
 次のクエリでは、製品カタログの説明に、 \<Warranty> \<Maintenance> 特定の製品のドキュメント順序で要素の前に要素が表示されている場合に True が返されます。  
  
```  
WITH XMLNAMESPACES (  
  'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD,  
  'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS WM)  
  
SELECT CatalogDescription.value('  
     (/PD:ProductDescription/PD:Features/WM:Warranty)[1] <<   
           (/PD:ProductDescription/PD:Features/WM:Maintenance)[1]', 'nvarchar(10)') as Result  
FROM  Production.ProductModel  
where ProductModelID=19  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   Query では、 **xml** データ型の **value ()** メソッドが使用されます。  
  
-   クエリのブール型の結果が **nvarchar (10)** に変換され、が返されます。  
  
-   このクエリは True を返します。  
  
## <a name="see-also"></a>参照  
 [型システム &#40;XQuery&#41;](../xquery/type-system-xquery.md)   
 [XQuery 式](../xquery/xquery-expressions.md)  
  
  
