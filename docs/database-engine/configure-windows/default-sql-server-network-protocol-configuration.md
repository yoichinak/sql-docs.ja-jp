---
title: SQL Server の既定のネットワーク プロトコル構成 | Microsoft Docs
description: SQL Server のインストール時にネットワーク プロトコルがオンになるかオフになるかに影響する要素について説明します。 インストール後にプロトコルを構成する方法について説明します。
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- protocols [SQL Server], default settings
- default protocols, after install
ms.assetid: 635ea361-a797-4971-bd05-e3415862bc5c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d5463ac163271cf14f5b52167559bc8f3f53d805
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2020
ms.locfileid: "91671115"
---
# <a name="default-sql-server-network-protocol-configuration"></a>SQL Server の既定のネットワーク プロトコル構成
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、セキュリティ強化のため、一部の新規インストールではネットワーク接続を無効にします。 Enterprise エディション、Standard エディション、Evaluation エディション、または Workgroup エディションを使っている場合、または以前からインストールされている [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] が存在する場合は、TCP/IP を使うネットワーク接続は無効になりません。 すべてのインストールについて、サーバーへのローカル接続を許可する共有メモリ プロトコルは有効化されています。 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Browser サービスは、インストール状態とインストール オプションに応じて、停止される場合があります。

インストール後にネットワーク プロトコルを構成するには、 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 構成マネージャーの [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ネットワークの構成ノードを使用します。 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Browser サービスを自動的に開始するように構成するには、 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 構成マネージャーの [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] のサービス ノードを使用します。 詳細については、「 [サーバー ネットワーク プロトコルの有効化または無効化](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)」を参照してください。


## <a name="default-configuration"></a>既定の構成

次の表は、インストール後の構成状態を示しています。

|Edition | 新規インストール/以前のインストールが存在する | 共有メモリ | TCP/IP | 名前付きパイプ|
| -------- | -- | -- | -- | --  |  
|Enterprise | 新しいインストール | Enabled | Enabled | ネットワーク接続に対して無効です。|
|Standard | 新しいインストール | Enabled | Enabled | ネットワーク接続に対して無効です。|
|Web | 新しいインストール | Enabled | Enabled | ネットワーク接続に対して無効です。|
|Developer | 新しいインストール | Enabled | 無効 | ネットワーク接続に対して無効です。|
|評価 | 新しいインストール | Enabled | Enabled | ネットワーク接続に対して無効です。|
|SQL Server Express | 新しいインストール | Enabled | 無効 | ネットワーク接続に対して無効です。|
|全エディション | 以前のインストールがありますが、アップグレードされていません。 | 新規インストールと同じ | 新規インストールと同じ | 新規インストールと同じ|
|全エディション | アップグレード | Enabled | 以前のインストールの設定が維持されます。 | 以前のインストールの設定が維持されます。|


>[!NOTE]
> インスタンスが [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] フェールオーバー クラスター上で動作している場合、このインスタンスは [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] セットアップの実行時に [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 用に指定された各 IP アドレスのポート上でリッスンします。
 
>[!NOTE]
> コマンド プロンプト引数を指定して [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] をインストールする場合は、 `TCPENABLED` パラメーターおよび `NPENABLED` パラメーターを使用して、有効にするプロトコルを指定できます。 詳細については、「 [コマンド プロンプトからの SQL Server のインストール](../install-windows/install-sql-server-from-the-command-prompt.md)」を参照してください。

## <a name="creating-a-connection-string"></a>接続文字列の作成

接続文字列のサンプルについては、次のトピックを参照してください。
* [共有メモリ プロトコルを使用した有効な接続文字列の作成](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)
* [TCP/IP を使用した有効な接続文字列の作成](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)



## <a name="ssnoversion_md-browser-settings"></a>[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ブラウザーの設定

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Browser サービスは、セットアップ時に自動的に起動するように構成できます。 既定では、以下の条件が満たされている場合、自動的に起動されます。

* インストールをアップグレードする場合
* [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] の他のインスタンスとサイド バイ サイドでインストールする場合
* クラスターにインストールする場合
* [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Express のすべてのインスタンスを含む、データベース エンジンの名前付きインスタンスをインストールする場合
* Analysis Services の名前付きインスタンスをインストールする場合

## <a name="see-also"></a>参照

[SQL Server 2016 のインストールに必要なハードウェアおよびソフトウェア](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)

[セキュリティ構成](../../relational-databases/security/surface-area-configuration.md)