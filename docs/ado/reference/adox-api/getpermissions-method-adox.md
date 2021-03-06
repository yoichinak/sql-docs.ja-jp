---
description: GetPermissions メソッド (ADOX)
title: GetPermissions メソッド (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- _User25::GetPermissions
- _Group25::raw_GetPermissions
- _Group25::GetPermissions
- _User25::raw_GetPermissions
helpviewer_keywords:
- GetPermissions method [ADOX]
ms.assetid: df201c1f-c76a-465d-98f0-83b7fc36e6e3
author: rothja
ms.author: jroth
ms.openlocfilehash: 6a90b95cb6ca9d020ce841524caa498743b8b1d6
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100050082"
---
# <a name="getpermissions-method-adox"></a>GetPermissions メソッド (ADOX)
オブジェクトまたはオブジェクトコンテナーに対する [グループ](./group-object-adox.md) または [ユーザー](./user-object-adox.md) の権限を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
ReturnValue=GroupOrUser.GetPermissions(Name, ObjectType    [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>戻り値  
 グループまたはユーザーがオブジェクトに対して持っているアクセス許可を含むビットマスクを指定する **Long 型** の値を返します。 この値は、1つ以上の [右 Senum](./rightsenum.md) 定数にすることができます。  
  
#### <a name="parameters"></a>パラメーター  
 *名前*  
 権限を設定するオブジェクトの名前を示す **バリアント** 値です。 オブジェクトコンテナーのアクセス許可を取得する場合は、[ *名前* を null 値に設定します。  
  
 *ObjectType*  
 [Objecttypeenum](./objecttypeenum.md)定数の1つであり、アクセス許可を取得するオブジェクトの型を指定する **Long 型** の値です。  
  
 *ObjectTypeId*  
 任意。 OLE DB 仕様で定義されていないプロバイダーオブジェクト型の GUID を示す **バリアント** 値です。 *ObjectType* が **Adpermobjproviderspecific** に設定されている場合、このパラメーターは必須です。それ以外の場合は使用されません。  
  
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
 [Name プロパティ (ADOX)](./name-property-adox.md)   
 [SetPermissions メソッド (ADOX)](./setpermissions-method-adox.md)