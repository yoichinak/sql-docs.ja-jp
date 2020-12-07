---
title: IServerVirtualDeviceSet2::BeginConfiguration
titlesuffix: SQL Server VDI reference
description: この記事では、IServerVirtualDeviceSet2::BeginConfiguration コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: d1a2bd52e923f64bac8b1865cee5e18aa2f6345e
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125354"
---
# <a name="iservervirtualdeviceset2beginconfiguration-vdi"></a>IServerVirtualDeviceSet2::BeginConfiguration (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

サーバーでは、**BeginConfiguration** 関数を呼び出して、仮想デバイス セットの構成を開始します。

## <a name="syntax"></a>構文

```c
HRESULT IServerVirtualDeviceSet2::BeginConfiguration (
   DWORD   dwFeatures,
   DWORD   dwAlignment,
   DWORD   dwBlockSize,
   DWORD   dwMaxTransferSize,
   DWORD   dwTimeout
);
```

## <a name="parameters"></a>パラメーター

*dwFeatures*: 変更された機能マスク。 VDF_WriteMedia または VDF_ReadMedia およびその両方。

*dwAlignment*: 最終的な配置。 0 の場合、既定値の dwBlockSize になります。 2 のべき乗で、>= dwBlockSize および <= 64 KB である必要があります。

*dwBlockSize*: 最大転送単位 (バイト単位)。 2 のべき乗で、>=512 および <= 64 KB である必要があります。

*dwMaxTransferSize*: 試行される最大の転送。 64 KB の倍数である必要があります。

*dwTimeout*: プライマリ クライアントが提供するバッファー領域の宣言を完了するまで待機するミリ秒数。

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| NOERROR | 仮想デバイス セットは、構成可能な状態です。 |
| VD_E_ABORT | SignalAbort が呼び出されました。 |
| VD_E_PROTOCOL | 仮想デバイス セットは接続状態ではありません。 |

## <a name="remarks"></a>解説

この関数が呼び出されると、仮想デバイス セットは構成可能な状態に移行し、バッファー レイアウトが決定されます。
基本構成が (パラメーターに従って) 設定されると、これらの値は仮想デバイス セットの有効期間中は固定されたままになります。 仮想デバイス セットの配置プロパティは、データ バッファーの配置を制御するために使用されます。 この値により、バッファー単位でオーバーライドできる配置の最小値が設定されます。

## <a name="next-steps"></a>次のステップ

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。