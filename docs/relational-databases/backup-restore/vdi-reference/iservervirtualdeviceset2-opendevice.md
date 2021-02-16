---
title: IServerVirtualDeviceSet2::OpenDevice
titlesuffix: SQL Server VDI reference
description: この記事では、IServerVirtualDeviceSet2::OpenDevice コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: d0da9263463fbe6c875bc411f88ec7f8ab440f46
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100347076"
---
# <a name="iservervirtualdeviceset2opendevice-vdi"></a>IServerVirtualDeviceSet2::OpenDevice (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**OpenDevice** 関数は、仮想デバイス セットから仮想デバイス インターフェイスを取得します。

## <a name="syntax"></a>構文

```c
HRESULT IServerVirtualDeviceSet2::OpenDevice (
   LPCWSTR                     lpName,
   IServerVirtualDevice**      ppVirtualDevice
);
```

## <a name="parameters"></a>パラメーター

*lpName*: これは、BACKUP または RESTORE コマンドの最初の VIRTUAL_DEVICE= 句で指定されます。 この名前は、クライアントによって作成された仮想デバイス セットへのアクセスを取得するためのキーとして使用されます。

*ppVirtualDevice*: これは、仮想デバイス インターフェイスを返すために使用されます。

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| NOERROR | 関数が正常に実行されました。 |
| VD_E_OPEN |すべてのデバイスが開かれています。 |

## <a name="remarks"></a>解説

各呼び出しでは、次の開かれていないデバイスが返されます。 この関数は、仮想デバイス セットの構成で指定されたデバイスの数と同じ回数だけ呼び出すことができます。

## <a name="next-steps"></a>次のステップ

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。