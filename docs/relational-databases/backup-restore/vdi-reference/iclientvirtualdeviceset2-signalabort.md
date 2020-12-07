---
title: IClientVirtualDeviceSet2::SignalAbort
titlesuffix: SQL Server VDI reference
description: この記事では、IClientVirtualDeviceSet2::SignalAbort コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: d36a08586a6903a6e85bb4bad4d6344a54938cd2
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125387"
---
# <a name="iclientvirtualdeviceset2signalabort-vdi"></a>IClientVirtualDeviceSet2::SignalAbort (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**SignalAbort** 関数は、異常終了が発生することを通知するために使用されます。

## <a name="syntax"></a>構文

```c
HRESULT IClientVirtualDeviceSet2::SignalAbort ();
```

## <a name="return-value"></a>戻り値

メソッド呼び出しの成功または失敗を示す *HRESULT* を返します。 値 NOERROR は、メソッド呼び出しが成功したことを示します。 0 以外の値は、エラーが発生したことを示します。

## <a name="remarks"></a>解説

クライアントでは、バックアップ操作または復元操作をいつでも中止できます。 このルーチンは、すべての操作を中止する必要があることを通知するものです。 仮想デバイス セット全体の状態が、中止状態になります。 後続のコマンドは、いずれのデバイスについても返されません。 未完了のコマンドはすべて自動的に完了し、完了コードとして ERROR_OPERATION_ABORTED が返されます。 クライアントでは、クライアントに提供されたバッファーの未処理の使用を安全に終了した後、IClientVirtualDeviceSet2::Close を呼び出す必要があります。 詳細については、「異常終了」に関する記事を参照してください。

## <a name="next-steps"></a>次のステップ

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。