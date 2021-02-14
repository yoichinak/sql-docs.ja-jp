---
title: シーケンス式 (XQuery) |Microsoft Docs
description: 項目のシーケンスを作成、フィルター処理、および結合する XQuery シーケンス式について説明します。
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
- sequence [XQuery]
- expressions [XQuery], sequence
- filtering sequences [XQuery]
ms.assetid: 41e18b20-526b-45d2-9bd9-e3b7d7fbce4e
author: rothja
ms.author: jroth
ms.openlocfilehash: ea654a45894791fa22ecfa843c44cdd6214a5181
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100351061"
---
# <a name="sequence-expressions-xquery"></a>シーケンス式 (XQuery)
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、アイテムのシーケンスの構築、フィルター処理、および組み合わせに使用される、XQuery 演算子がサポートされます。 アイテムには、アトミック値またはノードを指定できます。  
  
## <a name="constructing-sequences"></a>シーケンスの構築  
 コンマ演算子を使用すると、項目を1つのシーケンスに連結するシーケンスを作成できます。  
  
 シーケンスには重複する値を含めることができます。 シーケンス内のシーケンスである入れ子になったシーケンスは、折りたたまれます。 たとえば、シーケンス (1, 2, (3, 4, (5))) は (1, 2, 3, 4, 5) になります。 次に、シーケンス構築の例を示します。  
  
### <a name="example-a"></a>例 A  
 次のクエリでは、5つのアトミック値のシーケンスが返されます。  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1,2,3,4,5)')  
go  
-- result 1 2 3 4 5  
```  
  
 次のクエリでは、2つのノードのシーケンスが返されます。  
  
```  
-- sequence of 2 nodes  
declare @x xml  
set @x=''  
select @x.query('(<a/>, <b/>)')  
go  
-- result  
<a />  
<b />  
```  
  
 次のクエリではアトミック値とノードのシーケンスが構築されているので、エラーが返されます。 これは異種シーケンスであり、サポートされていません。  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1, 2, <a/>, <b/>)')  
go  
```  
  
### <a name="example-b"></a>例 B  
 次のクエリでは、異なる長さの 4 つのシーケンスを 1 つのシーケンスに組み合わせることにより、アトミック値のシーケンスが構築されます。  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1,2),10,(),(4, 5, 6)')  
go  
-- result = 1 2 10 4 5 6  
```  
  
 FLOWR および ORDER BY を使用して、シーケンスを並べ替えることができます。  
  
```  
declare @x xml  
set @x=''  
select @x.query('for $i in ((1,2),10,(),(4, 5, 6))  
                  order by $i  
                  return $i')  
go  
```  
  
 **Fn: count ()** 関数を使用すると、シーケンス内の項目をカウントできます。  
  
```  
declare @x xml  
set @x=''  
select @x.query('count( (1,2,3,(),4) )')  
go  
-- result = 4  
```  
  
### <a name="example-c"></a>例 C  
 次のクエリは、Contact テーブルの **xml** 型の AdditionalContactInfo 列に対して指定されています。 この列には、1 つ以上の追加の電話番号、ポケットベル番号、住所などの追加の連絡先情報が格納されます。 \<telephoneNumber>、 \<pager> 、およびその他のノードは、ドキュメント内のどこにでも表示できます。 このクエリは、コンテキストノードのすべての子を含むシーケンスを作成し、その \<telephoneNumber> 後に子を作成し \<pager> ます。 Return 式では、コンマシーケンス演算子が使用されていることに注意して `($a//act:telephoneNumber, $a//act:pager)` ください。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
 'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS aci)  
  
SELECT AdditionalContactInfo.query('  
   for $a in /aci:AdditionalContactInfo   
   return ($a//act:telephoneNumber, $a//act:pager)  
') As Result  
FROM Person.Contact  
WHERE ContactID=3  
```  
  
 結果を次に示します。  
  
```  
<act:telephoneNumber xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3333</act:number>  
</act:telephoneNumber>  
<act:telephoneNumber xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3334</act:number>  
</act:telephoneNumber>  
<act:pager xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>999-555-1244</act:number>  
  <act:SpecialInstructions>  
Page only in case of emergencies.  
</act:SpecialInstructions>  
</act:pager>  
```  
  
## <a name="filtering-sequences"></a>シーケンスのフィルター処理  
 式に述語を追加することで、式によって返されるシーケンスをフィルター処理できます。 詳細については、「 [パス式 &#40;XQuery&#41;](../xquery/path-expressions-xquery.md)」を参照してください。 たとえば、次のクエリでは、3つの <> 要素ノードのシーケンスが返され `a` ます。  
  
```  
declare @x xml  
set @x = '<root>  
<a attrA="1">111</a>  
<a></a>  
<a></a>  
</root>'  
SELECT @x.query('/root/a')  
```  
  
 結果を次に示します。  
  
```  
<a attrA="1">111</a>  
<a />  
<a />  
```  
  
 `a`属性 attrA を持つ <> 要素だけを取得するには、述語でフィルターを指定します。 結果のシーケンスには、<> 要素が1つだけ含まれ `a` ます。  
  
```  
declare @x xml  
set @x = '<root>  
<a attrA="1">111</a>  
<a></a>  
<a></a>  
</root>'  
SELECT @x.query('/root/a[@attrA]')  
```  
  
 結果を次に示します。  
  
```  
<a attrA="1">111</a>  
```  
  
 パス式で述語を指定する方法の詳細については、「 [パス式のステップでの述語の指定](../xquery/path-expressions-specifying-predicates.md)」を参照してください。  
  
 次の例では、サブツリーのシーケンス式を作成し、そのシーケンスにフィルターを適用します。  
  
```  
declare @x xml  
set @x = '  
<a>  
  <c>C under a</c>  
</a>  
<b>    
   <c>C under b</c>  
</b>  
<c>top level c</c>  
<d></d>  
'  
```  
  
 の式は、サブ `(/a, /b)` ツリーと、 `/a` `/b` 結果のシーケンスから expression filters 要素を含むシーケンスを構築し `<c>` ます。  
  
```  
SELECT @x.query('  
  (/a, /b)/c  
')  
```  
  
 結果を次に示します。  
  
```  
<c>C under a</c>  
<c>C under b</c>  
```  
  
 次の例では、述語フィルターを適用します。 式は、要素 <> を `a` 含む> <> <要素を検索し `b` `c` ます。  
  
```  
declare @x xml  
set @x = '  
<a>  
  <c>C under a</c>  
</a>  
<b>    
   <c>C under b</c>  
</b>  
  
<c>top level c</c>  
<d></d>  
'  
SELECT @x.query('  
  (/a, /b)[c]  
')  
```  
  
 結果を次に示します。  
  
```  
<a>  
  <c>C under a</c>  
</a>  
<b>  
  <c>C under b</c>  
</b>  
```  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 制限事項は次のとおりです。  
  
-   XQuery 範囲式はサポートされません。  
  
-   シーケンスは同種でなければなりません。 具体的には、シーケンス内のすべてのアイテムは、ノードまたはアトミック値のいずれかにする必要があります。 これは静的にチェックされます。  
  
-   Union、intersect、または except 演算子を使用したノードシーケンスの結合はサポートされていません。  
  
## <a name="see-also"></a>参照  
 [XQuery 式](../xquery/xquery-expressions.md)  
  
  
