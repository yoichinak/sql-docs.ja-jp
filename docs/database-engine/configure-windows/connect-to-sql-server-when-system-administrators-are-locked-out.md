---
title: システム管理者がロックアウトされた場合の SQL Server への接続 | Microsoft Docs
description: 誤ってロックアウトされた場合に、システム管理者として SQL Server へのアクセスを回復する方法について説明します。
ms.custom: contperfq4
ms.date: 05/20/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- sa account
- connecting when locked out [SQL Server]
- locked out [SQL Server]
ms.assetid: c0c0082e-b867-480f-a54b-79f2a94ceb67
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 801602c78193f9fc3fa9cdab40b98c3dc3dd42e0
ms.sourcegitcommit: 291ae8f6b72fd355f8f24ce5300339306293ea7e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/18/2020
ms.locfileid: "88512318"
---
# <a name="connect-to-sql-server-when-system-administrators-are-locked-out"></a>システム管理者がロックアウトされた場合の SQL Server への接続 
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
この記事では、システム管理者がロックアウトされた場合に、システム管理者として [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] へのアクセスを回復する方法について説明します。システム管理者は、次のいずれかの理由で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにアクセスできなくなることがあります。  
  
-   sysadmin 固定サーバー ロールのメンバーであるログインがすべて、誤って削除された。  
  
-   sysadmin 固定サーバー ロールのメンバーである Windows グループがすべて、誤って削除された。  
  
-   sysadmin 固定サーバー ロールのメンバーであるログインの使用者が退社したか不在である。  
  
-   sa アカウントが無効になっているか、パスワードが不明である。  
  
## <a name="resolution"></a>解決方法

アクセスの問題を解決するには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスをシングル ユーザー モードで起動することをお勧めします。 このモードでは、アクセスを回復しようとしている間に、他の接続が行われないようにします。 ここでは、SQL Server のインスタンスに接続し、**sysadmin** サーバー ロールにログインを追加できます。 この解決策に関する詳細な手順については、「[ステップ バイ ステップの手順](#step-by-step-instructions)」セクションを参照してください。


コマンド ラインから `-m` または `-f` オプションを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスをシングル ユーザー モードで起動できます。 これにより、コンピューターのローカル Administrators グループのメンバーがすべて、固定サーバー ロール **sysadmin** のメンバーとして [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続できるようになります。  

シングル ユーザー モードでインスタンスを起動する場合は、まず [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを停止してください。 そうしないと、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが先に接続し、サーバーへの使用可能な接続のみを取得して、ログインをブロックする可能性があります。

また、ログインできるようになる前に、不明なクライアント アプリケーションが使用可能な接続のみを取得してしまう場合もあります。 このような状況が発生しないようにするには、`-m` オプションの後にアプリケーション名を指定することで、指定したアプリケーションからの単一の接続に限定することができます。 たとえば、`-mSQLCMD` を指定して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を開始すると、**sqlcmd** クライアント プログラムとして識別される単一の接続に限定されます。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] のクエリ エディターを使用して接続するには、`-m"Microsoft SQL Server Management Studio - Query"` を使用します。  


> [!IMPORTANT]  
> セキュリティ機能として `-m` をアプリケーション名と一緒に使用しないでください。 クライアント アプリケーションは、接続文字列の設定を使用してアプリケーション名を指定するため、偽名を使って簡単になりすますことができます。

次の表は、コマンド ラインでインスタンスをシングル ユーザー モードで起動するさまざまな方法をまとめたものです。

| オプション | 説明 | 使用する場合 |
|:---|:---|:---|
|`-m` | 単一の接続に限定します | 他のユーザーがインスタンスに接続しようとしていない場合、またはインスタンスへの接続に使用しているアプリケーション名がわからない場合。 |
|`-mSQLCMD`| **sqlcmd** クライアント プログラムとして識別される必要がある単一の接続に限定します| **sqlcmd** でインスタンスに接続しようとしているときに、他のアプリケーションが使用可能な接続を取得できないようにする場合。 |
|`-m"Microsoft SQL Server Management Studio - Query"`| **Microsoft SQL Server Management Studio クエリ** アプリケーションとして識別される必要がある単一の接続に限定します。| [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] のクエリ エディターでインスタンスに接続しようとしているときに、他のアプリケーションが使用可能な接続のみを取得できないようにする場合。 |
|`-f`| 単一の接続に限定し、インスタンスを最小構成で開始します | 他の構成によって開始が妨げられている場合。 |
| &nbsp; | &nbsp; | &nbsp; |
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をシングル ユーザー モードで起動する詳細な手順については、「[シングル ユーザー モードでの SQL Server の起動](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)」を参照してください。

## <a name="step-by-step-instructions"></a>ステップ バイ ステップの手順

以下の手順では、誤ってアクセスできなくなってしまった SQL Server ログインにシステム管理者権限を付与する方法について説明します。

以下の手順では、次のことを想定しています。

* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]は Windows 8 以上で実行されている。 それ以前のバージョンの SQL Server または Windows の場合、必要に応じて調整する必要があります。

* [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] がコンピューターにインストールされている。  

ローカル Administrators グループのメンバーとして Windows にログインしているときに、以下の手順を実行します。

1.  Windows の [スタート] メニューから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager のアイコンを右クリックし、 **[管理者として実行]** を選択して、管理者の資格情報を Configuration Manager に渡します。  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーの左ペインで、 **[SQL Server のサービス]** を選択します。 右ペインで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスを探します ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のインスタンスには、コンピューター名の後に **(MSSQLSERVER)** が付いています。 名前付きインスタンスは、[登録済みサーバー] に表示されているものと同じ名前が大文字表記で表示されます)。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[起動時のパラメーター]** タブの **[起動時のパラメーターの指定]** ボックスに、「`-m`」と入力し、 **[追加]** をクリックします (入力文字はダッシュの後に小文字の m です)。  
  
    > [!NOTE]  
    >  以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **[起動時のパラメーター]** タブがない場合があります。その場合は、 **[詳細設定]** タブで、 **[起動時のパラメーター]** をダブルクリックします。 パラメーターが小さいウィンドウに表示されます。 既存のパラメーターは、いずれも変更しないように注意してください。 最後に、新しいパラメーター `;-m` を追加し、 **[OK]** をクリックします (入力文字はセミコロンの後に小文字の m です)。  
  
4.  **[OK]** をクリックし、再起動するためのメッセージが表示されたら、サーバー名を右クリックし、 **[再起動]** をクリックします。  
  
5.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再起動すると、サーバーはシングル ユーザー モードになります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行されていないことを確認します。 起動した場合、それが唯一の接続となります。  
  
6.  Windows の [スタート] メニューから、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を右クリックして、 **[管理者として実行]** を選択します。 これにより、管理者資格情報が SSMS に渡されます。
  
    > [!NOTE]  
    >  以前のバージョンの Windows では、 **[管理者として実行]** オプションはサブメニューとして表示されます。  
  
     構成によっては、SSMS が複数の接続の確立を試みます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はシングル ユーザー モードなので、複数の接続は失敗します。 実際のシナリオに基づいて、次のいずれかのアクションを実行します。  
  
    1.  Windows 認証 (管理者の資格情報を含む) を使用してオブジェクト エクスプローラーと接続します。 **[セキュリティ]** 、 **[ログイン]** の順に展開し、自身のログインをダブルクリックします。 **[サーバー ロール]** ページで、 **[sysadmin]** を選択し、 **[OK]** をクリックします。  
  
    2.  オブジェクト エクスプローラーではなく、Windows 認証 (管理者の資格情報を含む) を使用してクエリ ウィンドウと接続します (この方法で接続できるのは、オブジェクト エクスプローラーと接続していない場合のみです)。**sysadmin** 固定サーバー ロールのメンバーである新しい Windows 認証ログインを追加するには、次のようなコードを実行します。 次の例では、`CONTOSO\PatK` という名前のドメイン ユーザーを追加します。  
  
        ```  
        CREATE LOGIN [CONTOSO\PatK] FROM WINDOWS;  
        ALTER SERVER ROLE sysadmin ADD MEMBER [CONTOSO\PatK];  
        ```  
  
    3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を混合認証モードで実行している場合、Windows 認証 (管理者の資格情報を含む) を使用してクエリ ウィンドウと接続します。 **sysadmin** 固定サーバー ロールのメンバーである新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証ログインを作成するには、次のようなコードを実行します。  
  
        ```  
        CREATE LOGIN TempLogin WITH PASSWORD = '************';  
        ALTER SERVER ROLE sysadmin ADD MEMBER TempLogin;  
        ```  
  
        > [!WARNING]  
        >  ************ は強力なパスワードと置き換えてください。  
  
    4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を混合認証モードで実行していて、 **sa** アカウントのパスワードをリセットする場合、Windows 認証 (管理者の資格情報を含む) を使用してクエリ ウィンドウと接続します。 次の構文を使用して、 **sa** アカウントのパスワードを変更します。  
  
        ```  
        ALTER LOGIN sa WITH PASSWORD = '************';  
        ```  
  
        > [!WARNING]  
        >  ************ は強力なパスワードと置き換えてください。  

7. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]を終了します。  
  
8. 以降のいくつかの手順では、SQL Server をマルチ ユーザー モードに戻します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーの左ペインで、 **[SQL Server のサービス]** を選択します。

9. 右ペインで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスを右クリックし、 **[プロパティ]** をクリックします。  
  
10. **[起動時のパラメーター]** タブの **[既存のパラメーター]** ボックスで、[ `-m` ] を選択し、 **[削除]** をクリックします。  
  
    > [!NOTE]  
    >  以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **[起動時のパラメーター]** タブがない場合があります。その場合は、 **[詳細設定]** タブで、 **[起動時のパラメーター]** をダブルクリックします。 パラメーターが小さいウィンドウに表示されます。 前の手順で追加した `;-m` を削除し、 **[OK]** をクリックします。  
  
11. サーバー名を右クリックし、 **[再起動]** をクリックします。 シングル ユーザー モードで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を開始する前に、エージェントを停止している場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを再起動してください。
  
これで、 **sysadmin** 固定サーバー ロールのメンバーであるアカウントの 1 つを使用して正常に接続できます。  
  
## <a name="see-also"></a>参照  

* [サーバー スタートアップ オプションの構成](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md)
* [データベース エンジン サービスのスタートアップ オプション](../../database-engine/configure-windows/database-engine-service-startup-options.md)  
