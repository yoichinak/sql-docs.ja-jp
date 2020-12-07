---
title: IServerVirtualDeviceSet2::AllocateBuffer
titlesuffix: SQL Server VDI reference
description: この記事では、IServerVirtualDeviceSet2::AllocateBuffer コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: d311b2253e9083c78207d1443782096b4c82a491
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96128942"
---
# <a name="iservervirtualdeviceset2allocatebuffer-vdi"></a>IServerVirtualDeviceSet2::AllocateBuffer (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**AllocateBuffer** 関数は、仮想デバイス セットから共有メモリ バッファーを取得します。

## <a name="syntax"></a>構文

```c
HRESULT IServerVirtualDeviceSet2::AllocateBuffer (
   LPVOID*      ppBuffer,
   UINT32      dwSize,
   UINT32      dwAlignment
);
```

## <a name="parameters"></a>パラメーター

*ppBuffer*: これはバッファーの先頭にポインターを返します。

*dwSize*: これは、バッファーのサイズを取得します (バイト単位)。 これには、クライアントによって要求されたプレフィックス ゾーンは含まれません。 このようなゾーンはサーバーに表示されず、バッファー アドレスが返される前に使用可能な領域があります。

*dwAlignment*: これはバッファーの配置境界を指定します。 たとえば、4096 の値を指定すると、バッファーが確実に 4096 バイトの境界に沿って配置されます。 これは、返されたアドレスの下位 12 ビットが 0 に設定される場合があることを意味します。 このパラメーターは 2 のべき乗である必要があります。

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| NOERROR | バッファーが返されます。 |
| VD_E_MEMORY | メモリ不足の状態が発生しました。 |
| VD_E_INVALID | パラメーターが無効でした。 |

## <a name="next-steps"></a>次のステップ

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。