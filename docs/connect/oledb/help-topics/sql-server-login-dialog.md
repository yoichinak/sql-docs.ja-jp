---
title: '[SQL Server ログイン] ダイアログ ボックス (OLE DB) | Microsoft Docs'
description: 十分な情報を指定せずに接続しようとすると、OLE DB Driver for SQL Server によって [SQL Server ログイン] ダイアログ ボックスが表示され、入力が求められます。
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: 403c134c6e627ba1eb6c18cd2ba5341e54d65975
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727257"
---
# <a name="sql-server-login-dialog-box"></a>[SQL Server ログイン] ダイアログ ボックス
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

十分な情報を指定せずに接続しようとすると、OLE DB ドライバーによって **[SQL Server ログイン]** ダイアログ ボックスが表示されます。

> [!NOTE]  
> [SQL Server ログイン] ダイアログのプロンプト動作は、`DBPROP_INIT_PROMPT` 初期化プロパティによって制御されます。 詳細については、次を参照してください。
> - [初期化プロパティと承認プロパティ](../ole-db-data-source-objects/initialization-and-authorization-properties.md)
> - [OLE DB プログラマー ガイド](/previous-versions/windows/desktop/ms714342(v=vs.85))

![[SQL Server ログイン] ダイアログ ボックスのスクリーンショット](../media/sql-server-login-dialog.png)

## <a name="options"></a>オプション
|オプション|説明|
|---   |---        |
|サーバー|ネットワーク上の SQL Server のインスタンスの名前です。 一覧から server\instance 形式の名前を選択するか、 **[サーバー]** ボックスに server\instance 形式の名前を入力します。 必要に応じて、**SQL Server 構成マネージャー**を使用してクライアント コンピューターでサーバーの別名を作成し、 **[サーバー]** ボックスにその名前を入力することができます。 <br/><br/>SQL Server と同じコンピューターを使用している場合は、「(local)」と入力することができます。 その後、ネットワークに接続されていない SQL Server を実行している場合でも、SQL Server のローカル インスタンスに接続することができます。<br/><br/>さまざまな種類のネットワークに対応するサーバー名の詳細については、[SQL Server のインストール](../../../database-engine/install-windows/install-sql-server.md)に関するページを参照してください。|
|認証モード|ドロップダウン リストから、次の認証オプションを選択できます。<br/><ul><li>`Windows Authentication:` 現在ログインしているユーザーの Windows アカウントの資格情報を使用した SQL Server に対する認証。</li><li>`SQL Server Authentication:` ログイン ID とパスワードを使用した認証。</li><li>`Active Directory - Integrated:` Azure Active Directory の ID による統合認証。 このモードは、SQL Server に対する Windows 認証でも使用できます。</li><li>`Active Directory - Password:` Azure Active Directory の ID によるユーザー ID とパスワードの認証。</li><li>`Active Directory - Universal with MFA support:` Azure Active Directory の ID による対話型認証。 このモードでは、Azure Multi-Factor Authentication (MFA) がサポートされます。</li></ul>|
|サーバー SPN|セキュリティ接続を使用する場合、サーバーのサービス プリンシパル名 (SPN) を指定できます。|
|Login ID|接続に使用するログイン ID を指定します。 [ログイン ID] テキスト ボックスは、`Authentication Mode` が `SQL Server Authentication`、`Active Directory - Password`、または `Active Directory - Universal with MFA support` に設定されている場合にのみ有効になります。|
|Password|接続に使用するパスワードを指定します。 [パスワード] テキスト ボックスは、`Authentication Mode` が `SQL Server Authentication` または `Active Directory - Password` に設定されている場合にのみ有効になります。|
|オプション|**[オプション]** グループを表示または非表示にします。 **[オプション]** ボタンは、 **[サーバー]** に値が設定されている場合に有効になります。|
|パスワードの変更|オンにすると、 **[新しいパスワード]** と **[新しいパスワードの確認入力]** テキスト ボックスが有効になります。|
|新しいパスワード|新しいパスワードを指定します。|
|[新しいパスワードの確認入力]|確認のために、新しいパスワードをもう一度指定します。|
|データベース|接続で使用する既定のデータベースを選択または入力します。 この設定は、サーバーのログインに指定されている既定のデータベースをオーバーライドします。 データベースが指定されていない場合、接続はサーバーのログインに指定されている既定のデータベースを使用します。|
|[ミラー サーバー]|ミラー化するデータベースのフェールオーバー パートナーの名前を指定します。|
|[ミラー SPN]|必要に応じて、ミラー サーバーに SPN を指定できます。 ミラー サーバーの SPN は、クライアントとサーバー間の相互認証に使用されます。|
|言語|SQL Server システム メッセージに使用する言語を指定します。 SQL Server を実行しているコンピューターには言語がインストールされている必要があります。 この設定は、サーバーのログインに指定されている既定の言語をオーバーライドします。 言語が指定されていない場合、接続はサーバーのログインに指定されている既定の言語を使用します。|
|アプリケーション名|**sys.sysprocesses** 内でこの接続の行の **program_name** 列に格納されるアプリケーション名を指定します。|
|[ワークステーション ID]|**sys.sysprocesses** 内でこの接続の行の **hostname** 列に格納されるワークステーション ID を指定します。|
|[データに強力な暗号を使用する]|オンにすると、接続を介して渡されるデータが暗号化されます。|
|[サーバー証明書を信頼する]|オンにすると、サーバーの証明書が検証されます。 サーバーの証明書は、サーバーの正しいホスト名を含み、信頼された証明機関によって発行されている必要があります。|

> [!NOTE]  
> `Windows Authentication` または `SQL Server Authentication` モードを使用する場合、 **[サーバー証明書を信頼する]** は、 **[データに強力な暗号を使用する]** オプションが有効な場合にのみ考慮対象になります。

## <a name="next-steps"></a>次のステップ
- OLE DB ドライバーを使用して [Azure Active Directory に対する認証を行います](../features/using-azure-active-directory.md)。
- [ユニバーサル データ リンク (UDL)](data-link-pages.md) を使用して接続情報を設定します。