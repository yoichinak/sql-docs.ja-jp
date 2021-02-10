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
ms.openlocfilehash: e37c09d4793a96056ab5d8003bf022b1d250b744
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100049682"
---
# <a name="user-object-adox"></a>User オブジェクト (ADOX)
セキュリティで保護されたデータベース内でアクセス許可を持つユーザーアカウントを表します。  
  
## <a name="remarks"></a>解説  
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