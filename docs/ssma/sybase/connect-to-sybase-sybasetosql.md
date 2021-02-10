---
title: Sybase への接続 (SybaseToSQL) |Microsoft Docs
description: SSMA for Sybase (SAP ASE) を使用して移行を開始するには、SAP ASE インスタンスに接続します。 [Sybase への接続] ダイアログボックスを使用します。
author: nahk-ivanov
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 524f95ef-10bd-497c-84ca-c06a0ae794fb
ms.author: alexiva
ms.openlocfilehash: 8d43e6a48746fbb1587327b430b67c6959731013
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100064097"
---
# <a name="connect-to-sybase-sybasetosql"></a>Sybase への接続 (SybaseToSQL)

[ **Sybase への接続** ] ダイアログボックスを使用して、移行する Sybase Adaptive Server ENTERPRISE (ASE) インスタンスに接続します。

このダイアログボックスにアクセスするには、[ **ファイル** ] メニューの [ **Sybase に接続**] を選択します。 以前に接続している場合は、コマンドが **Sybase に再接続** されます。

## <a name="options"></a>オプション

**プロバイダー**  
Sybase サーバーに接続するコンピューター上のインストールされている任意のプロバイダーを選択します。

**モード**  
[標準] または [高度な接続モード] を選択します。 標準モードでは、サーバー名、ポート、ユーザー名、およびパスワードの値を入力または選択します。 詳細設定モードでは、接続文字列を指定します。

**サーバー名**  
アダプティブサーバーの名前または IP アドレスを入力または選択します。 既定のサーバー名は、コンピューター名と同じです。 これは標準モードオプションです。

**[サーバー ポート]**  
ASE への接続に既定以外のポートを使用している場合は、ポート番号を入力します。 既定のポート番号は5000です。 これは標準モードオプションです。
  
**ユーザー名**  
ASE への接続に使用するユーザー名を入力します。 これは標準モードオプションです。

**パスワード**  
ユーザー名に対応するパスワードを入力します。 これは標準モードオプションです。

**接続文字列**  
ASE への接続に使用する完全な接続文字列を入力します。

接続文字列は、パラメーターの名前と値のペアで構成されます。 パラメーターの名前は、使用されているプロバイダーによって異なります。

**さまざまなプロバイダーの接続パラメーターは次のとおりです。**

1. **OLE DB プロバイダー** の接続パラメーター

   |設定|Sybase 12.5 パラメーター|Sybase 15 パラメーター|
   |-----------|-------------------------|-----------------------|
   |サーバー名|サーバー名|サーバー|
   |Port|サーバーポートアドレス|Port|
   |ユーザー名|ユーザー ID|ユーザー ID|
   |Password|Password|Password|
   |プロバイダー|プロバイダー|プロバイダー|

   Sybase ASE 12.5 の場合、接続文字列の例は次のようになります。

   `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`

   Sybase ASE 15 の場合、接続文字列の例は次のようになります。

   `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=ASEOLEDB;Port=5000;`

2. **ODBC プロバイダー** の接続パラメーター

   |設定|Sybase 12.5/15 パラメーター|
   |-----------|-----------------------------|
   |ドライバ名|ドライバー|
   |サーバー名|サーバー|
   |[ユーザー名]|Uid|
   |Password|Pwd|
   |ポート番号|Port|

   Sybase ASE 12.5 または15の場合、接続文字列の例は次のようになります。

   `driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`

3. **ADO.NET Provider** の接続パラメーター

   |設定|Sybase 12.5/15 パラメーター|
   |-----------|-----------------------------|
   |サーバー名|サーバー|
   |[ユーザー名]|Uid|
   |Password|Pwd|
   |ポート番号|Port|

   ADO.NET Provider の接続文字列の例を次に示します。

   `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`

   詳細については、ASE のドキュメントを参照してください。

   これは高度なモードオプションです。

## <a name="next-steps"></a>次のステップ

移行プロセスの次の手順では、 [SQL Server に接続](connect-to-sql-server-sybasetosql.md)します。
