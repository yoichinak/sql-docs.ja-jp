---
description: XML での階層レコードセット
title: XML 内の階層的なレコードセット |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO], in XML
ms.assetid: 5d4b11c4-c94f-4910-b99b-5b9abc50d791
author: rothja
ms.author: jroth
ms.openlocfilehash: a9563782851575970d9f2ab9a5fcabce5efa32d1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980533"
---
# <a name="hierarchical-recordsets-in-xml"></a>XML での階層レコードセット
ADO を使用すると、階層的なレコードセットオブジェクトを XML に永続化できます。 階層的なレコードセットオブジェクトを使用すると、親レコードセット内のフィールドの値は別のレコードセットになります。 このようなフィールドは、属性ではなく XML ストリームの子要素として表されます。  
  
## <a name="remarks"></a>解説  
 この場合の例を次に示します。  
  
```  
Rs.Open "SHAPE {select stor_id, stor_name, state from stores} APPEND ({select stor_id, ord_num, ord_date, qty from sales} AS rsSales RELATE stor_id TO stor_id)", "Provider=MSDataShape;DSN=pubs;Integrated Security=SSPI;"  
```  
  
 次に、永続化されたレコードセットの XML 形式を示します。  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"     xmlns:dt="uuid:C2F41010-65B3-11d1-A29F-00AA00C14882"     xmlns:rs="urn:schemas-microsoft-com:rowset"   
    xmlns:z="#RowsetSchema">   
  <s:Schema id="RowsetSchema">   
    <s:ElementType name="row" content="eltOnly" rs:updatable="true">   
      <s:AttributeType name="stor_id" rs:number="1"   
        rs:writeunknown="true">   
        <s:datatype dt:type="string" dt:maxLength="4"   
          rs:fixedlength="true" rs:maybenull="false"/>   
      </s:AttributeType>   
      <s:AttributeType name="stor_name" rs:number="2" rs:nullable="true"   
        rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="40"/>   
      </s:AttributeType>   
      <s:AttributeType name="state" rs:number="3" rs:nullable="true"   
        rs:writeunknown="true">   
        <s:datatype dt:type="string" dt:maxLength="2"   
          rs:fixedlength="true"/>   
      </s:AttributeType>   
      <s:ElementType name="rsSales" content="eltOnly"   
        rs:updatable="true" rs:relation="010000000100000000000000">   
        <s:AttributeType name="stor_id" rs:number="1"   
          rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="4"   
            rs:fixedlength="true" rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="ord_num" rs:number="2"   
          rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="20"   
            rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="ord_date" rs:number="3"   
          rs:writeunknown="true">   
            <s:datatype dt:type="dateTime" dt:maxLength="16"   
              rs:scale="3" rs:precision="23" rs:fixedlength="true"   
              rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="qty" rs:number="4" rs:writeunknown="true">   
          <s:datatype dt:type="i2" dt:maxLength="2" rs:precision="5"   
            rs:fixedlength="true" rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:extends type="rs:rowbase"/>   
      </s:ElementType>   
      <s:extends type="rs:rowbase"/>   
    </s:ElementType>   
  </s:Schema>   
  <rs:data>   
    <z:row stor_id="6380" stor_name="Eric the Read Books" state="WA">   
      <rsSales stor_id="6380" ord_num="6871"   
        ord_date="1994-09-14T00:00:00" qty="5"/>   
      <rsSales stor_id="6380" ord_num="722a"   
        ord_date="1994-09-13T00:00:00" qty="3"/>   
    </z:row>   
    <z:row stor_id="7066" stor_name="Barnum's" state="CA">   
      <rsSales stor_id="7066" ord_num="A2976"   
        ord_date="1993-05-24T00:00:00" qty="50"/>   
      <rsSales stor_id="7066" ord_num="QA7442.3"   
        ord_date="1994-09-13T00:00:00" qty="75"/>   
    </z:row>   
    <z:row stor_id="7067" stor_name="News & Brews" state="CA">   
      <rsSales stor_id="7067" ord_num="D4482"   
        ord_date="1994-09-14T00:00:00" qty="10"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="40"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="20"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="20"/>   
    </z:row>   
  </rs:data>   
</xml>   
```  
  
 親レコードセット内の列の正確な順序は、このように永続化されている場合、明確ではありません。 親のフィールドには、子レコードセットを含めることができます。 永続化プロバイダーは、すべてのスカラー列を最初に属性として保持した後、すべての子レコードセット "columns" を親行の子要素として保持します。 親レコードセットのフィールドの位置を表す序数を取得するには、レコードセットのスキーマ定義を参照します。 すべてのフィールドには、フィールドの序数を含むレコードセットスキーマ名前空間で rs: number という OLE DB プロパティが定義されています。  
  
 子レコードセット内のすべてのフィールドの名前は、この子を含む親レコードセット内のフィールドの名前と連結されます。 これは、親と子のレコードセットの両方に2つの異なるテーブルから取得されたフィールドが含まれている場合に、名前の競合が発生しないようにするためですが、個別という名前が付けられています。  
  
 階層的なレコードセットを XML に保存する場合は、ADO の次の制限事項に注意する必要があります。  
  
-   保留中の更新を含む階層的なレコードセットを XML に保存することはできません。  
  
-   パラメーター化された shape コマンドを使用して作成された階層レコードセットは、(XML 形式または ADTG 形式で) 永続化できません。  
  
-   現在、ADO では、親と子のレコードセット間のリレーションシップがバイナリラージオブジェクト (BLOB) として保存されています。 このリレーションシップを記述する XML タグは、行セットスキーマの名前空間でまだ定義されていません。  
  
-   階層レコードセットが保存されると、すべての子レコードセットが一緒に保存されます。 現在のレコードセットが別のレコードセットの子である場合、その親は保存されません。 現在のレコードセットのサブツリーを形成するすべての子レコードセットが保存されます。  
  
 階層レコードセットを XML 永続化形式から再び開く場合は、次の制限事項に注意する必要があります。  
  
-   子レコードに、対応する親レコードが存在しないレコードが含まれている場合、これらの行は階層レコードセットの XML 表現では書き込まれません。 したがって、レコードセットが永続化された場所から再び開かれると、これらの行は失われます。  
  
-   子レコードが複数の親レコードを参照している場合は、レコードセットを再び開くと、子レコードセットに重複するレコードが含まれることがあります。 ただし、これらの重複は、ユーザーが基になる子行セットを直接操作している場合にのみ表示されます。 子レコードセット内を移動するためにチャプターが使用されている場合 (ADO 間を移動する唯一の方法)、重複は表示されません。  
  
## <a name="see-also"></a>参照  
 [レコードを XML 形式で保持する](./persisting-records-in-xml-format.md)