---
description: Key オブジェクト (ADOX)
title: Key オブジェクト (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Key
helpviewer_keywords:
- Key object [ADOX]
ms.assetid: 55f116fe-4d56-4892-bffe-0cdd6fc727c9
author: rothja
ms.author: jroth
ms.openlocfilehash: 51c694c39004330dd780a2deea632eee186ad9c3
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99169338"
---
# <a name="key-object-adox"></a>Key オブジェクト (ADOX)
データベーステーブルの主キー、外部キー、または一意キーフィールドを表します。  
  
## <a name="remarks"></a>コメント  
 次のコードでは、新しい **キー** が作成されます。  
  
```  
Dim obj As New Key  
```  
  
 **キー** オブジェクトのプロパティとコレクションを使用すると、次のことができます。  
  
-   [Name](./name-property-adox.md)プロパティを使用してキーを識別します。  
  
-   [Type](./type-property-key-adox.md)プロパティを使用して、キーがプライマリ、外部、または一意であるかどうかを確認します。  
  
-   [Columns](./columns-collection-adox.md)コレクションを使用して、キーのデータベース列にアクセスします。  
  
-   関連テーブルの名前を "関連付け [テーブル](./relatedtable-property-adox.md) " プロパティと共に指定します。  
  
-   [DeleteRule](./deleterule-property-adox.md)プロパティと[UpdateRule](./updaterule-property-adox.md)プロパティを使用して、主キーの削除または更新に対して実行されるアクションを確認します。  
  
 ここでは、次のトピックについて説明します。  
  
-   [Key オブジェクトのプロパティ、メソッド、およびイベント](./key-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Keys Append メソッド、Key Type、UpdateRule プロパティの例 (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Columns コレクション (ADOX)](./columns-collection-adox.md)   
 [Keys コレクション (ADOX)](./keys-collection-adox.md)