---
description: Index オブジェクト (ADOX)
title: Index オブジェクト (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Index
helpviewer_keywords:
- Index object [ADOX]
ms.assetid: 6b9578c0-bc94-46b9-b801-c18e14b04b31
author: rothja
ms.author: jroth
ms.openlocfilehash: 58b9e80dc57ddfdbd95bcb9523e428031fcebff0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984293"
---
# <a name="index-object-adox"></a>Index オブジェクト (ADOX)
データベーステーブルのインデックスを表します。  
  
## <a name="remarks"></a>解説  
 次のコードでは、新しい **インデックス**を作成します。  
  
```  
Dim obj As New Index  
```  
  
 **インデックス**オブジェクトのプロパティとコレクションを使用すると、次のことができます。  
  
-   [Name](./name-property-adox.md)プロパティを使用してインデックスを識別します。  
  
-   [Columns](./columns-collection-adox.md)コレクションを使用して、インデックスのデータベース列にアクセスします。  
  
-   インデックスキーが [一意](./unique-property-adox.md) のプロパティで一意である必要があるかどうかを指定します。  
  
-   インデックスが [PrimaryKey](./primarykey-property-adox.md) プロパティを持つテーブルの主キーであるかどうかを指定します。  
  
-   インデックスフィールドに null 値を持つレコードのインデックスエントリが [IndexNulls](./indexnulls-property-adox.md) プロパティに設定されているかどうかを指定します。  
  
-   [クラスター](./clustered-property-adox.md)化されたプロパティを使用してインデックスをクラスター化するかどうかを指定します。  
  
-   [プロパティ](../ado-api/properties-collection-ado.md)コレクションを使用して、プロバイダー固有のインデックスプロパティにアクセスします。  
  
> [!NOTE]
>  [テーブル](./tables-collection-adox.md)コレクションに既に追加されている[テーブル](./table-object-adox.md)オブジェクト**に列が**存在しない場合、**インデックス**の**Columns**コレクションに[列](./column-object-adox.md)を追加すると、エラーが発生します。  
  
> [!NOTE]
>  データプロバイダーが、 **インデックス** オブジェクトのすべてのプロパティをサポートしていない可能性があります。 プロバイダーでサポートされていないプロパティの値を設定した場合は、エラーが発生します。 新しい **インデックス** オブジェクトの場合、オブジェクトがコレクションに追加されるとエラーが発生します。 既存のオブジェクトの場合、プロパティの設定時にエラーが発生します。  
  
> [!NOTE]
>  **インデックス**オブジェクトを作成するときに、オプションのプロパティに適切な既定値が存在しても、プロバイダーがプロパティをサポートしているかどうかは保証されません。 プロバイダーがサポートしているプロパティの詳細については、プロバイダーのドキュメントを参照してください。  
  
 ここでは、次のトピックについて説明します。  
  
-   [Index オブジェクトのプロパティ、メソッド、およびイベント](./index-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Indexes Append メソッドの例 (VB)](./indexes-append-method-example-vb.md)   
 [IndexNulls プロパティの例 (VB)](./indexnulls-property-example-vb.md)   
 [PrimaryKey および Unique プロパティの例 (VB)](./primarykey-and-unique-properties-example-vb.md)   
 [順序のプロパティの例 (VB)](./sortorder-property-example-vb.md)   
 [Columns コレクション (ADOX)](./columns-collection-adox.md)   
 [Indexes コレクション (ADOX)](./indexes-collection-adox.md)   
 [Properties コレクション (ADO)](../ado-api/properties-collection-ado.md)