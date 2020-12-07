---
title: IClientVirtualDeviceSet2::Close
titlesuffix: SQL Server VDI reference
description: この記事では、IClientVirtualDeviceSet2::Close コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: ccac23e8049884ba7bd403c91f6bde8a1f29cf84
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96128985"
---
# <a name="iclientvirtualdeviceset2close-vdi"></a>IClientVirtualDeviceSet2::Close (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**Close** 関数は、IClientVirtualDeviceSet2::Create によって作成された仮想デバイス セットを閉じるために使用されます。 これにより、仮想デバイス セットに関連付けられているすべてのリソースが解放されます。

## <a name="syntax"></a>構文

```c
HRESULT IClientVirtualDeviceSet2::Close ();
```

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| NOERROR | これは、仮想デバイス セットが正常に閉じられた場合に返されます。 |
| VD_E_PROTOCOL | 仮想デバイス セットが開かれていないため、アクションは実行されませんでした。 |
| VD_E_OPEN | デバイスがまだ開いたままでした。 |

## <a name="remarks"></a>解説

Close の呼び出しは、仮想デバイス セットによって使用されているすべてのリソースを解放する必要があるというクライアントによる宣言です。 クライアントでは、Close を呼び出す前に、データ バッファーと仮想デバイスに関連するすべてのアクティビティが終了していることを確認する必要があります。 OpenDevice によって返されたすべての仮想デバイス インターフェイスは、Close によって無効化されます。

クライアントでは、Close 呼び出しが戻った後、仮想デバイス セット インターフェイスに対して Create 呼び出しを発行することが許可されます。 この呼び出しによって、後続のバックアップまたは復元操作用に、新しい仮想デバイス セットが作成されます。

1 つ以上の仮想デバイスが開いたままの状態で Close が呼び出された場合は、VD_E_OPEN が返されます。 その場合、SignalAbort が内部でトリガーされ、可能であれば、適切なシャットダウンが行われます。 VDI リソースは解放されます。 クライアントでは、IClientVirtualDeviceSet2::Close を呼び出す前に、各デバイスで VD_E_CLOSE が通知されるまで待機する必要があります。 仮想デバイス セットが既に異常終了状態になっていることがクライアントでわかっている場合は、GetCommand から VD_E_CLOSE が通知されるのを待たず、共有バッファーでのアクティビティが終了した後すぐに、IClientVirtualDeviceSet2::Close を呼び出すことができます。

## <a name="next-steps"></a>次のステップ

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。