---
description: MSSQLSERVER_18483
title: MSSQLSERVER_18483
ms.custom: ''
ms.date: 12/25/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 18483 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 9ec3453277430ba71b9764ad69861f157c153699
ms.sourcegitcommit: d8cdbb719916805037a9167ac4e964abb89c3909
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/20/2021
ms.locfileid: "98596276"
---
# <a name="mssqlserver_18483"></a>MSSQLSERVER_18483
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細

|属性|値|
|---|---|
|製品名|SQL Server|
|イベント ID|18483|
|イベント ソース|MSSQLSERVER|
|コンポーネント|SQLEngine|
|シンボル名|REMLOGIN_INVALID_USER|
|メッセージ テキスト|サーバー '%.ls' に接続できませんでした。'%. ls' はそのサーバーでリモート ログインとして定義されていません。 正しいログイン名を指定していることを確認してください。 %.*ls。|
||

## <a name="explanation"></a>説明

このエラーは、SQL インスタンスが最初にインストールされた別のコンピューターのハード ディスク イメージを使用して復元されたシステムで、レプリケーション ディストリビューターを構成しようとしたときに発生します。 次のようなエラー メッセージがユーザーに報告されます。

> SQL Server Management Studio で、'\<Server>\<Instance>' を '\<Server>\<Instance>' のディストリビューターとして構成できませんでした。 エラー 18483:'distributor_admin' がサーバーでリモート ログインとして定義されていないので、サーバー '\<Server>\<Instance>' に接続できませんでした。 正しいログイン名を指定していることを確認してください。 %.*ls。

## <a name="cause"></a>原因

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がインストールされている別のコンピューターのハード ディスク イメージから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を展開すると、イメージが作成されたコンピューターのネットワーク名は新しいインストールに保持されます。 ネットワーク名が正しくないと、レプリケーション ディストリビューターの構成に失敗します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール後にコンピューターの名前を変更した場合、同じ問題が発生します。

## <a name="user-action"></a>ユーザー アクション

この問題を回避するには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サーバー名をコンピューターの正しいネットワーク名に置き換えます。 これを行うには、次のステップに従います。

1. ディスク イメージから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を展開したコンピューターにログオンし、SSMS で次の Transact-SQL ステートメントを実行します。

    ```sql
    -- Use the Master database
    USE master
    GO

    -- Declare local variables
    DECLARE @serverproperty_servername varchar(100),
    @servername varchar(100);

    -- Get the value returned by the SERVERPROPERTY system function
    SELECT @serverproperty_servername = CONVERT(varchar(100), SERVERPROPERTY('ServerName'));

    -- Get the value returned by @@SERVERNAME global variable
    SELECT @servername = CONVERT(varchar(100), @@SERVERNAME);

    -- Drop the server with incorrect name
    EXEC sp_dropserver @server=@servername;

    -- Add the correct server as a local server
    EXEC sp_addserver @server=@serverproperty_servername, @local='local';
    ```

2. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているコンピューターを再起動します。
3. コンピューターの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名とネットワーク名が同じであることを確認するには、次の Transact-SQL ステートメントを実行します。

    ```sql
    SELECT @@SERVERNAME, SERVERPROPERTY('ServerName');
    ```

## <a name="more-information"></a>説明

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で `@@SERVERNAME` グローバル変数または `SERVERPROPERTY`(' ServerName ') 関数を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が実行されているコンピューターのネットワーク名を見つけることができます。 `SERVERPROPERTY` 関数の ServerName プロパティによって、コンピューターと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを再起動したときに、コンピューターのネットワーク名の変更が自動的に報告されます。 `@@SERVERNAME` グローバル変数には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名が手動でリセットされるまで、元の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンピューター名が保持されます。

### <a name="steps-to-reproduce-the-problem"></a>問題を再現する手順

ディスク イメージから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を展開したコンピューターで、次の手順を実行します。

1. [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)]を起動します。
2. **オブジェクト エクスプローラー** で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス名を展開します。
3. **レプリケーション** フォルダーを右クリックし、 **[Configure distribution Replication]\(ディストリビューション レプリケーションの構成\)** をクリックしてから、 **[Configure Publishing, Subscribers, and Distribution]\(パブリッシング、サブスクライバー、およびディストリビューションの構成\)** をクリックします。
4. **[ディストリビューションの構成ウィザード]** ダイアログ ボックスで、 **[次へ]** をクリックします。
5. **[ディストリビューター]** ダイアログ ボックスで、'\<**Server**>\<**Instance**>' をクリックして選択すると、それが独自のディストリビューターとして機能し、SQL Server によってディストリビューション データベースとログ ラジオ ボタンが作成されます。その後、 **[次へ]** をクリックします。
6. **[SQL Server エージェントの起動]** ダイアログ ボックスで、 **[次へ]** をクリックします。
7. **[スナップショット フォルダー]** ダイアログ ボックスで、 **[次へ]** をクリックします。

    > [!NOTE]
    > スナップショット フォルダーのパスを確認するメッセージが表示された場合は、 **[はい]** をクリックします。
8. **[ディストリビューション データべース]** ダイアログ ボックスで、 **[次へ]** をクリックします。
9. **[パブリッシャー]** ダイアログ ボックスで、 **[次へ]** をクリックします。
10. **[ウィザードのアクション]** ダイアログ ボックスで、 **[次へ]** をクリックします。
11. **[ウィザードの完了]** ダイアログ ボックスで、 **[完了]** をクリックします。

## <a name="see-also"></a>関連項目

- [SQL Server のスタンドアロン インスタンスをホストするコンピューターの名前変更](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)
- [@@SERVERNAME (Transact-SQL)](../../t-sql/functions/servername-transact-sql.md)
- [SERVERPROPERTY (Transact-SQL)](../../t-sql/functions/serverproperty-transact-sql.md)
- [sp_addserver (Transact-SQL)](../system-stored-procedures/sp-addserver-transact-sql.md)