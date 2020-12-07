---
description: Append メソッド (ADOX Groups)
title: Append メソッド (ADOX Groups) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Groups::raw_Append
- Groups::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 56b94fc6-7ef0-4e4a-82a3-033b94c46036
author: rothja
ms.author: jroth
ms.openlocfilehash: 5890ffa77884927574f10edeb0d2acc3a428185e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985493"
---
# <a name="append-method-adox-groups"></a>Append メソッド (ADOX Groups)
[グループ](./groups-collection-adox.md)コレクションに新しい[グループ](./group-object-adox.md)オブジェクトを追加します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Groups.Append Group  
```  
  
#### <a name="parameters"></a>パラメーター  
 *グループ*  
 追加する **グループ** オブジェクト、または作成して追加するグループの名前。  
  
## <a name="remarks"></a>解説  
 [カタログ](./catalog-object-adox.md)の**Groups**コレクションは、すべてのカタログのグループアカウントを表します。 [ユーザー](./user-object-adox.md)の**Groups**コレクションは、ユーザーが属しているグループのみを表します。  
  
 プロバイダーがグループの作成をサポートしていない場合、エラーが発生します。  
  
> [!NOTE]
>  **グループ**オブジェクトを**ユーザー**オブジェクトの**groups**コレクションに追加する前に、追加するオブジェクトと同じ[名前](./name-property-adox.md)の**グループ**オブジェクトが、**カタログ**の**groups**コレクションに既に存在している必要があります。  
  
## <a name="applies-to"></a>適用対象  
 [Groups コレクション (ADOX)](./groups-collection-adox.md)  
  
## <a name="see-also"></a>参照  
 [Groups および Users Append、ChangePassword メソッドの例 (VB)](./groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append メソッド (ADOX Columns)](./append-method-adox-columns.md)   
 [Append メソッド (ADOX Indexes)](./append-method-adox-indexes.md)   
 [Append メソッド (ADOX Keys)](./append-method-adox-keys.md)   
 [Append メソッド (ADOX Procedures)](./append-method-adox-procedures.md)   
 [Append メソッド (ADOX Tables)](./append-method-adox-tables.md)   
 [Append メソッド (ADOX Users)](./append-method-adox-users.md)   
 [Append メソッド (ADOX Views)](./append-method-adox-views.md)