---
description: Groups コレクション (ADOX)
title: Groups コレクション (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Groups
- User::Groups
- Catalog::Groups
helpviewer_keywords:
- Groups collection [ADOX]
ms.assetid: 09aa7b0a-69d5-4564-80a7-20ad8189670f
author: rothja
ms.author: jroth
ms.openlocfilehash: e0cbcc0941c3c2c7158d15bc73f07e4b835db4f3
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99164232"
---
# <a name="groups-collection-adox"></a>Groups コレクション (ADOX)
カタログまたはユーザーの格納されているすべての [グループ](./group-object-adox.md) オブジェクトが含まれます。  
  
## <a name="remarks"></a>コメント  
 [カタログ](./catalog-object-adox.md)の **Groups** コレクションは、すべてのカタログのグループアカウントを表します。 [ユーザー](./user-object-adox.md)の **Groups** コレクションは、ユーザーが属しているグループのみを表します。  
  
 **Groups** コレクションの [Append](./append-method-adox-groups.md)メソッドは、ADOX で一意です。 次のようにすることができます。  
  
-   **追加** メソッドを使用して、新しいセキュリティグループをコレクションに追加します。  
  
 その他のプロパティとメソッドは、ADO コレクションの標準です。 次のようにすることができます。  
  
-   [項目](../ado-api/item-property-ado.md)プロパティを使用して、コレクション内のグループにアクセスします。  
  
-   [Count](../ado-api/count-property-ado.md)プロパティを使用して、コレクションに含まれるグループの数を返します。  
  
-   [Delete](./delete-method-adox-collections.md)メソッドを使用して、コレクションからグループを削除します。  
  
-   [更新](../ado-api/refresh-method-ado.md)メソッドを使用して、現在のデータベーススキーマを反映するように、コレクション内のオブジェクトを更新します。  
  
> [!NOTE]
>  **グループ** オブジェクトを **ユーザー** オブジェクトの **groups** コレクションに追加する前に、追加するオブジェクトと同じ [名前](./name-property-adox.md)の **グループ** オブジェクトが、**カタログ** の **groups** コレクションに既に存在している必要があります。  
  
 ここでは、次のトピックについて説明します。  
  
-   [Groups コレクションのプロパティ、メソッド、およびイベント](./groups-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Catalog オブジェクト (ADOX)](./catalog-object-adox.md)   
 [Group オブジェクト (ADOX)](./group-object-adox.md)