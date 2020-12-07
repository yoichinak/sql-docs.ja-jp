---
title: '[SQL Server ログイン] ダイアログ ボックス (ODBC)'
description: データベースに接続するための情報を寿分に指定せずにアプリケーションで ODBC 接続が行われると、SQL Server ログイン ダイアログが表示されることがあります。
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: David-Engel
ms.author: v-jizho2
ms.openlocfilehash: 7c0a2be5961e4fab07941d999da1a2b2fe5f9dbe
ms.sourcegitcommit: a4ee6957708089f7d0dda15668804e325b8a240c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87898808"
---
# <a name="sql-server-login-dialog-box-odbc"></a>[SQL Server ログイン] ダイアログ ボックス (ODBC)

ドライバーが SQL Server に接続するのに十分な情報を指定せずに ODBC 接続を呼び出すと、ODBC ドライバーにより、 **[SQL Server ログイン]** ダイアログ ボックスが表示されます。

## <a name="options"></a>Options

### <a name="server"></a>サーバー

ネットワーク上の SQL Server のインスタンスの名前です。 一覧から server\instance 形式の名前を選択するか、 **[サーバー]** ボックスに server\instance 形式の名前を入力します。 必要に応じて、**SQL Server 構成マネージャー**を使用してクライアント コンピューターでサーバーの別名を作成し、 **[サーバー]** ボックスにその名前を入力することができます。

SQL Server と同じコンピューターを使用している場合は、「(local)」と入力することができます。 その後、ネットワークに接続されていない SQL Server を実行している場合でも、SQL Server のローカル インスタンスに接続することができます。

さまざまな種類のネットワークに対応するサーバー名の詳細については、SQL Server オンライン ブックにある SQL Server のインストールに関するドキュメントを参照してください。

### <a name="authentication-mode"></a>認証モード

次のいずれかの認証モードを選択します。
- ログイン ID とパスワードを使用した **SQL Server**
- 現在ログインしているユーザーのアカウントを使用した **Windows 統合**認証
- ログイン ID とパスワードを使用した **Active Directory パスワード**
- 現在ログインしているユーザーのアカウントを使用した **Active Directory 統合**認証
- ログイン ID を使用した **Active Directory 対話型**認証
- マネージド ID による**マネージド サービス ID** 認証

認証モードの詳細については、「[データ ソース ウィザード画面 2](../../../connect/odbc/windows/dsn-wizard-2.md)」を参照してください。

### <a name="server-spn"></a>サーバー SPN

セキュリティ接続を使用する場合、サーバーのサービス プリンシパル名 (SPN) を指定できます。

### <a name="login-id"></a>Login ID

**[認証モード]** が **[SQL Server]** 、 **[Active Directory パスワード]** 、 **[Active Directory 対話型]** 、 **[マネージド サービス ID]** に設定されている場合は、接続に使用する SQL Server または Azure Active Directory のログイン ID を指定します。 それ以外の場合、 **[ログイン ID]** ボックスは無効になります。

### <a name="password"></a>Password

**[認証モード]** が **[SQL Server]** または **[Active Directory パスワード]** に設定されている場合は、接続に使用する SQL Server または Azure Active Directory のログイン ID のパスワードを指定します。 それ以外の場合、 **[パスワード]** ボックスは無効になります。

### <a name="options"></a>Options

**[オプション]** グループを表示または非表示にします。 **[オプション]** ボタンは、 **[サーバー]** に値が設定されている場合に有効になります。

### <a name="change-password"></a>パスワードの変更

このチェック ボックスをオンにすると、 **[新しいパスワード]** ボックスと **[新しいパスワードの確認入力]** ボックスが表示されます。

### <a name="new-password"></a>新しいパスワード

新しいパスワードを指定します。

### <a name="confirm-new-password"></a>[新しいパスワードの確認入力]

確認のために、新しいパスワードをもう一度指定します。

### <a name="database"></a>データベース

接続で使用する既定のデータベースを指定します。 この設定は、サーバーのログインに指定されている既定のデータベースをオーバーライドします。 データベースが指定されていない場合、接続はサーバーのログインに指定されている既定のデータベースを使用します。

### <a name="mirror-server"></a>[ミラー サーバー]

ミラー化するデータベースのフェールオーバー パートナーの名前を指定します。

### <a name="mirror-spn"></a>[ミラー SPN]

必要に応じて、ミラー サーバーに SPN を指定できます。 ミラー サーバーの SPN は、クライアントとサーバー間の相互認証に使用されます。

### <a name="language"></a>Language

SQL Server システム メッセージに使用する言語を指定します。 SQL Server を実行しているコンピューターには言語がインストールされている必要があります。 この設定は、サーバーのログインに指定されている既定の言語をオーバーライドします。 言語が指定されていない場合、接続はサーバーのログインに指定されている既定の言語を使用します。

### <a name="application-name"></a>アプリケーション名

(省略可) **sys.sysprocesses** でこの接続の行の **program_name** 列にアプリケーション名が格納されるように指定します。

### <a name="workstation-id"></a>[ワークステーション ID]

(省略可) **sys.sysprocesses** でこの接続の行の **hostname** 列にワークステーション ID が格納されるように指定します。

### <a name="use-strong-encryption-for-data"></a>[データに強力な暗号を使用する]

オンにすると、接続を介して渡されたデータが暗号化されます。 このチェック ボックスがオフの場合でも、既定では、ログインが暗号化されます。

### <a name="trust-server-certificate"></a>[サーバー証明書を信頼する]

このオプションは、 **[データに強力な暗号化を使用する]** が有効になっている場合にのみ適用されます。 このオプションを選択すると、サーバーの証明書は、サーバーの正しいホスト名を持ち、信頼された証明機関によって発行されたことを検証されません。

## <a name="see-also"></a>参照

[Microsoft ODBC Driver for SQL Server on Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
