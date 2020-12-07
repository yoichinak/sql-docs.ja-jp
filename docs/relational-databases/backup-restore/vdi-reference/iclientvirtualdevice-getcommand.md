---
title: IClientVirtualDevice::GetCommand
titlesuffix: SQL Server VDI reference
description: この記事では、IClientVirtualDevice::GetCommand コマンドについて説明します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 226c11ebde66450431719c8d6c2e027479eb3ca4
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125417"
---
# <a name="iclientvirtualdevicegetcommand-vdi"></a>IClientVirtualDevice::GetCommand (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**GetCommand** 関数は、デバイスのキューに登録されている次のコマンドを取得するために使用します。 要求された場合、この関数は次のコマンドを待機します。

## <a name="syntax"></a>構文

```c
HRESULT IClientVirtualDevice::GetCommand (
   DWORD               dwTimeOut,
   VDC_Command**      const ppCmd
);
```

## <a name="parameters"></a>パラメーター

*ppCmd* コマンドが正常に返された場合は、このパラメーターによって、実行するコマンドのアドレスが返されます。 返されるメモリは読み取り専用です。 コマンドが完了すると、このポインターは CompleteCommand ルーチンに渡されます。 各コマンドの詳細については、コマンドに関するページを参照してください。

*dwTimeOut* これは、ミリ秒単位の待機時間です。 無期限に待機するには、INFINTE を使用します。 コマンドをポーリングするには、0 を使用します。 現在使用できるコマンドがない場合は、VD_E_TIMEOUT が返されます。 タイムアウトが発生した場合は、クライアントによって次のアクションが決定されます。

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| NOERROR | コマンドがフェッチされました。 |
| VD_E_CLOSE | デバイスがサーバーによって閉じられました。 |
| VD_E_TIMEOUT | 使用可能なコマンドがなく、タイムアウトになりました。 |
| VD_E_ABORT | クライアントまたはサーバーが SignalAbort を使用して強制的にシャットダウンされました。 |

## <a name="remarks"></a>解説

VD_E_CLOSE が返された場合は、SQL Server によってデバイスが閉じられたことを意味します。 これは通常のシャットダウンの一部です。 すべてのデバイスが閉じられると、クライアントによって IClientVirtualDeviceSet2::Close が呼び出され、仮想デバイス セットが閉じられます。

このルーチンで、コマンドを待機するためにブロックする必要がある場合、スレッドは警告可能な状態のまま維持されます。

## <a name="next-steps"></a>次のステップ

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。