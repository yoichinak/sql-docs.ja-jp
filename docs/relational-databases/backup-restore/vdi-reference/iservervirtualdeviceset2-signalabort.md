---
title: IServerVirtualDeviceSet2::SignalAbort
titlesuffix: SQL Server VDI reference
description: この記事では、IServerVirtualDeviceSet2::SignalAbort コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 7dd21dfb56d093a6d35d977577971545c3fb1263
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100347053"
---
# <a name="iservervirtualdeviceset2signalabort-vdi"></a>IServerVirtualDeviceSet2::SignalAbort (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**SignalAbort** 関数は、異常終了が発生することを通知します。

## <a name="syntax"></a>構文

```c
HRESULT IServerVirtualDeviceSet2::SignalAbort ();
```

## <a name="return-value"></a>戻り値

メソッド呼び出しの成功または失敗を示す *HRESULT* を返します。 値 NOERROR は、メソッド呼び出しが成功したことを示します。 0 以外の値は、エラーが発生したことを示します。

## <a name="remarks"></a>解説

サーバーでは、バックアップ操作または復元操作をいつでも中止できます。

このルーチンは、すべての操作を中止する必要があることを通知するものです。 インターフェイス全体が中止状態になります。 後続のコマンドは、いずれのデバイスでも受け入れられません。 完了エージェントは、未処理の要求ごとに ERROR_OPERATION_ABORTED を返して呼び出し元に戻ります。 クライアントで記録された完了はすべて無視されます。

サーバーによって、仮想デバイス インターフェイスから返されるバッファーまたはデバイスをこれ以上使用する必要がないことが保証されます。 次に、サーバーによって異常終了のクリーンアップが実行されます。これには、IServerVirtualDeviceSet2::Close 関数の呼び出しが含まれている必要があります。

## <a name="next-steps"></a>次のステップ

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。