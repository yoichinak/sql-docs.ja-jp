---
description: User オブジェクト (ADOX)
title: User オブジェクト (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- User
helpviewer_keywords:
- User object [ADOX]
ms.assetid: f68e32ce-ef7c-407d-bdb5-d280947ae0e2
author: rothja
ms.author: jroth
ms.openlocfilehash: c5ca59cb5900643202c2d541072c48b275b5b5df
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99169133"
---
# <a name="user-object-adox"></a>User オブジェクト (ADOX)
セキュリティで保護されたデータベース内でアクセス許可を持つユーザーアカウントを表します。  
  
## <a name="remarks"></a>コメント  
 [カタログ](./catalog-object-adox.md)の[ユーザー](./users-collection-adox.md)コレクションは、すべてのカタログのユーザーを表します。 [グループ](./group-object-adox.md)の **ユーザー** コレクションは、特定のグループのユーザーのみを表します。  
  
 **ユーザー** オブジェクトのプロパティ、コレクション、およびメソッドを使用すると、次のことができます。  
  
-   [Name](./name-property-adox.md)プロパティを使用してユーザーを識別します。  
  
-   [ChangePassword](./changepassword-method-adox.md)メソッドを使用して、ユーザーのパスワードを変更します。  
  
-   ユーザーが [getpermissions](./getpermissions-method-adox.md) メソッドと [SetPermissions](./setpermissions-method-adox.md) メソッドを使用して、読み取り、書き込み、または削除のアクセス許可を持っているかどうかを確認します。  
  
-   [グループ](./groups-collection-adox.md)コレクションに属しているユーザーが属するグループにアクセスします。  
  
-   [プロパティ](../ado-api/properties-collection-ado.md)コレクションを使用して、プロバイダー固有のプロパティにアクセスします。  
  
-   ユーザーの [ParentCatalog](./parentcatalog-property-adox.md) を決定します。  
  
 ここでは、次のトピックについて説明します。  
  
-   [User オブジェクトのプロパティ、メソッド、およびイベント](./user-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [GetPermissions および SetPermissions メソッドの例 (VB)](./getpermissions-and-setpermissions-methods-example-vb.md)   
 [Groups コレクション (ADOX)](./groups-collection-adox.md)   
 [Users コレクション (ADOX)](./users-collection-adox.md)