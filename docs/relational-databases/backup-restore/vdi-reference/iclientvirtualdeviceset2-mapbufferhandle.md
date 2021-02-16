---
title: IClientVirtualDeviceSet2::MapBufferHandle
titlesuffix: SQL Server VDI reference
description: この記事では、IClientVirtualDeviceSet2::MapBufferHandle コマンドについて説明します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 28ce82433b718bc98c6a27e66385b97996fe65a0
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100347227"
---
# <a name="iclientvirtualdeviceset2mapbufferhandle-vdi"></a>IClientVirtualDeviceSet2::MapBufferHandle (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**MapBufferHandle** 関数は、他のプロセスから取得したバッファー ハンドルから有効なバッファー アドレスを取得するために使用されます。

## <a name="syntax"></a>構文

```c
HRESULT IClientVirtualDeviceSet2::MapBufferHandle (
   DWORD      dwBuffer,
   BYTE**      ppBuffer
);
```

## <a name="parameters"></a>パラメーター

*dwBuffer* これは、IClientVirtualDeviceSet2::GetBufferHandle から返されるハンドルです。

*ppBuffer* これは、現在のプロセスで有効なバッファーのアドレスです。

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| NOERROR | 関数が正常に実行されました。 |
| VD_E_PROTOCOL | 仮想デバイス セットは現在開いていません。 |
| VD_E_INVALID | ppBuffer は無効なハンドルです。 |

## <a name="remarks"></a>解説

ハンドルが正しく通信されるように注意する必要があります。 ハンドルは、1 つの仮想デバイス セットに対してローカルです。 ハンドルを共有するパートナーでは、バッファー ハンドルが、最初に取得された仮想デバイス セットのスコープ内でのみ使用されていることを確認する必要があります。

## <a name="next-steps"></a>次のステップ

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。