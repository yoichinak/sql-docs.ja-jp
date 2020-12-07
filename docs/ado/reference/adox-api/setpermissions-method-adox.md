---
description: SetPermissions メソッド (ADOX)
title: SetPermissions メソッド (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- User25::SetPermissions
- User25::raw_SetPermissions
- _Group25::SetPermissions
- _Group25::raw_SetPermissions
helpviewer_keywords:
- SetPermissions method [ADOX]
ms.assetid: b7f925d7-b05c-4376-bb49-f8d2c17b8b24
author: rothja
ms.author: jroth
ms.openlocfilehash: 1333fc42f98ba787cfcc139b40932038307e5592
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983293"
---
# <a name="setpermissions-method-adox"></a>SetPermissions メソッド (ADOX)
オブジェクトの [グループ](./group-object-adox.md) または [ユーザー](./user-object-adox.md) に対する権限を指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
GroupOrUser.SetPermissions Name, ObjectType, Action, Rights [, Inherit] [, ObjectTypeId]  
```  
  
#### <a name="parameters"></a>パラメーター  
 *名前*  
 権限を設定するオブジェクトの名前を示す **文字列** 値です。  
  
 *ObjectType*  
 [Objecttypeenum](./objecttypeenum.md)定数の1つであり、アクセス許可を取得するオブジェクトの型を指定する**Long 型**の値です。  
  
 *操作*  
 **Long**値。権限を設定するときに実行するアクションの種類を指定する[actionenum](./actionenum.md)定数の1つです。  
  
 *権限*  
 設定する権限を示す1つ以上の[右 Senum](./rightsenum.md)定数のビットマスクとして使用できる**Long 型**の値。  
  
 *識別子*  
 省略可能。 オブジェクトがこれらのアクセス許可を継承する方法を指定する、 [Inherittypeenum](./inherittypeenum.md)定数の1つである**Long**値。 既定値は **Adinheritnone**です。  
  
 *ObjectTypeId*  
 省略可能。 OLE DB 仕様で定義されていないプロバイダーオブジェクト型の GUID を示す **バリアント** 値です。 *ObjectType*が**Adpermobjproviderspecific**に設定されている場合、このパラメーターは必須です。それ以外の場合は使用されません。  
  
## <a name="remarks"></a>解説  
 プロバイダーがグループまたはユーザーのアクセス権の設定をサポートしていない場合、エラーが発生します。  
  
> [!NOTE]
>  **SetPermissions**を呼び出す場合、 **adaccessrevoke**にアクションを設定すると、 *Rights*パラメーターの設定が上書きされます。 *Rights*パラメーターに指定された権限を有効にする場合は、*アクション*を**adaccessrevoke**に設定しないでください。  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Group オブジェクト (ADOX)](./group-object-adox.md)  
    :::column-end:::
    :::column:::
        [User オブジェクト (ADOX)](./user-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>参照  
 [GetPermissions および SetPermissions メソッドの例 (VB)](./getpermissions-and-setpermissions-methods-example-vb.md)   
 [GetPermissions メソッド (ADOX)](./getpermissions-method-adox.md)   
 [Name プロパティ (ADOX)](./name-property-adox.md)