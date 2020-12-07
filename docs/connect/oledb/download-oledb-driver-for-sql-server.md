---
title: Microsoft OLE DB Driver for SQL Server のダウンロード | Microsoft Docs
description: SQL Server や Azure SQL Database に接続するネイティブ Windows アプリケーションを開発するには、Microsoft OLE DB Driver for SQL Server をダウンロードします。
ms.date: 05/25/2020
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4424f11e4b8d31c964d024b3ecaf90bec0cd7c21
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727343"
---
# <a name="download-microsoft-ole-db-driver-for-sql-server"></a>Microsoft OLE DB Driver for SQL Server のダウンロード

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

OLE DB Driver for SQL Server はスタンドアロンのデータ アクセス アプリケーション プログラミング インターフェイス (API) で、OLE DB に使用されます。 OLE DB Driver for SQL Server は Windows 上で利用でき、SQL OLE DB ドライバーが 1 つのダイナミック リンク ライブラリ (DLL) で提供されます。

## <a name="download"></a>ダウンロード

Microsoft OLE DB Driver for SQL Server の再頒布可能インストーラーでは、新しい SQL Server 機能を利用するために実行時に必要なクライアント コンポーネントがインストールされます。 バージョン 18.3 以降のインストーラーには、Microsoft Active Directory 認証ライブラリ (ADAL.dll) も含まれていてインストールされます。

Microsoft OLE DB Driver 18.4 for SQL Server は、最新の一般提供 (GA) バージョンです。 以前のバージョンの Microsoft OLE DB Driver 18 for SQL Server がインストールされている場合は、18.4 をインストールすると 18.4 にアップグレードされます。

**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft OLE DB Driver for SQL Server r (x64) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2129954)**  
**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft OLE DB Driver for SQL Server r (x86) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2131003)**  

### <a name="version-information"></a>バージョン情報

- リリース番号:18.4.0
- リリース日:2020 年 5 月 30 日

> [!Note]
> 英語以外のバージョンからこのページにアクセスしていて、最新の内容を見たい場合は、[サイトの英語 (米国) 版]()をご覧ください。 [使用できる言語](#available-languages)を選択して、英語 (米国) 版のサイトから別の言語をダウンロードできます。ます。

## <a name="available-languages"></a>使用できる言語

Microsoft OLE DB Driver for SQL Server のこのリリースは、次の言語でインストールできます。

Microsoft OLE DB Driver 18.4 for SQL Server (x64):  
[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x40a)

Microsoft OLE DB Driver 18.4 for SQL Server (x86):  
[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x40a)

## <a name="release-notes"></a>リリース ノート

このリリースの詳細については、[リリース ノート](release-notes-for-oledb-driver-for-sql-server.md)をご覧ください。

## <a name="previous-releases"></a>以前のリリース

[Microsoft OLE DB Driver for SQL Server の以前のリリース](release-notes-for-oledb-driver-for-sql-server.md#previous-releases)

## <a name="see-also"></a>関連項目

[Microsoft OLE DB Driver for SQL Server のリリース ノートです](release-notes-for-oledb-driver-for-sql-server.md)  
[OLE DB Driver for SQL Server のシステム要件](system-requirements-for-oledb-driver-for-sql-server.md)  
[OLE DB Driver for SQL Server のサポート ポリシー](applications\support-policies-for-oledb-driver-for-sql-server.md)  
[OLE DB Driver for SQL Server をいつ使用するか](when-to-use-oledb-driver-for-sql-server.md)  
[OLE DB Driver for SQL Server のインストール](applications/installing-oledb-driver-for-sql-server.md)