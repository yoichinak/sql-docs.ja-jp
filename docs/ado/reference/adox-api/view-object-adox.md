---
description: View オブジェクト (ADOX)
title: View オブジェクト (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- View
helpviewer_keywords:
- View object [ADOX]
ms.assetid: 653421ce-7b94-43d0-9bc6-4900f8f2af45
author: rothja
ms.author: jroth
ms.openlocfilehash: 227a52fb1ee89777d1e198e96e253ef8dd5bb979
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100049662"
---
# <a name="view-object-adox"></a>View オブジェクト (ADOX)
フィルター処理されたレコードセットまたは仮想テーブルを表します。 ADO [コマンド](../ado-api/command-object-ado.md) オブジェクトと組み合わせて使用すると、ビュー **オブジェクトを使用して** 、ビューの追加、削除、または変更を行うことができます。  
  
## <a name="remarks"></a>解説  
 ビューは、他のデータベーステーブルまたはビューから作成された仮想テーブルです。 **ビュー** オブジェクトを使用すると、プロバイダーの "create View" 構文を知らない場合や使用しなくても、ビューを作成できます。  
  
 **View** オブジェクトのプロパティを使用すると、次のことができます。  
  
-   [Name](./name-property-adox.md)プロパティを使用してビューを識別します。  
  
-   [コマンド](./command-property-adox.md)プロパティを使用してビューを追加、削除、または変更するために使用できる ADO **コマンド** オブジェクトを指定します。  
  
-   [DateCreated](./datecreated-property-adox.md)プロパティと[DateModified](./datemodified-property-adox.md)プロパティを使用して日付情報を返します。  
  
 ここでは、次のトピックについて説明します。  
  
-   [View オブジェクトのプロパティ、メソッド、およびイベント](./view-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Views および Fields コレクションの例 (VB)](./views-and-fields-collections-example-vb.md)   
 [Views Append メソッドの例 (VB)](./views-append-method-example-vb.md)   
 [Views Collection、CommandText プロパティの例 (VB)](./views-collection-commandtext-property-example-vb.md)   
 [Views Delete メソッドの例 (VB)](./views-delete-method-example-vb.md)   
 [Views コレクション (ADOX)](./views-collection-adox.md)