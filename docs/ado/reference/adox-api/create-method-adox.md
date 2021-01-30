---
description: Create メソッド (ADOX)
title: Create メソッド (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- _Catalog::raw_Create
- _Catalog::Create
helpviewer_keywords:
- Create method [ADOX]
ms.assetid: 64f5c21c-b581-42d8-bdc7-c4f1bebaf105
author: rothja
ms.author: jroth
ms.openlocfilehash: b44be7497ca6952dd88d6f18ac0b42a6c989db36
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99172205"
---
# <a name="create-method-adox"></a>Create メソッド (ADOX)
新しいカタログを作成します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Catalog.Create ConnectString  
```  
  
#### <a name="parameters"></a>パラメーター  
 *ConnectString*  
 データソースへの接続に使用する **文字列** 値。  
  
## <a name="remarks"></a>コメント  
 **Create** メソッドは、 *connectstring* に指定されたデータソースへの新しい ADO [接続](../ado-api/connection-object-ado.md)を作成して開きます。 成功した場合は、新しい **接続** オブジェクトが [ActiveConnection](./activeconnection-property-adox.md) プロパティに割り当てられます。  
  
 プロバイダーが新しいカタログの作成をサポートしていない場合は、エラーが発生します。  
  
## <a name="applies-to"></a>適用対象  
 [Catalog オブジェクト (ADOX)](./catalog-object-adox.md)  
  
## <a name="see-also"></a>参照  
 [Create メソッドの例 (VB)](./create-method-example-vb.md)   
 [ActiveConnection プロパティ (ADOX)](./activeconnection-property-adox.md)