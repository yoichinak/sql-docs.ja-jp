---
description: Group オブジェクト (ADOX)
title: Group オブジェクト (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Group
helpviewer_keywords:
- group object [ADOX]
ms.assetid: 55ef0ade-68ea-4da5-8aa5-4cd27d1f6d1e
author: rothja
ms.author: jroth
ms.openlocfilehash: b72179e91ad4c9742ffd42a70ff37e33f402d8e3
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100054197"
---
# <a name="group-object-adox"></a>Group オブジェクト (ADOX)
セキュリティで保護されたデータベース内でアクセス許可を持つグループアカウントを表します。  
  
## <a name="remarks"></a>解説  
 [カタログ](./catalog-object-adox.md)の[Groups](./groups-collection-adox.md)コレクションは、すべてのカタログのグループアカウントを表します。 [ユーザー](./user-object-adox.md)の **Groups** コレクションは、ユーザーが属しているグループのみを表します。  
  
 **Group** オブジェクトのプロパティ、コレクション、およびメソッドを使用すると、次のことができます。  
  
-   " [名前](./name-property-adox.md) " プロパティを使用してグループを識別します。  
  
-   グループに、 [getpermissions](./getpermissions-method-adox.md) および [SetPermissions](./setpermissions-method-adox.md) メソッドを使用した読み取り、書き込み、または削除のアクセス許可があるかどうかを確認します。  
  
-   [ユーザー](./users-collection-adox.md)コレクションを使用して、グループ内のメンバーシップを持つユーザーアカウントにアクセスします。  
  
-   [プロパティ](../ado-api/properties-collection-ado.md)コレクションを使用して、プロバイダー固有のプロパティにアクセスします。  
  
 ここでは、次のトピックについて説明します。  
  
-   [Group オブジェクトのプロパティ、メソッド、およびイベント](./group-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Groups コレクション (ADOX)](./groups-collection-adox.md)   
 [Users コレクション (ADOX)](./users-collection-adox.md)