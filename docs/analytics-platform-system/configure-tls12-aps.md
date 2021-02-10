---
title: TLS 1.2 の構成
description: APS で TLS 1.2 を構成するための推奨事項
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 10/29/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 561a0a4f1d45d78e0f2fd23d61aae67f6adb6ff7
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100052743"
---
# <a name="configure-tls-12-in-aps"></a>APS で TLS 1.2 を構成する

TLS 1.2 のみを使用するように AP をセキュリティで保護するには、すべての物理ホストと仮想ホストで他のプロトコルを明示的に無効にする必要があります。 プロトコルを無効にするには、レジストリ設定の変更が必要です。 レジストリを変更するには、仮想ホストと物理ホストを再起動する必要があります。

> [!WARNING]
> このセクションの作業には、レジストリを変更する手順が含まれます。 ただし、データの損失を引き起こす可能性があり、オペレーティングシステムの再インストールが必要になる可能性があるレジストリを誤って変更すると、深刻な問題が発生する可能性があります。 レジストリを変更する前に、バックアップしておくことを強くお勧めします。 バックアップがあれば、問題が生じた場合でもレジストリを復元できます。 バックアップおよび復元方法の詳細を参照するには、以下の Microsoft サポート技術情報番号をクリックしてください。<br>
[322756](https://support.microsoft.com/help/322756) Windows でレジストリをバックアップおよび復元する方法

**切り替える**
```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0]
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1]
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
```

また、APS SSIS 変換先アダプターなどのツールがインストールされているクライアントコンピューターに、次のキーを設定します。
```
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001 
```



