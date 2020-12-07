---
title: IServerVirtualDeviceSet2::FreeBuffer
titlesuffix: SQL Server VDI reference
description: この記事では、IServerVirtualDeviceSet2::FreeBuffer コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: d75d859b4340e95d705037b603f186871acb3b42
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125350"
---
# <a name="iservervirtualdeviceset2freebuffer-vdi"></a>IServerVirtualDeviceSet2::FreeBuffer (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**FreeBuffer** 関数は、仮想デバイス セットから共有メモリ バッファーを取得します。

## <a name="syntax"></a>構文

```c
HRESULT IServerVirtualDeviceSet2::FreeBuffer (
   LPVOID   pBuffer,
   UINT32   dwSize
);
```

## <a name="parameters"></a>パラメーター

*pBuffer*: これは、IServerVirtualDeviceSet2::AllocateBuffer によって返されるバッファーを返します。

*dwSize*: これは、バッファーのサイズを取得します (バイト単位)。 これには、クライアントによって要求されたプレフィックス ゾーンは含まれません。 このようなゾーンはサーバーに表示されず、バッファー アドレスが返される前に使用可能な領域があります。

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| NOERROR | バッファーが返されます。 |
| VD_E_INVALID | パラメーターが無効でした。 |

## <a name="next-steps"></a>次のステップ

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。