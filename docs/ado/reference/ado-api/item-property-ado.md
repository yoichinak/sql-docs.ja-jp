---
description: Item プロパティ (ADO)
title: Item プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Parameters::GetItem
- Indexes::GetItem
- Parameters::Item
- Tables::Item
- Procedures::Item
- Users::GetItem
- Tables::GetItem
- Procedures::GetItem
- Users::get_Item
- Users::Item
- Views::GetItem
- Groups::Item
- Groups::get_Item
- Columns::Item
- Indexes::Item
- Fields15::GetItem
- Columns::GetItem
- Fields::Item
- Indexes::get_Item
- Columns::get_Item
- Fields15::Item
- Views::get_Item
- Groups::GetItem
- Errors::get_Item
- Fields15::get_Item
- Tables::get_Item
- Views::Item
- Errors::GetItem
- Parameters::get_Item
- Errors::Item
- Procedures::get_Item
helpviewer_keywords:
- Item property [ADO]
ms.assetid: e11484bb-c5c7-42d8-9bb8-21572125d727
author: rothja
ms.author: jroth
ms.openlocfilehash: 3f54ba0276affc1b098b3e499c31769f4cf9f927
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990753"
---
# <a name="item-property-ado"></a>Item プロパティ (ADO)
名前または序数を指定して、コレクションの特定のメンバーを示します。  
  
## <a name="syntax"></a>構文  
  
```  
Set object = collection.Item ( Index )  
```  
  
## <a name="return-value"></a>戻り値  
 オブジェクト参照を返します。  
  
## <a name="parameters"></a>パラメーター  
 *Index*  
 コレクション内のオブジェクトの名前または序数に評価される **バリアント** 式。  
  
## <a name="remarks"></a>解説  
 コレクション内の特定のオブジェクトを返すには、 **Item** プロパティを使用します。 **Item**が*Index*引数に対応するコレクション内のオブジェクトを見つけられない場合、エラーが発生します。 また、一部のコレクションでは名前付きオブジェクトがサポートされていません。これらのコレクションでは、序数参照を使用する必要があります。  
  
 **Item**プロパティは、すべてのコレクションの既定のプロパティです。したがって、次の構文形式は置き換えることができます。  
  
```  
collection.Item (Index)  
collection (Index)  
```  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Axes コレクション (ADO MD)](../ado-md-api/axes-collection-ado-md.md)  
        [Columns コレクション (ADOX)](../adox-api/columns-collection-adox.md)  
        [CubeDefs コレクション (ADO MD)](../ado-md-api/cubedefs-collection-ado-md.md)  
        [Dimensions コレクション (ADO MD)](../ado-md-api/dimensions-collection-ado-md.md)  
        [Errors コレクション (ADO)](./errors-collection-ado.md)  
        [Fields コレクション (ADO)](./fields-collection-ado.md)  
        [Groups コレクション (ADOX)](../adox-api/groups-collection-adox.md)  
    :::column-end:::
    :::column:::
        [Hierarchies コレクション (ADO MD)](../ado-md-api/hierarchies-collection-ado-md.md)  
        [Indexes コレクション (ADOX)](../adox-api/indexes-collection-adox.md)  
        [Keys コレクション (ADOX)](../adox-api/keys-collection-adox.md)  
        [Levels コレクション (ADO MD)](../ado-md-api/levels-collection-ado-md.md)  
        [Members コレクション (ADO MD)](../ado-md-api/members-collection-ado-md.md)  
        [Parameters コレクション (ADO)](./parameters-collection-ado.md)  
    :::column-end:::
    :::column:::
        [Positions コレクション (ADO MD)](../ado-md-api/positions-collection-ado-md.md)  
        [Procedures コレクション (ADOX)](../adox-api/procedures-collection-adox.md)  
        [Properties コレクション (ADO)](./properties-collection-ado.md)  
        [Tables コレクション (ADOX)](../adox-api/tables-collection-adox.md)  
        [Users コレクション (ADOX)](../adox-api/users-collection-adox.md)  
        [Views コレクション (ADOX)](../adox-api/views-collection-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>参照  
 [Item プロパティの例 (VB)](./item-property-example-vb.md)   
 [Item プロパティの例 (VC++)](./item-property-example-vc.md)