---
description: データ セクション
title: Data Section |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data section [ADO]
ms.assetid: 43dc42a8-7057-48e6-93d6-880d5c5c51a4
author: rothja
ms.author: jroth
ms.openlocfilehash: ac4febc789aca18401380ee8ada7b2ab7f9d30a3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991453"
---
# <a name="data-section"></a>データ セクション
データセクションでは、保留中の更新、挿入、または削除と共に、行セットのデータを定義します。 Data セクションには、0個以上の行を含めることができます。 行がスキーマによって定義されている場合にのみ、1つの行セットからデータを格納できます。 また、前述のように、データのない列は省略できます。 Data セクションで属性またはサブ要素が使用されていて、そのコンストラクトが schema セクションで定義されていない場合、そのコンストラクトは警告なしで無視されます。  
  
## <a name="string"></a>文字列型  
 テキストデータ内の予約済み XML 文字は、適切な文字エンティティに置き換える必要があります。 たとえば、"Joe's ガレージ" という会社名では、単一引用符をエンティティに置き換える必要があります。 実際の行は次のようになります。  
  
```  
<z:row CompanyName="Joe's Garage"/>  
```  
  
 次の文字は XML で予約されており、文字エンティティ {'、"、&、} で置き換える必要があり \<,> ます。  
  
## <a name="binary"></a>Binary  
 バイナリデータは、16進数でエンコードされます (つまり、1バイトが2文字にマップされ、1つの文字がニブルごとに1文字)。  
  
## <a name="datetime"></a>DateTime  
 バリアント VT_DATE 形式は、XML データ型で直接サポートされていません。 データと時間の両方の要素を含む日付の正しい形式は、Yyyy-mm-ddthh: mm: ss です。  
  
 XML で指定された日付形式の詳細については、「 [W3C xml-Data specification](https://go.microsoft.com/fwlink/?LinkId=5692)」を参照してください。  
  
 XML データ仕様で2つの同等のデータ型が定義されている場合 (たとえば、i4 = = int)、ADO はフレンドリ名を書き込みますが、両方を読み取ります。  
  
## <a name="managing-pending-changes"></a>保留中の変更の管理  
 レコードセットは、即時更新モードまたはバッチ更新モードで開くことができます。 クライアント側カーソルを使用してバッチ更新モードで開かれた場合、レコードセットに加えられたすべての変更は、UpdateBatch メソッドが呼び出されるまで保留状態になります。 保留中の変更は、レコードセットが保存されるときにも保持されます。 XML では、urn: schema-microsoft-com: rowset で定義された "update" 要素を使用して表されます。 また、行セットを更新できる場合は、行の定義で更新可能なプロパティを true に設定する必要があります。 たとえば、仕入先テーブルに保留中の変更が含まれていることを定義する場合、行定義は次のようになります。  
  
```  
<s:ElementType name="row" content="eltOnly" updatable="true">  
  <s:attribute type="ShipperID"/>  
  <s:attribute type="CompanyName"/>  
  <s:attribute type="Phone"/>  
  <s:extends type="rs:rowbase"/>  
</s:ElementType>  
```  
  
 これにより、データを保存するように永続化プロバイダーに指示し、ADO が更新可能なレコードセットオブジェクトを構築できるようにします。  
  
 次のサンプルデータは、挿入、変更、および削除が永続化されたファイルでどのように表示されるかを示しています。  
  
```  
<rs:data>  
  <z:row ShipperID="2" CompanyName="United Package"   
    Phone="(503) 555-3199"/>  
<rs:update>  
  <rs:original>  
    <z:row ShipperID="3" CompanyName="Federal Shipping"   
      Phone="(503) 555-9931"/>  
  </rs:original>  
  <z:row Phone="(503) 552-7134"/>  
</rs:update>  
<rs:insert>  
  <z:row ShipperID="12" CompanyName="Lightning Shipping"   
    Phone="(505) 111-2222"/>  
  <z:row ShipperID="13" CompanyName="Thunder Overnight"   
    Phone="(505) 111-2222"/>  
  <z:row ShipperID="14" CompanyName="Blue Angel Air Delivery"   
    Phone="(505) 111-2222"/>  
</rs:insert>  
<rs:delete>  
  <z:row ShipperID="1" CompanyName="Speedy Express" Phone="(503) 555-9831"/>  
</rs:delete>  
</rs:data>  
```  
  
 更新には常に、元の行データの後に変更された行データが含まれます。 変更された行には、すべての列、または実際に変更された列のみを含めることができます。 前の例では、出荷業者2の行は変更されておらず、電話の列のみが出荷業者3の値を変更したため、変更された行に含まれるのは唯一の列です。 運送会社12、13、14の挿入された行は、1つの rs: insert タグの下にまとめてバッチ処理されます。 削除された行もバッチ処理できますが、これは前の例には示されていません。  
  
## <a name="see-also"></a>参照  
 [レコードを XML 形式で保持する](./persisting-records-in-xml-format.md)