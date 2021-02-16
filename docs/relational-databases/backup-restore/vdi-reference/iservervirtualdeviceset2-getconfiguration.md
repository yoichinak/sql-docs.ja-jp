---
title: IServerVirtualDeviceSet2::GetConfiguration
titlesuffix: SQL Server VDI reference
description: この記事では、IServerVirtualDeviceSet2::GetConfiguration コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: d0b2b89a9ac7415c80927e4cedd28a2530c7c5bc
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100347112"
---
# <a name="iservervirtualdeviceset2getconfiguration-vdi"></a>IServerVirtualDeviceSet2::GetConfiguration (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**GetConfiguration** 関数は、クライアントによって要求された構成を取得します。

## <a name="syntax"></a>構文

```c
HRESULT IServerVirtualDeviceSet2::GetConfiguration (
   VDConfig*   pCfg
);
```

## <a name="parameters"></a>パラメーター

*pCfg*: これは、IClientVirtualDeviceSet2::Create を使用してクライアントによって指定された構成です。

## <a name="return-value"></a>戻り値

メソッド呼び出しの成功または失敗を示す *HRESULT* を返します。 値 NOERROR は、メソッド呼び出しが成功したことを示します。 0 以外の値は、エラーが発生したことを示します。

## <a name="remarks"></a>解説

サーバーには、クライアントによって提供される設定を検査して応答することが求められます。 詳細については、「構成」に関する記事を参照してください。 サーバーが指定された構成で正しく動作できないと判断されると、そのサーバーで SignalAbort を使用できます。

## <a name="next-steps"></a>次のステップ

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。