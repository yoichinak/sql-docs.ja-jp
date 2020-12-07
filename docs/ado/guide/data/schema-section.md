---
description: スキーマ セクション
title: スキーマセクション |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Schema section [ADO]
ms.assetid: 4ac6e524-2c92-48e8-b871-0a4b5c8fda18
author: rothja
ms.author: jroth
ms.openlocfilehash: a1f294e9c0258f1cc9d108d1eb9a47087b456ca8
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979723"
---
# <a name="schema-section"></a>スキーマ セクション
スキーマセクションが必要です。 前の例で示したように、ADO では、各列に関する詳細なメタデータを書き込み、データ値のセマンティクスを更新可能な限り保持します。 ただし、XML に読み込むために必要なのは、列の名前と、それらが属する行セットだけです。 最小スキーマの例を次に示します。  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"  
    xmlns:rs="urn:schemas-microsoft-com:rowset"  
    xmlns:z="#RowsetSchema">  
  <s:Schema id="RowsetSchema">  
    <s:ElementType name="row" content="eltOnly">  
      <s:AttributeType name="ShipperID"/>  
      <s:AttributeType name="CompanyName"/>  
      <s:AttributeType name="Phone"/>  
      <s:Extends type="rs:rowbase"/>  
    </s:ElementType>  
  </s:Schema>  
  <rs:data>  
...  
  </rs:data>  
</xml>  
```  
  
 前の例では、スキーマに型情報が含まれていないため、ADO はデータを可変長文字列として扱います。  
  
## <a name="creating-aliases-for-column-names"></a>列名の別名の作成  
 Rs: name 属性では、列名の別名を作成できます。これにより、行セットによって公開される列情報にわかりやすい名前が表示され、データセクションで短い名前が使用される可能性があります。 たとえば、次のように、ShipperID を s1、CompanyName から s2、Phone から s3 にマップするように、前のスキーマを変更できます。  
  
```  
<s:Schema id="RowsetSchema">   
<s:ElementType name="row" content="eltOnly" rs:updatable="true">   
<s:AttributeType name="s1" rs:name="ShipperID" rs:number="1" ...>   
...  
</s:AttributeType>   
<s:AttributeType name="s2" rs:name="CompanyName" rs:number="2" ...>   
...  
</s:AttributeType>   
<s:AttributeType name="s3" rs:name="Phone" rs:number="3" ...>   
...  
</s:AttributeType>   
...  
</s:ElementType>   
</s:Schema>  
```  
  
 次に、data セクションで、行は name 属性 (rs: name ではなく) を使用してその列を参照します。  
  
```  
"<row s1="1" s2="Speedy Express" s3="(503) 555-9831"/>  
```  
  
 列名が XML の有効な属性またはタグ名でない場合は、列名のエイリアスを作成する必要があります。 たとえば、"LastName" はエイリアスを持つ必要があります。これは、スペースが埋め込まれた名前が無効な属性であるためです。 次の行は XML パーサーによって正しく処理されません。そのため、スペースが埋め込まれていない他の名前のエイリアスを作成する必要があります。  
  
```  
<row last name="Jones"/>  
```  
  
 Name 属性に使用する値は、XML ドキュメントのスキーマとデータの両方のセクションで列が参照される場所で常に使用する必要があります。 次の例は、s1 の一貫した使用方法を示しています。  
  
```  
<s:Schema id="RowsetSchema">  
  <s:ElementType name="row" content="eltOnly">  
    <s:attribute type="s1"/>  
    <s:attribute type="CompanyName"/>  
    <s:attribute type="s3"/>  
    <s:extends type="rs:rowbase"/>  
  </s:ElementType>  
  <s:AttributeType name="s1" rs:name="ShipperID" rs:number="1"   
    rs:maydefer="true" rs:writeunknown="true">  
    <s:datatype dt:type="i4" dt:maxLength="4" rs:precision="10"   
      rs:fixedlength="true" rs:maybenull="true"/>  
  </s:AttributeType>  
</s:Schema>  
<rs:data>  
  <z:row s1="1" CompanyName="Speedy Express" s3="(503) 555-9831"/>  
</rs:data>  
```  
  
 同様に、前の例でに定義された別名がないため `CompanyName` 、は `CompanyName` ドキュメント全体で一貫して使用する必要があります。  
  
## <a name="data-types"></a>データ型  
 Dt: type 属性を使用して、列にデータ型を適用できます。 許可される XML 型についての明確なガイドについては、 [W3C XML データ仕様](http://www.w3.org/TR/1998/NOTE-XML-data/)の「データ型」を参照してください。 データ型を指定するには、次の2つの方法があります。列定義に対して dt: type 属性を直接指定するか、または、列定義の入れ子になった要素として、-datatype コンストラクトを使用します。 たとえば、次のように入力します。  
  
```  
<s:AttributeType name="Phone" >  
  <s:datatype dt:type="string"/>  
</s:AttributeType>  
```  
  
 上記の式は、次の式と同じです。  
  
```  
<s:AttributeType name="Phone" dt:type="string"/>  
```  
  
 行定義から dt: type 属性を完全に省略した場合、既定では列の型は可変長文字列になります。  
  
 型名以外の型情報がある場合 (たとえば、dt: maxLength)、には、-datatype 子要素を使用する方が読みやすくなります。 ただし、これは単なる規則であり、要件ではありません。  
  
 次の例は、スキーマに型情報を追加する方法を示しています。  
  
```  
<!-- 1. String with no max length -->  
<s:AttributeType name="title_id"/>  
<!-or -->  
<s:AttributeType name="title_id" dt:type="string"/>  
  
<!-- 2. Fixed length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" rs:fixedlength="true" />  
</s:AttributeType>  
  
<!-- 3. Variable length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" />  
</s:AttributeType>  
  
<!-- 4. Integer -->  
<s:AttributeType name="title_id" dt:type="int"/>  
```  
  
 2番目の例では、rs: fixedlength 属性が微妙に使用されています。 Rs: fixedlength 属性が true に設定されている列は、データの長さがスキーマで定義されている必要があることを意味します。 この場合、title_id の有効な値は "123456" です ("123")。 ただし、"123" は、長さが6ではなく3であるため、有効ではありません。 Fixedlength プロパティの詳細については、OLE DB プログラマーガイドを参照してください。  
  
## <a name="handling-nulls"></a>Null の処理  
 Null 値は rs: maybenull 属性によって処理されます。 この属性が true に設定されている場合、列の内容に null 値を含めることができます。 さらに、列がデータ行に見つからない場合、行セットからデータを読み取るユーザーは、IRowset:: GetData () から null 状態になります。 仕入先テーブルの次の列の定義について考えてみましょう。  
  
```  
<s:AttributeType name="ShipperID">  
  <s:datatype dt:type="int" dt:maxLength="4"/>  
</s:AttributeType>  
<s:AttributeType name="CompanyName">  
  <s:datatype dt:type="string" dt:maxLength="40" rs:maybenull="true"/>  
</s:AttributeType>  
```  
  
 この定義では、を null にすることはでき `CompanyName` ますが、 `ShipperID` null 値を含めることはできません。 Data セクションに次の行が含まれている場合、永続化プロバイダーは、列のデータの状態 `CompanyName` を OLE DB 状態の定数 DBSTATUS_S_ISNULL に設定します。  
  
```  
<z:row ShipperID="1"/>  
```  
  
 行が完全に空の場合、次のように永続化プロバイダーは DBSTATUS_E_UNAVAILABLE の OLE DB 状態を返し、 `ShipperID` CompanyName に DBSTATUS_S_ISNULL します。  
  
```  
<z:row/>   
```  
  
 長さ0の文字列は null と同じではないことに注意してください。  
  
```  
<z:row ShipperID="1" CompanyName=""/>  
```  
  
 前の行では、永続化プロバイダーは両方の列に対して DBSTATUS_S_OK の OLE DB 状態を返します。 `CompanyName`この場合のは単に "" (長さ0の文字列) です。  
  
 OLE DB の XML ドキュメントのスキーマ内で使用できる OLE DB コンストラクトの詳細については、「urn: schema-microsoft-com: rowset」と『 OLE DB プログラマーズガイド』の定義を参照してください。  
  
## <a name="see-also"></a>参照  
 [レコードを XML 形式で保持する](../../../ado/guide/data/persisting-records-in-xml-format.md)
