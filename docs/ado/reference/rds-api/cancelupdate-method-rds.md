---
description: CancelUpdate メソッド (RDS)
title: CancelUpdate メソッド (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
helpviewer_keywords:
- CancelUpdate method [RDS]
ms.assetid: 76d8a6e9-bc6c-4ea0-8e7a-2bae5ed06650
author: rothja
ms.author: jroth
ms.openlocfilehash: c2a845eef1d48dd8a41d1499104908db9ba10be0
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99169059"
---
# <a name="cancelupdate-method-rds"></a>CancelUpdate メソッド (RDS)
[Recordset](../ado-api/recordset-object-ado.md)オブジェクトの現在の行または新しい行に対して行われたすべての変更を取り消します。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
DataControl.CancelUpdate  
```  
  
#### <a name="parameters"></a>パラメーター  
 *DataControl*  
 RDS を表すオブジェクト変数です [。DataControl](./datacontrol-object-rds.md) オブジェクト。  
  
## <a name="remarks"></a>コメント  
 OLE DB 用の Cursor Service では、元の値のコピーと変更のキャッシュの両方が保持されます。 **CancelUpdate** を呼び出すと、変更のキャッシュが空にリセットされ、バインドされたコントロールは元のデータで更新されます。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>参照  
 [CancelUpdate メソッドの例 (VBScript)](./cancelupdate-method-example-vbscript.md)   
 [アドレス帳のコマンドボタン](../../guide/remote-data-service/address-book-command-buttons.md)   
 [Cancel メソッド (ADO)](../ado-api/cancel-method-ado.md)   
 [Cancel メソッド (RDS)](./cancel-method-rds.md)   
 [CancelBatch メソッド (ADO)](../ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate メソッド (ADO)](../ado-api/cancelupdate-method-ado.md)   
 [Refresh メソッド (RDS)](./refresh-method-rds.md)   
 [SubmitChanges メソッド (RDS)](./submitchanges-method-rds.md)