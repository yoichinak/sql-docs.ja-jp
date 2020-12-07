---
description: Keys コレクション (ADOX)
title: Keys コレクション (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table::Keys
- Keys
helpviewer_keywords:
- Keys collection [ADOX]
ms.assetid: cdb31c76-e559-475c-b33a-aac24f73e70e
author: rothja
ms.author: jroth
ms.openlocfilehash: 675584dd52cd1a403b9d9d44351b86e88caba382
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983983"
---
# <a name="keys-collection-adox"></a>Keys コレクション (ADOX)
[テーブル](./table-object-adox.md)のすべての[キー](./key-object-adox.md)オブジェクトを格納します。  
  
## <a name="remarks"></a>解説  
 [キーコレクション]()の[Append](./append-method-adox-keys.md)メソッドは、ADOX で一意です。 次のようにすることができます。  
  
-   [追加](./append-method-adox-keys.md)メソッドを使用して、新しいキーをコレクションに追加します。  
  
 その他のプロパティとメソッドは、ADO コレクションの標準です。 次のようにすることができます。  
  
-   [項目](../ado-api/item-property-ado.md)プロパティを使用して、コレクション内のキーにアクセスします。  
  
-   [Count](../ado-api/count-property-ado.md)プロパティを使用して、コレクションに格納されているキーの数を返します。  
  
-   [Delete](./delete-method-adox-collections.md)メソッドを使用して、コレクションからキーを削除します。  
  
-   [更新](../ado-api/refresh-method-ado.md)メソッドを使用して、現在のデータベースのスキーマを反映するように、コレクション内のオブジェクトを更新します。  
  
 ここでは、次のトピックについて説明します。  
  
-   [Indexes コレクションのプロパティ、メソッド、およびイベント](./indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Keys Append メソッド、Key Type、UpdateRule プロパティの例 (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Keys コレクションのプロパティ、メソッド、およびイベント](./keys-collection-properties-methods-and-events.md)   
 [Key オブジェクト (ADOX)](./key-object-adox.md)