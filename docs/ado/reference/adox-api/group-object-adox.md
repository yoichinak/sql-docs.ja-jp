---
description: Group オブジェクト (ADOX)
title: Group オブジェクト (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Group
helpviewer_keywords:
- group object [ADOX]
ms.assetid: 55ef0ade-68ea-4da5-8aa5-4cd27d1f6d1e
author: rothja
ms.author: jroth
ms.openlocfilehash: 21514bbcbe91e1320a4a2806e545d5f7b40df8d3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984433"
---
# <a name="group-object-adox"></a>Group オブジェクト (ADOX)
セキュリティで保護されたデータベース内でアクセス許可を持つグループアカウントを表します。  
  
## <a name="remarks"></a>解説  
 [カタログ](./catalog-object-adox.md)の[Groups](./groups-collection-adox.md)コレクションは、すべてのカタログのグループアカウントを表します。 [ユーザー](./user-object-adox.md)の**Groups**コレクションは、ユーザーが属しているグループのみを表します。  
  
 **Group**オブジェクトのプロパティ、コレクション、およびメソッドを使用すると、次のことができます。  
  
-   " [名前](./name-property-adox.md) " プロパティを使用してグループを識別します。  
  
-   グループに、 [getpermissions](./getpermissions-method-adox.md) および [SetPermissions](./setpermissions-method-adox.md) メソッドを使用した読み取り、書き込み、または削除のアクセス許可があるかどうかを確認します。  
  
-   [ユーザー](./users-collection-adox.md)コレクションを使用して、グループ内のメンバーシップを持つユーザーアカウントにアクセスします。  
  
-   [プロパティ](../ado-api/properties-collection-ado.md)コレクションを使用して、プロバイダー固有のプロパティにアクセスします。  
  
 ここでは、次のトピックについて説明します。  
  
-   [Group オブジェクトのプロパティ、メソッド、およびイベント](./group-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Groups コレクション (ADOX)](./groups-collection-adox.md)   
 [Users コレクション (ADOX)](./users-collection-adox.md)