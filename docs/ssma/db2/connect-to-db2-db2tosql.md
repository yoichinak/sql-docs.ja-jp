---
description: DB2 への接続 (DB2ToSQL)
title: DB2 への接続 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9d485fd0-ab5d-402a-a59a-e9982a61b7de
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 24ffef4775339baf182b01062f2a06136a04abf1
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100081573"
---
# <a name="connect-to-db2-db2tosql"></a>DB2 への接続 (DB2ToSQL)
[ **Db2 への接続** ] ダイアログボックスを使用して、移行する db2 データベースに接続します。  
  
このダイアログボックスにアクセスするには、[ **ファイル** ] メニューの [ **DB2 への接続**] を選択します。 以前に接続している場合は、コマンドが **DB2 に再接続** されます。  
  
## <a name="options"></a>オプション  
**プロバイダー**  
DB2 データベースへの接続に使用するデータアクセスプロバイダーを選択します。 使用可能なプロバイダーは、DB2 クライアントプロバイダーと OLE DB プロバイダーです。 既定値は DB2 クライアントプロバイダーです。  
  
**モード**  
[標準]、[TNSNAME]、[接続文字列モード] のいずれかを選択します。  
  
-   標準モードでは、プロバイダー、サーバー名、サーバーポート、DB2 SID、ユーザー名、およびパスワードの値を入力または選択します。  
  
-   TNSNAME モードでは、DB2 データベース、ユーザー名、およびパスワードの接続識別子 (TNS alias) を入力します。  
  
-   接続文字列モードでは、接続文字列を指定します。  
  
    > [!IMPORTANT]  
    > 接続文字列モードを使用することはお勧めしません。これは、テキストにパスワードが含まれる可能性があり、クリアテキストとして送信されるためです。  
  
既定値は [標準モードです。  
  
**サーバー名**  
DB2 サーバー名を入力します。 既定のサーバー名は、コンピューター名と同じです。 これは標準モードオプションです。  
  
**[サーバー ポート]**  
DB2 への接続に 1521 (既定値) 以外のポート番号を使用している場合は、ポート番号を入力します。 これは標準モードオプションです。  
  
**接続識別子**  
DB2 connect 識別子を入力します。 これは、ローカル tnsnames. ora ファイルで定義されているデータベースの別名です。  
  
これは TNSNAME モードオプションです。  
  
**DB2 SID**  
データベースの SID を入力します。 SID は、コンピューター上の DB2 データベースを区別するための識別子です。 データベースの既定の SID は、データベース名の最初の8文字です。  
  
これは標準モードオプションです。  
  
**ユーザー名**  
SSMA が DB2 データベースへの接続に使用するユーザー名を入力します。  
  
**パスワード**  
ユーザー名に対応するパスワードを入力します。  
  
**接続文字列**  
> [!IMPORTANT]  
> 接続文字列モードを使用することはお勧めしません。これは、テキストにパスワードが含まれる可能性があり、クリアテキストとして送信されるためです。  
  
接続文字列モードを使用する場合は、DB2 に接続するための完全な接続文字列を入力します。  
  
接続文字列は、パラメーターの名前と値のペアで構成されます。  
  
-   OLE DB の接続文字列情報については、MSDN ライブラリの「 [Microsoft OLE DB Provider for DB2](../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) 」を参照してください。  
  
SSMA 接続文字列の場合は、常に Provider パラメーターを含めます。 また、DB2 に接続するときは、必ず Port パラメーターを指定してください。  
