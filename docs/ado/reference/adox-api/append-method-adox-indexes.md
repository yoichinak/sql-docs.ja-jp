---
description: Append メソッド (ADOX Indexes)
title: Append メソッド (ADOX Indexes) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Indexes::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6695769f-275b-4b70-81bd-1a5f7d74926c
author: rothja
ms.author: jroth
ms.openlocfilehash: 00b37055efe15f204049d02c337b54c228468419
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985513"
---
# <a name="append-method-adox-indexes"></a>Append メソッド (ADOX Indexes)
新しい [Index](./index-object-adox.md) オブジェクトを [Indexes](./indexes-collection-adox.md) コレクションに追加します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Indexes.Append Index [,Columns]  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Index*  
 追加する **インデックス** オブジェクト、または作成および追加するインデックスの名前。  
  
 *[列]*  
 省略可能。 インデックスを作成する列の名前を指定する **バリアント** 値です (複数可)。 *Columns*パラメーターは、[列](./column-object-adox.md)オブジェクトまたはオブジェクトの[Name](./name-property-adox.md)プロパティの値に対応します。  
  
## <a name="remarks"></a>解説  
 *Columns*パラメーターには、列名または列名の配列のいずれかを指定できます。  
  
 プロバイダーがインデックスの作成をサポートしていない場合、エラーが発生します。  
  
## <a name="applies-to"></a>適用対象  
 [Indexes コレクション (ADOX)](./indexes-collection-adox.md)  
  
## <a name="see-also"></a>参照  
 [Indexes Append メソッドの例 (VB)](./indexes-append-method-example-vb.md)   
 [Append メソッド (ADOX Columns)](./append-method-adox-columns.md)   
 [Append メソッド (ADOX Groups)](./append-method-adox-groups.md)   
 [Append メソッド (ADOX Keys)](./append-method-adox-keys.md)   
 [Append メソッド (ADOX Procedures)](./append-method-adox-procedures.md)   
 [Append メソッド (ADOX Tables)](./append-method-adox-tables.md)   
 [Append メソッド (ADOX Users)](./append-method-adox-users.md)   
 [Append メソッド (ADOX Views)](./append-method-adox-views.md)