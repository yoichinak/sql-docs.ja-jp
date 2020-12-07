---
title: IServerVirtualDeviceSet2::Open
titlesuffix: SQL Server VDI reference
description: この記事では、IServerVirtualDeviceSet2::Open コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 0e4d91e75ee2c030112a1e826366d5caee537ee3
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96128862"
---
# <a name="iservervirtualdeviceset2open-vdi"></a>IServerVirtualDeviceSet2::Open (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**Open** 関数は、サーバーで設定された仮想デバイスを開きます。これは、COM によって提供されるインターフェイス ハンドルを使用した最初の呼び出しである必要があります。

## <a name="syntax"></a>構文

```c
HRESULT IServerVirtualDeviceSet2::Open (
   LPCWSTR      lpInstanceName,
   LPCWSTR      lpName
);
```

## <a name="parameters"></a>パラメーター

*lpInstanceName*: この文字列により、SQL コマンドの送信先となる SQL Server インスタンスが識別されます。 現在のマシン上の既定のインスタンスを識別するために、NULL を渡すことができる場合があります。

*lpName*: これは、BACKUP または RESTORE コマンドの最初の VIRTUAL_DEVICE= 句で指定されます。 この名前は、クライアントによって作成された仮想デバイス セットへのアクセスを取得するためのキーとして使用されます。

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| NOERROR | 関数が正常に実行されました。 |
| VD_E_INVALID | 指定された名前で、サーバーからアクセス可能な仮想デバイス セットが識別できませんでした。 |

## <a name="remarks"></a>解説

この関数が正常に呼び出されると、サーバーで GetConfiguration と SetConfiguration を使用して仮想デバイス セットの構成を続行できます。

## <a name="next-steps"></a>次のステップ

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。