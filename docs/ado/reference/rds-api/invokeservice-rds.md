---
description: InvokeService (RDS)
title: InvokeService (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- InvokeService [RDS]
ms.assetid: ad45c676-ec7e-4a3a-9a6b-a54f75eb3012
author: rothja
ms.author: jroth
ms.openlocfilehash: 8d3dc0ca3744f715f080e5e34a9d4cd5e88bc8b6
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724493"
---
# <a name="invokeservice-rds"></a>InvokeService (RDS)
サポートされているオブジェクトのバージョンで、要求されたインターフェイスへのポインターを返します。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、  [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.InvokeService(REFID riid, IUknown* punkNotSoFunctionalInterface, IUknown** ppunkMoreFunctionalInterface) As HRESULT  
```  
  
#### <a name="parameters"></a>パラメーター  
 *riid*  
  
 から要求されているインターフェイスの識別子。  
  
 *punkNotSoFunctionalInterface*  
  
 からサポートされていないソースオブジェクト。  
  
 *ppunkMoreFunctionalInterface*  
  
 入出力 *Riid*で要求されたインターフェイスポインターを受け取るポインター変数のアドレス。 正常に返された場合、 *ppunkMoreFunctionalInterface* パラメーターには、オブジェクトへの要求されたインターフェイスポインターが格納されます。 オブジェクトが、 *riid*で指定されたインターフェイスをサポートしていない場合、 *ppunkMoreFunctionalInterface* は NULL に設定されます。  
  
## <a name="return-value"></a>戻り値  
 **InvokeService**メソッドの呼び出しが成功したかどうかを示す HRESULT 値。  
  
## <a name="remarks"></a>解説  
 RDS カーソルエンジンの **InvokeService** の実装では、入力行セット (または複数の結果オブジェクト) を取得し、入力行セットからカーソルエンジンを設定してから、ポインターをそれ自体に返します。  
  
## <a name="applies-to"></a>適用対象  
 [IRDSService インターフェイス (RDS)](./irdsservice-interface-rds.md)  
  
## <a name="see-also"></a>参照  
 [RDS メソッド](./rds-methods.md)