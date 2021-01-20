---
title: Oracle への接続 (OracleToSQL) |Microsoft Docs
description: SSMA for Oracle を使用して Oracle データベースに接続し、移行を開始する方法について説明します。 [Oracle への接続] ダイアログボックスを使用します。
author: nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 23a48cb6-ff30-49bb-b4a7-603ebcab336f
ms.author: alexiva
ms.openlocfilehash: 8e13b9ea8bcd264d1668cf0979dc2956bd11bef7
ms.sourcegitcommit: d8cdbb719916805037a9167ac4e964abb89c3909
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/20/2021
ms.locfileid: "98596722"
---
# <a name="connect-to-oracle-oracletosql"></a>Oracle への接続 (OracleToSQL)

[ **Oracle への接続** ] ダイアログボックスを使用すると、移行する oracle データベースに接続できます。

このダイアログボックスにアクセスするには、[ **ファイル** ] メニューの [ **Oracle への接続**] をクリックします。 以前に接続している場合は、コマンドが **Oracle に再接続** されます。

## <a name="options"></a>オプション

**プロバイダー**  
Oracle データベースへの接続に使用するデータアクセスプロバイダーを選択します。 使用可能なプロバイダーは、Oracle クライアントプロバイダーと OLE DB プロバイダーです。 既定値は [Oracle Client Provider (Oracle クライアントプロバイダー) です。

**モード**  
[標準]、[TNSNAME]、[接続文字列モード] のいずれかを選択します。

- 標準モードでは、プロバイダー、サーバー名、サーバーポート、Oracle SID、ユーザー名、およびパスワードの値を入力または選択します。
- TNSNAME モードでは、Oracle データベース、ユーザー名、およびパスワードの接続識別子 (TNS alias) を入力します。
- 接続文字列モードでは、接続文字列を指定します。

  > [!IMPORTANT]
  > 接続文字列モードを使用することはお勧めしません。これは、テキストにパスワードが含まれる可能性があり、クリアテキストとして送信されるためです。

既定値は [標準モードです。

**サーバー名**  
Oracle サーバー名を入力します。 既定のサーバー名は、コンピューター名と同じです。 これは標準モードオプションです。

**[サーバー ポート]**  
Oracle への接続に 1521 (既定値) 以外のポート番号を使用している場合は、ポート番号を入力します。 これは標準モードオプションです。

**接続識別子**  
Oracle 接続識別子を入力します。 これは、ローカル tnsnames. ora ファイルで定義されているデータベースの別名です。

これは TNSNAME モードオプションです。

**Oracle SID**  
データベースの SID を入力します。 SID は、コンピューター上の Oracle データベースを区別するための識別子です。 データベースの既定の SID は、データベース名の最初の8文字です。

これは標準モードオプションです。

**ユーザー名**  
SSMA が Oracle データベースへの接続に使用するユーザー名を入力します。

**パスワード**  
ユーザー名に対応するパスワードを入力します。

**接続文字列**  
> [!IMPORTANT]
> 接続文字列モードを使用することはお勧めしません。これは、テキストにパスワードが含まれる可能性があり、クリアテキストとして送信されるためです。

接続文字列モードを使用する場合は、Oracle への接続に使用する完全な接続文字列を入力します。

接続文字列は、パラメーターの名前と値のペアで構成されます。

- OLE DB の接続文字列情報については、MSDN ライブラリの「 [Microsoft OLE DB Provider for Oracle](../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) 」を参照してください。

SSMA 接続文字列の場合は、常に Provider パラメーターを含めます。 また、Oracle に接続するときは、Port パラメーターを必ず含めてください。

## <a name="next-steps"></a>次のステップ

移行プロセスの次の手順では、 [SQL Server に接続](connect-to-sql-server-oracletosql.md)します。