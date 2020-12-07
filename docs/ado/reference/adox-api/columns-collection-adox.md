---
description: Columns コレクション (ADOX)
title: Columns コレクション (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Index::Columns
- Table::Columns
- Key::Columns
- Columns
helpviewer_keywords:
- Columns collection [ADOX]
ms.assetid: 23b9fea8-4f76-4a51-95ce-1a6ce4560b34
author: rothja
ms.author: jroth
ms.openlocfilehash: f1295aea12a1b9d60427864993630320d0f973ce
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985023"
---
# <a name="columns-collection-adox"></a>Columns コレクション (ADOX)
テーブル、インデックス、またはキーのすべての [Column](./column-object-adox.md) オブジェクトを格納します。  
  
## <a name="remarks"></a>解説  
 **Columns**コレクションの[Append](./append-method-adox-columns.md)メソッドは、ADOX で一意です。 次のようにすることができます。  
  
-   **追加**メソッドを使用して、新しい列をコレクションに追加します。  
  
 その他のプロパティとメソッドは、ADO コレクションの標準です。 次のようにすることができます。  
  
-   [Item](../ado-api/item-property-ado.md)プロパティを使用して、コレクション内の列にアクセスします。  
  
-   [Count](../ado-api/count-property-ado.md)プロパティを使用して、コレクションに含まれる列の数を返します。  
  
-   [Delete](./delete-method-adox-collections.md)メソッドを使用して、コレクションから列を削除します。  
  
-   [更新](../ado-api/refresh-method-ado.md)メソッドを使用して、現在のデータベースのスキーマを反映するように、コレクション内のオブジェクトを更新します。  
  
> [!NOTE]
>  [テーブル](./tables-collection-adox.md)コレクションに既に追加されている[テーブル](./table-object-adox.md)**に列が**存在しない場合、[インデックス](./index-object-adox.md)の**Columns**コレクションに**列**を追加すると、エラーが発生します。  
  
 ここでは、次のトピックについて説明します。  
  
-   [Columns コレクションのプロパティ、メソッド、およびイベント](./columns-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Columns および Tables Append メソッド、Name プロパティの例 (VB)](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close メソッド、Table Type プロパティの例 (VB)](./connection-close-method-table-type-property-example-vb.md)   
 [Keys Append メソッド、Key Type、UpdateRule プロパティの例 (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog プロパティの例 (VB)](./parentcatalog-property-example-vb.md)   
 [順序のプロパティの例 (VB)](./sortorder-property-example-vb.md)   
 [Column オブジェクト (ADOX)](./column-object-adox.md)