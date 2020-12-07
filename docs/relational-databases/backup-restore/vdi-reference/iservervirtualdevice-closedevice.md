---
title: IServerVirtualDevice::CloseDevice
titlesuffix: SQL Server VDI reference
description: この記事では、IServerVirtualDevice::CloseDevice コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 61d877fddb32f6455303a006e8955b1042ce7aa6
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96128901"
---
# <a name="iservervirtualdeviceclosedevice-vdi"></a>IServerVirtualDevice::CloseDevice (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**CloseDevice** 関数は、IServerVirtualDeviceSet2::OpenDevice で開かれた仮想デバイスを閉じます。

## <a name="syntax"></a>構文

```c
HRESULT IServerVirtualDevice::CloseDevice ();
```

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| VD_E_CLOSE | デバイスは既に閉じられています。 |
| VD_E_ABORT | インターフェイスは中止状態です。 |

## <a name="remarks"></a>解説

異常終了を強制するために SignalAbort を使用すると、CloseDevice は不要になります。 SignalAbort が使用された後に CloseDevice が呼び出された場合、何のアクションも実行されません。

## <a name="next-steps"></a>次のステップ

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。