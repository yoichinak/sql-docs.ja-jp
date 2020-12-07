---
title: サーバーの認証モードの変更
description: SQL Server でサーバーの認証モードを変更する方法について説明します。 このタスクには、SQL Server Management Studio か Transact-SQL のどちらかを使用できます。
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- sa account
- authentication [SQL Server], changing modes
- server authentication mode [SQL Server]
- modifying server authentication mode
ms.assetid: 79babcf8-19fd-4495-b8eb-453dc575cac0
author: markingmyname
ms.author: maghan
ms.custom: ''
ms.date: 02/18/2020
ms.openlocfilehash: 79dc463039be1100f265e6bb44561a6e2dc71c93
ms.sourcegitcommit: bf5acef60627f77883249bcec4c502b0205300a4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2020
ms.locfileid: "88200953"
---
# <a name="change-server-authentication-mode"></a>サーバーの認証モードの変更

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、サーバーの認証モードを変更する方法について説明します。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] はインストール中に、 **[Windows 認証モード]** または **[SQL Server 認証モードと Windows 認証モード]** のいずれかに設定されます。 インストール後は、認証モードをいつでも変更できます。

インストール中に **[Windows 認証モード]** を選択した場合、sa ログインは無効となり、パスワードはセットアップによって割り当てられます。 後で認証モードを **[SQL Server 認証モードと Windows 認証モード]** に変更しても、sa ログインは無効のままです。 sa ログインを使用するには、ALTER LOGIN ステートメントを使用して、sa ログインを有効にし、新しいパスワードを割り当ててください。 sa ログインは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用しないとサーバーに接続できません。

## <a name="before-you-begin"></a>開始する前に

sa アカウントは、よく知られた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントで、悪意のあるユーザーの攻撃対象となることが少なくありません。 sa アカウントは、アプリケーションで必要とならない限り、有効にしないでください。 sa ログインには、複雑なパスワードを使用することが重要です。

## <a name="change-authentication-mode-with-ssms"></a>SSMS を使用した認証モードを変更する

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] オブジェクト エクスプローラーで、サーバーを右クリックし、 **[プロパティ]** をクリックします。

2. **[セキュリティ]** ページの **[サーバー認証]** で、新しいサーバーの認証モードを選択し、 **[OK]** をクリックします。

3. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の再起動が必要であることを示す **のダイアログ ボックスで、** [OK] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をクリックします。

4. オブジェクト エクスプローラーでサーバーを右クリックし、 **[再起動]** をクリックします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントも再起動する必要があります (実行されている場合)。

## <a name="enable-sa-login"></a>sa ログインを有効にする

SSMS または T-SQL を使用して **sa** ログインを有効にすることができます。

### <a name="use-ssms"></a>SSMS を使用する

1. オブジェクト エクスプローラーで、 **[セキュリティ]** 、[ログイン] の順に展開し、 **[sa]** を右クリックして **[プロパティ]** をクリックします。

2. **[全般]** ページで、**sa** ログイン用のパスワードの作成と確認が必要になる場合があります。

3. **[状態]** ページで、 **[ログイン]** の **[有効]** をクリックし、 **[OK]** をクリックします。

### <a name="using-transact-sql"></a>Transact-SQL の使用

次の例では、sa ログインを有効にし、新しいパスワードを設定します。 `<enterStrongPasswordHere>` を強力なパスワードに置き換えてから、実行してください。

```sql  
ALTER LOGIN sa ENABLE ;  
GO  
ALTER LOGIN sa WITH PASSWORD = '<enterStrongPasswordHere>' ;  
GO  
```

## <a name="change-authentication-mode-t-sql"></a>認証モードの変更 (T-SQL)

次の例では、サーバー認証を混合モード (Windows + SQL) から Windows のみに変更します。

> [!CAUTION]
> 次の例では、拡張ストアド プロシージャを使用して、サーバー レジストリを変更します。 レジストリの変更の方法を誤った場合、深刻な問題が発生することがあります。 これらの問題が起きた場合、オペレーティング システムを再インストールしなければならない場合があります。 Microsoft は、これらの問題を解決できることを保証できません。 レジストリを変更する場合は、ご自分の責任で行ってください。

```sql
USE [master]
GO
EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE', 
     N'Software\Microsoft\MSSQLServer\MSSQLServer',
     N'LoginMode', REG_DWORD, 1
GO
```

> [!Note]
> 認証モードを変更するために必要なアクセス許可は、[sysadmin](../../relational-databases/security/authentication-access/server-level-roles.md#fixed-server-level-roles) または [Control Server](../../relational-databases/security/permissions-database-engine.md) です

## <a name="see-also"></a>関連項目

- [強力なパスワード](../../relational-databases/security/strong-passwords.md)
- [SQL Server インストールにおけるセキュリティの考慮事項](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)
- [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)
- [システム管理者がロックアウトされた場合の SQL Server への接続](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)
