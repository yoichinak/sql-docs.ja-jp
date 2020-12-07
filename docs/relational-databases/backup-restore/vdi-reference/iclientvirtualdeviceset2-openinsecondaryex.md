---
title: IClientVirtualDeviceSet2::OpenInSecondaryEx
titlesuffix: SQL Server VDI reference
description: この記事では、IClientVirtualDeviceSet2::OpenInSecondaryEx コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: a5b2a680e34d6aa6c174cc356a2cb99bee75131f
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96128954"
---
# <a name="iclientvirtualdeviceset2openinsecondaryex-vdi"></a>IClientVirtualDeviceSet2::OpenInSecondaryEx (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**OpenInSecondaryEx** 関数では、セカンダリ クライアントで設定された仮想デバイスが開かれます。 プライマリ クライアントには、既に CreateEx と GetConfiguration を使用して仮想デバイス セットが設定されている必要があります。

## <a name="syntax"></a>構文

```c
HRESULT IClientVirtualDeviceSet2::OpenInSecondaryEx (
   LPCWSTR      lpInstanceName,
   LPCWSTR      lpSetName
);
```

## <a name="parameters"></a>パラメーター

*lpInstanceName*: この文字列により、SQL コマンドの送信先となる SQL Server インスタンスが識別されます。

*lpSetName*: これによりセットが識別されます。 この名前は大文字と小文字が区別されます。また、IClientVirtualDeviceSet2::Create を呼び出す際にプライマリ クライアントによって使用された名前と一致する必要があります。

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| NOERROR | 関数が正常に実行されました。 |
| VD_E_PROTOCOL | 仮想デバイス セットが開かれているか、またはセカンダリ クライアントからのオープン要求を受け入れる準備が仮想デバイス セットで整っていません。 |
| VD_E_ABORT | 操作を中止しています。 |

## <a name="remarks"></a>解説

複数のプロセス モデルを使用している場合、セカンダリ クライアントの正常終了と異常終了を検出する役割は、プライマリ クライアントが担います。

インスタンス名で、T-SQL を発行するインスタンスを識別する必要があります。 NULL は既定のインスタンスを識別します。 "machineName\" プレフィックスは許可されていません。

OpenInSecondaryEx により、元の SQL Server バージョン 7.0 インターフェイスで定義された元の IClientVirtualDeviceSet::OpenInSecondary が置き換えられます。 新しい開発では OpenInSecondaryEx を使用する必要があります。

## <a name="next-steps"></a>次のステップ

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。