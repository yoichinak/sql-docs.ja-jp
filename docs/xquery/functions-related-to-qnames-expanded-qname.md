---
title: ems-QName (XQuery) |Microsoft Docs
description: 展開された QName () 関数を使用して、QName の名前空間 URI とローカル名の部分を返す方法について説明します。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expanded-QName function
- fn:expanded-QName function
ms.assetid: b8377042-95cc-467b-9ada-fe43cebf4bc3
author: rothja
ms.author: jroth
ms.openlocfilehash: d1a59104b8becec2edd8b4b15c28e13e19011a4b
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036825"
---
# <a name="functions-related-to-qnames---expanded-qname"></a>QNames に関係する関数 - expanded-QName
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  *$ParamURI*で指定された名前空間 URI と *$paramLocal*で指定されたローカル名を使用して、xs: QName 型の値を返します。 *$ParamURI*が空の文字列または空のシーケンスの場合は、名前空間を表しません。  
  
## <a name="syntax"></a>構文  
  
```  
fn:expanded-QName($paramURI as xs:string?, $paramLocal as xs:string?) as xs:QName?  
```  
  
## <a name="arguments"></a>引数  
 *$paramURI*  
 QName の名前空間 URI です。  
  
 *$paramLocal*  
 QName のローカル名部分です。  
  
## <a name="remarks"></a>解説  
 次の例は、 **拡張 QName ()** 関数に適用されます。  
  
-   指定された *$paramLocal* 値が Xs: NCName 型の正しい構文形式でない場合、空のシーケンスが返され、動的なエラーを表します。  
  
-   では、xs: QName 型から他の型への変換はサポートされていません [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。 このため、 **拡張 QName ()** 関数は XML の構築では使用できません。 たとえば、`<e> expanded-QName(...) </e>` など、ノードを構築する場合、型指定なしの値を使用する必要があります。 これは、`expanded-QName()` で返される xs:QName の値を xdt:untypedAtomic に変換する必要性を意味します。 ただし、これはサポートされていません。 ソリューションは、このトピックで後述する例で提供されています。  
  
-   既存の QName 型の値を変更または比較することができます。 たとえば、は、 `/root[1]/e[1] eq expanded-QName("http://nsURI" "myNS")` 要素の値 <`e`> を、展開された **qname ()** 関数によって返された qname と比較します。  
  
## <a name="examples"></a>例  
 このトピックでは、データベースのさまざまな **xml** 型の列に格納されている xml インスタンスに対して XQuery の例を示し [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] ます。  
  
### <a name="a-replacing-a-qname-type-node-value"></a>A. QName 型ノードの値を置換する  
 この例では、QName 型の要素ノードの値を変更する方法を示しています。 この例では、次の処理を実行します。  
  
-   QName 型の要素を定義する XML スキーマコレクションを作成します。  
  
-   Xml スキーマコレクションを使用して、 **xml** 型の列を含むテーブルを作成します。  
  
-   XML インスタンスをテーブルに保存します。  
  
-   では、xml データ型の **modify ()** メソッドを使用して、インスタンスの QName 型の要素の値を変更します。 新しい QName 型の値を生成するには、展開された **qname ()** 関数を使用します。  
  
```  
-- If XML schema collection (if exists)  
-- drop xml schema collection SC  
-- go  
-- Create XML schema collection  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
    xmlns:xs="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="QNameXSD"   
      xmlns:xqo="QNameXSD" elementFormDefault="qualified">  
      <element name="Root" type="xqo:rootType" />  
      <complexType name="rootType">  
            <sequence minOccurs="1" maxOccurs="1">  
                        <element name="ElemQN" type="xs:QName" />  
            </sequence>  
      </complexType>  
</schema>'  
go  
-- Create table.  
CREATE TABLE T( XmlCol xml(SC) )  
-- Insert sample XML instnace  
INSERT INTO T VALUES ('  
<Root xmlns="QNameXSD" xmlns:ns="https://myURI">  
      <ElemQN>ns:someName</ElemQN>  
</Root>')  
go  
-- Verify the insertion  
SELECT * from T  
go  
-- Result  
<Root xmlns="QNameXSD" xmlns:ns="https://myURI">  
  <ElemQN>ns:someName</ElemQN>  
</Root>   
```  
  
 次のクエリでは、次に `ElemQN` 示すように、xml データ型の **modify ()** メソッドおよび xml DML の replace 値を使用して、<> 要素の値が置き換えられます。  
  
```  
-- the value.  
UPDATE T   
SET XmlCol.modify('  
  declare default element namespace "QNameXSD";   
  replace value of /Root[1]/ElemQN   
  with expanded-QName("https://myURI", "myLocalName") ')  
go  
-- Verify the result  
SELECT * from T  
go  
```  
  
 結果は次のとおりです。 `ElemQN`QName 型の> <要素に新しい値が追加されていることに注意してください。  
  
```  
<Root xmlns="QNameXSD" xmlns:ns="urn">  
  <ElemQN xmlns:p1="https://myURI">p1:myLocalName</ElemQN>  
</Root>  
```  
  
 次のステートメントは、この例で使用しているオブジェクトを削除します。  
  
```  
-- Cleanup  
DROP TABLE T  
go  
drop xml schema collection SC  
go  
```  
  
### <a name="b-dealing-with-the-limitations-when-using-the-expanded-qname-function"></a>B. 拡張 QName () 関数を使用する場合の制限事項に対処する  
 **拡張 QName**関数は、XML の構築では使用できません。 次の例を使って説明します。 この制限を回避するために、この例では最初にノードを挿入してから、そのノードを変更しています。  
  
```  
-- if exists drop the table T  
--drop table T  
-- go  
-- Create XML schema collection  
-- DROP XML SCHEMA COLLECTION SC  
-- go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" type="QName" nillable="true"/>  
</schema>'  
go  
 -- Create table T with a typed xml column (using the XML schema collection)  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- Insert an XML instance.  
insert into T values ('<root xmlns:a="https://someURI">a:b</root>')  
 go  
-- Verify  
SELECT *   
FROM T  
```  
  
 次の試行では、別の <`root`> 要素が追加されますが、これは失敗します。これは、拡張 QName () 関数が XML 構築でサポートされていないためです。  
  
```  
update T SET xmlCol.modify('  
insert <root>{expanded-QName("http://ns","someLocalName")}</root> as last into / ')  
go  
```  
  
 これを解決するには、まず <> 要素の値を持つインスタンスを挿入 `root` し、それを変更します。 この例では、<> 要素が挿入されるときに nil 初期値が使用され `root` ます。 この例の XML スキーマコレクションでは、<> 要素の nil 値が許可されて `root` います。  
  
```  
update T SET xmlCol.modify('  
insert <root xsi:nil="true"/> as last into / ')  
go  
-- now replace the nil value with another QName.  
update T SET xmlCol.modify('  
replace value of /root[last()] with expanded-QName("http://ns","someLocalName") ')  
go  
 -- verify   
SELECT * FROM T  
go  
-- result  
<root>b</root>  
```  
  
 `<root xmlns:a="https://someURI">a:b</root>`  
  
 `<root xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:p1="http://ns">p1:someLocalName</root>`  
  
 次のクエリに示すように、QName 値を比較できます。 このクエリは、値が `root` **ems ()** 関数によって返された qname 型の値と一致する <> 要素だけを返します。  
  
```  
SELECT xmlCol.query('  
    for $i in /root  
    return  
       if ($i eq expanded-QName("http://ns","someLocalName") ) then  
          $i  
       else  
          ()')  
FROM T  
```  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 1つの制限事項があります。 **拡張 QName ()** 関数では、2番目の引数として空のシーケンスが受け入れられ、2番目の引数が正しくない場合に、実行時エラーを発生させる代わりに、空のが返されます。  
  
## <a name="see-also"></a>参照  
 [QNames &#40;XQuery&#41;に関連する関数 ]()  
  
