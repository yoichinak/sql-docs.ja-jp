---
description: Name プロパティ (ADOX)
title: Name プロパティ (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::PutName
- _Table::GetName
- _Key::Name
- _Key::get_Name
- _Column::GetName
- _Index::Name
- _Index::put_Name
- _Column::PutName
- _Key::put_Name
- _Table::put_Name
- _User25::PutName
- _Index::get_Name
- _Column::get_Name
- _Group25::Name
- _Group25::get_Name
- _Column::Name
- _User25::get_Name
- _Table::Name
- _Group25::GetName
- _Index::PutName
- _Column::put_Name
- _Key::GetName
- _Table::get_Name
- _User25::Name
- _User25::put_Name
- _Index::GetName
- _User25::GetName
helpviewer_keywords:
- Name property [ADOX]
ms.assetid: 81b92baf-b6b9-4f4e-9f33-4503795518cd
author: rothja
ms.author: jroth
ms.openlocfilehash: dd3a9fd328ce332c409d613ad468b96f0b94d31e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983913"
---
# <a name="name-property-adox"></a>Name プロパティ (ADOX)
オブジェクトの名前を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 **文字列**値を設定または返します。  
  
## <a name="remarks"></a>解説  
 名前はコレクション内で一意である必要はありません。  
  
 **Name**プロパティは、[列](./column-object-adox.md)、[グループ](./group-object-adox.md)、[キー](./key-object-adox.md)、[インデックス](./index-object-adox.md)、[テーブル](./table-object-adox.md)、および[ユーザー](./user-object-adox.md)オブジェクトに対して読み取り/書き込みが可能です。 **Name**プロパティは、[カタログ](./catalog-object-adox.md)、[プロシージャ](./procedure-object-adox.md)、および[ビュー](./view-object-adox.md)オブジェクトでは読み取り専用です。  
  
 読み取り/書き込みオブジェクト (**列**、 **グループ**、 **キー**、 **インデックス**、 **テーブル** 、 **ユーザー** オブジェクト) の場合、既定値は空の文字列 ("") になります。  
  
> [!NOTE]
>  キーの場合、このプロパティは既にコレクションに追加されている **キー** オブジェクトに対して読み取り専用になります。 テーブルの場合、このプロパティは、既にコレクションに追加されている **テーブル** オブジェクトに対しては読み取り専用です。  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Column オブジェクト (ADOX)](./column-object-adox.md)  
        [Group オブジェクト (ADOX)](./group-object-adox.md)  
        [Index オブジェクト (ADOX)](./index-object-adox.md)  
    :::column-end:::
    :::column:::
        [Key オブジェクト (ADOX)](./key-object-adox.md)  
        [Procedure オブジェクト (ADOX)](./procedure-object-adox.md)  
        [Property オブジェクト (ADO)](../ado-api/property-object-ado.md)  
    :::column-end:::
    :::column:::
        [Table オブジェクト (ADOX)](./table-object-adox.md)  
        [User オブジェクト (ADOX)](./user-object-adox.md)  
        [View オブジェクト (ADOX)](./view-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>参照  
 [Columns および Tables Append メソッド、Name プロパティの例 (VB)](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Keys Append メソッド、Key Type、UpdateRule プロパティの例 (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog プロパティの例 (VB)](./parentcatalog-property-example-vb.md)