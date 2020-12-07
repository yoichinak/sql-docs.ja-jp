---
title: IClientVirtualDeviceSet2::GetBufferHandle
titlesuffix: SQL Server VDI reference
description: この記事では、IClientVirtualDeviceSet2::GetBufferHandle コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 1c3b771e3b5ec69cbfb33a21496ffd0455d0b2a7
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96128972"
---
# <a name="iclientvirtualdeviceset2getbufferhandle-vdi"></a>IClientVirtualDeviceSet2::GetBufferHandle (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

アプリケーションによっては、**IClientVirtualDevice2::GetCommand** によって返されるバッファーを操作するために、複数のプロセスが必要になる場合があります。 その場合、コマンドを受け取るプロセスでは、**GetBufferHandle** を使用して、バッファーを識別するプロセス独立ハンドルを取得することができます。 その後、このハンドルによって、同じ仮想デバイス セットを開いている他のプロセスと通信することができます。 そのプロセスでは、IClientVirtualDeviceSet2::MapBufferHandle を使用して、バッファーのアドレスが取得されます。 このアドレスは、パートナーとは異なるアドレスになる可能性があります。なぜなら、各プロセスが異なるアドレスでバッファーをマッピングしている可能性があるからです。

## <a name="syntax"></a>構文

```c
HRESULT IClientVirtualDeviceSet2::GetBufferHandle (
   BYTE*         pBuffer,
   DWORD*      pBufferHandle
);
```

## <a name="parameters"></a>パラメーター

*pBuffer*: これは、Read または Write コマンドから取得されたバッファーのアドレスです。

*pBufferHandle*: バッファーの一意の識別子が返されます。

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| NOERROR | 関数が正常に実行されました。 |
| VD_E_PROTOCOL | 仮想デバイス セットは現在開いていません。 |
| VD_E_INVALID | pBuffer は有効なアドレスではありません。 |

## <a name="remarks"></a>解説

GetBufferHandle 関数を呼び出すプロセスでは、データ転送が完了したときに IClientVirtualDevice2::CompleteCommand を呼び出す必要があります。

## <a name="next-steps"></a>次のステップ

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。