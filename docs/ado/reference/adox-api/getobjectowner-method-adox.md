---
description: GetObjectOwner メソッド (ADOX)
title: GetObjectOwner メソッド (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Catalog::raw_GetObjectOwner
- _Catalog::GetObjectOwner
helpviewer_keywords:
- GetObjectOwner method [ADOX]
ms.assetid: 8965adf0-9075-4125-8142-73eb700029c3
author: rothja
ms.author: jroth
ms.openlocfilehash: 3f065e2625afa088489f08ade9f4ef00c5eb7d4d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984543"
---
# <a name="getobjectowner-method-adox"></a>GetObjectOwner メソッド (ADOX)
[カタログ](./catalog-object-adox.md)内のオブジェクトの所有者を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Owner = Catalog.GetObjectOwner(ObjectName, ObjectType [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>戻り値  
 オブジェクトを所有する[ユーザー](./user-object-adox.md)または[グループ](./group-object-adox.md)の[名前](./name-property-adox.md)を指定する**文字列**値を返します。  
  
#### <a name="parameters"></a>パラメーター  
 *ObjectName*  
 所有者を返す対象のオブジェクトの名前を示す **文字列** 値です。  
  
 *ObjectType*  
 オブジェクトの所有者を取得するオブジェクトの型を指定する、 [Objecttypeenum](./objecttypeenum.md)定数の1つを指定する**Long 型**の値です。  
  
 *ObjectTypeId*  
 省略可能。 OLE DB 仕様で定義されていないプロバイダーオブジェクト型の GUID を示す **バリアント** 値です。 *ObjectType*が**Adpermobjproviderspecific**に設定されている場合、このパラメーターは必須です。それ以外の場合は使用されません。  
  
## <a name="remarks"></a>解説  
 プロバイダーがオブジェクトの所有者を返すことをサポートしていない場合、エラーが発生します。  
  
## <a name="applies-to"></a>適用対象  
 [Catalog オブジェクト (ADOX)](./catalog-object-adox.md)  
  
## <a name="see-also"></a>参照  
 [GetObjectOwner メソッドと SetObjectOwner メソッドの例 (VB)](./getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [SetObjectOwner メソッド](./setobjectowner-method.md)