---
description: Indexes コレクション (ADOX)
title: Indexes コレクション (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Table::Indexes
- Indexes
helpviewer_keywords:
- Indexes collection [ADOX]
ms.assetid: 184cf536-455c-42be-bf1c-a5c25bade961
author: rothja
ms.author: jroth
ms.openlocfilehash: 8b8873cf8815fc6ffac1afbd9f6e003ee792d61f
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100054107"
---
# <a name="indexes-collection-adox"></a>Indexes コレクション (ADOX)
テーブルのすべての [Index](./index-object-adox.md) オブジェクトを格納します。  
  
## <a name="remarks"></a>解説  
 **Indexes** コレクションの [Append](./append-method-adox-indexes.md)メソッドは、ADOX で一意です。 次の操作を行うことができます。  
  
-   **追加** メソッドを使用して、新しいインデックスをコレクションに追加します。  
  
 その他のプロパティとメソッドは、ADO コレクションの標準です。 次の操作を行うことができます。  
  
-   [Item](../ado-api/item-property-ado.md)プロパティを使用して、コレクション内のインデックスにアクセスします。  
  
-   [Count](../ado-api/count-property-ado.md)プロパティを使用して、コレクションに格納されているインデックスの数を返します。  
  
-   [Delete](./delete-method-adox-collections.md)メソッドを使用して、コレクションからインデックスを削除します。  
  
-   [更新](../ado-api/refresh-method-ado.md)メソッドを使用して、現在のデータベーススキーマを反映するように、コレクション内のオブジェクトを更新します。  
  
 ここでは、次のトピックについて説明します。  
  
-   [Indexes コレクションのプロパティ、メソッド、およびイベント](./indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Indexes Append メソッドの例 (VB)](./indexes-append-method-example-vb.md)   
 [Index オブジェクト (ADOX)](./index-object-adox.md)