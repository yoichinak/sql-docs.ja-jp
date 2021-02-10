---
description: Append メソッド (ADOX Indexes)
title: Append メソッド (ADOX Indexes) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Indexes::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6695769f-275b-4b70-81bd-1a5f7d74926c
author: rothja
ms.author: jroth
ms.openlocfilehash: feb259809798e3260e4e201c4658bfbc1455f168
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100050543"
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
 任意。 インデックスを作成する列の名前を指定する **バリアント** 値です (複数可)。 *Columns* パラメーターは、[列](./column-object-adox.md)オブジェクトまたはオブジェクトの [Name](./name-property-adox.md)プロパティの値に対応します。  
  
## <a name="remarks"></a>解説  
 *Columns* パラメーターには、列名または列名の配列のいずれかを指定できます。  
  
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