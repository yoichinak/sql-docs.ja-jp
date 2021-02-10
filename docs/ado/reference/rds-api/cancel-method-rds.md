---
description: Cancel メソッド (RDS)
title: Cancel メソッド (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
helpviewer_keywords:
- Cancel method [RDS]
ms.assetid: 560b5b3d-fba9-4275-8920-9c3e186134f7
author: rothja
ms.author: jroth
ms.openlocfilehash: 5c3c1c78d69db0ceba435c91f13172a5ee77a697
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100049552"
---
# <a name="cancel-method-rds"></a>Cancel メソッド (RDS)
保留中の非同期メソッド呼び出しの実行を取り消します。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
RDS.DataControl.Cancel  
```  
  
## <a name="remarks"></a>解説  
 **Cancel** を呼び出すと、 [ReadyState](./readystate-property-rds.md)が自動的に **Adcreadystateloaded** に設定され、[レコードセット](../ado-api/recordset-object-ado.md)は空になります。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>参照  
 [Cancel メソッドの例 (VBScript)](./cancel-method-example-vbscript.md)   
 [Cancel メソッド (ADO)](../ado-api/cancel-method-ado.md)   
 [CancelBatch メソッド (ADO)](../ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate メソッド (ADO)](../ado-api/cancelupdate-method-ado.md)   
 [CancelUpdate メソッド (RDS)](./cancelupdate-method-rds.md)   
 [ExecuteOptions プロパティ (RDS)](./executeoptions-property-rds.md)