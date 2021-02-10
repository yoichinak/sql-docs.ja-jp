---
description: Catalog オブジェクト (ADOX)
title: Catalog オブジェクト (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Catalog
helpviewer_keywords:
- Catalog object [ADOX]
ms.assetid: bb651639-a488-4e38-b6de-0ed99fa4dd92
author: rothja
ms.author: jroth
ms.openlocfilehash: 00e698ed85e739b2ea6a8dccebef7ce36e3be8e0
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100054477"
---
# <a name="catalog-object-adox"></a>Catalog オブジェクト (ADOX)
データソースのスキーマカタログを記述するコレクション ([テーブル](./tables-collection-adox.md)、 [ビュー](./views-collection-adox.md)、 [ユーザー](./users-collection-adox.md)、 [グループ](./groups-collection-adox.md)、および [プロシージャ](./procedures-collection-adox.md)) が格納されます。  
  
## <a name="remarks"></a>解説  
 **カタログ** オブジェクトを変更するには、オブジェクトを追加または削除するか、既存のオブジェクトを変更します。 一部のプロバイダーでは、すべての **カタログ** オブジェクトがサポートされていない場合や、スキーマ情報の表示のみがサポートされている場合があります。  
  
 **Catalog** オブジェクトのプロパティとメソッドを使用すると、次のことができます。  
  
-   [ActiveConnection](./activeconnection-property-adox.md)プロパティを ADO [connection](../ado-api/connection-object-ado.md)オブジェクトまたは有効な接続文字列に設定して、カタログを開きます。  
  
-   [Create](./create-method-adox.md)メソッドを使用して、新しいカタログを作成します。  
  
-   [GetObjectOwner](./getobjectowner-method-adox.md)メソッドと [SetObjectOwner](./setobjectowner-method.md)メソッドを使用して、**カタログ** 内のオブジェクトの所有者を特定します。  
  
 ここでは、次のトピックについて説明します。  
  
-   [Catalog オブジェクトのプロパティ、メソッド、およびイベント](./catalog-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Catalog ActiveConnection プロパティの例 (VB)](./catalog-activeconnection-property-example-vb.md)   
 [Command プロパティと CommandText プロパティの例 (VB)](./command-and-commandtext-properties-example-vb.md)   
 [Connection Close メソッド、Table Type プロパティの例 (VB)](./connection-close-method-table-type-property-example-vb.md)   
 [Create メソッドの例 (VB)](./create-method-example-vb.md)   
 [Keys Append メソッド、Key Type、UpdateRule プロパティの例 (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Parameters コレクション、Command プロパティの例 (VB)](./parameters-collection-command-property-example-vb.md)   
 [ParentCatalog プロパティの例 (VB)](./parentcatalog-property-example-vb.md)   
 [Procedures Append メソッドの例 (VB)](./procedures-append-method-example-vb.md)   
 [Procedures Delete メソッドの例 (VB)](./procedures-delete-method-example-vb.md)   
 [Procedures Refresh メソッドの例 (VB)](./procedures-refresh-method-example-vb.md)   
 [Views および Fields コレクションの例 (VB)](./views-and-fields-collections-example-vb.md)   
 [Views Append メソッドの例 (VB)](./views-append-method-example-vb.md)   
 [Views Collection、CommandText プロパティの例 (VB)](./views-collection-commandtext-property-example-vb.md)   
 [Views Delete メソッドの例 (VB)](./views-delete-method-example-vb.md)   
 [Views Refresh メソッドの例 (VB)](./views-refresh-method-example-vb.md)   
 [Groups コレクション (ADOX)](./groups-collection-adox.md)   
 [Procedures コレクション (ADOX)](./procedures-collection-adox.md)   
 [Tables コレクション (ADOX)](./tables-collection-adox.md)   
 [Users コレクション (ADOX)](./users-collection-adox.md)   
 [Views コレクション (ADOX)](./views-collection-adox.md)