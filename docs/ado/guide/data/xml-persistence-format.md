---
description: XML 保存形式
title: XML 永続化形式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML persistence [ADO], persistence format
ms.assetid: 6e146738-ac4d-47bb-b6cd-d87b2260aead
author: rothja
ms.author: jroth
ms.openlocfilehash: 2da0090b9e06a9df7692a27242a08303174f51aa
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978833"
---
# <a name="xml-persistence-format"></a>XML 保存形式
ADO は、永続化する XML ストリームに UTF-8 エンコードを使用します。  
  
 ADO XML 形式は、スキーマセクションと data セクションの2つのセクションに分かれています。 Northwind データベースの仕入先テーブルの XML ファイルの例を次に示します。 この例では、XML のさまざまな部分について説明します。  
  
## <a name="remarks"></a>解説  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"   
xmlns:dt="uuid:C2F41010-65B3-11d1-A29F-00AA00C14882"   
xmlns:rs="urn:schemas-microsoft-com:rowset"   
xmlns:z="#RowsetSchema">   
  <s:Schema id="RowsetSchema">   
    <s:ElementType name="row" content="eltOnly" rs:updatable="true">   
      <s:AttributeType name="ShipperID" rs:number="1"   
        rs:basetable="shippers" rs:basecolumn="ShipperID"  
        rs:keycolumn="true">   
        <s:datatype dt:type="int" dt:maxLength="4" rs:precision="10"   
          rs:fixedlength="true" rs:maybenull="false"/>   
      </s:AttributeType>   
      <s:AttributeType name="CompanyName" rs:number="2"   
        rs:nullable="true" rs:write="true" rs:basetable="shippers"   
        rs:basecolumn="CompanyName">   
        <s:datatype dt:type="string" dt:maxLength="40" />   
      </s:AttributeType>   
      <s:AttributeType name="Phone" rs:number="3" rs:nullable="true"   
        rs:write="true" rs:basetable="shippers"   
        rs:basecolumn="Phone">   
        <s:datatype dt:type="string" dt:maxLength="24"/>   
      </s:AttributeType>   
      <s:extends type="rs:rowbase"/>   
    </s:ElementType>   
  </s:Schema>   
  
  <rs:data>   
    <z:row ShipperID="1" CompanyName="Speedy Express"   
      Phone="(503) 555-9831"/>   
    <z:row ShipperID="2" CompanyName="United Package"   
      Phone="(503) 555-3199"/>   
    <z:row ShipperID="3" CompanyName="Federal Shipping"   
      Phone="(503) 555-9931"/>   
  </rs:data>   
</xml>  
```  
  
 スキーマには、名前空間、スキーマセクション、およびデータセクションの宣言が示されています。 Schema セクションには、row、ShipperID、CompanyName、および Phone の定義が含まれています。  
  
 スキーマ定義は [W3C XML データ仕様](http://www.w3.org/TR/1998/NOTE-XML-data/) に準拠しており、完全に検証できます (ただし、検証は Internet Explorer 5 では実行されません)。 現在、XML データは、レコードセットの永続化に対してサポートされている唯一のスキーマ形式です。  
  
 データセクションには、運送会社に関する情報を含む3つの行があります。 空の行セットの場合、data セクションは空になることがありますが、 \<rs:data> タグが存在している必要があります。 データがない場合は、単にタグの短縮形を記述でき \<rs:data/> ます。 "Rs" で始まるすべてのタグは、urn: schema-microsoft-com: rowset によって定義された名前空間にあることを示します。  
  
## <a name="see-also"></a>参照  
 [レコードを XML 形式で保持する](./persisting-records-in-xml-format.md)