---
title: IServerVirtualDeviceSet2::EndConfiguration
titlesuffix: SQL Server VDI reference
description: この記事では、IServerVirtualDeviceSet2::EndConfiguration コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 522a2edd0a4b8ffb30cdffc9fc271f879f8d336c
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100347206"
---
# <a name="iservervirtualdeviceset2endconfiguration-vdi"></a>IServerVirtualDeviceSet2::EndConfiguration (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**EndConfiguration** 関数は、サーバーの構成が完了したことを VDI に通知します。

## <a name="syntax"></a>構文

```c
HRESULT IServerVirtualDeviceSet2::EndConfiguration ();
```

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| NOERROR | 関数が正常に実行されました。 |
| VD_E_ABORT | 中止が要求されました。 |
| VD_E_PROTOCOL | セットは構成可能な状態ではありません。 |
| VD_E_MEMORY | 'RequestBuffers' 呼び出しを介して必要なメモリを取得できませんでした。 このセットは、使用可能なバッファー領域がない構成可能な状態のままになります。 サーバーでは、バッファー要件の削減、または操作の中止のいずれかを行えます。 |

## <a name="next-steps"></a>次のステップ

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。