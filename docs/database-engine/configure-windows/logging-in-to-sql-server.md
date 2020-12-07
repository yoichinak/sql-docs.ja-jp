---
title: SQL Server へのログイン | Microsoft Docs
description: SQL Server のインスタンスにサインインするさまざまな方法について説明します。 さまざまな環境でサーバー名にどの形式を使用すべきかについて説明します。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server, logging in
- services [SQL Server], logging in
- TCP connection string
- connecting to the Database Engine
- logins [SQL Server], about logging in
- named pipe connection string
- log ins [SQL Server]
- shared memory connection string
- logging in [SQL Server]
- logins [SQL Server]
ms.assetid: 77158a9a-d638-4818-90a1-cb2eb57df514
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bb0fe13f5a15a726235c306c7b6b3c6b79bcef2c
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2020
ms.locfileid: "91669652"
---
# <a name="logging-in-to-sql-server"></a>SQL Server へのログイン
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  任意のグラフィカルな管理ツール、またはコマンド プロンプトを使用して、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにログインできます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] などのグラフィカルな管理ツールを使用して [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]のインスタンスにログインする場合、必要に応じて、サーバー名、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン、およびパスワードを指定するように求められます。 Windows 認証を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にログインする場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスにアクセスするたびに SQL Server ログインを指定する必要はありません。 代わりに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により自動的に [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントを使用したログインが行われます。 混合モード認証 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証モードと Windows 認証モード) で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用してログインする場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のログインとパスワードを指定する必要があります。 可能な場合は、Windows 認証を使用します。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をインストールしたときに大文字と小文字を区別する照合順序を選択した場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインでも大文字と小文字が区別されます。  
  
## <a name="format-for-specifying-the-name-of-sql-server"></a>SQL Server の名前を指定する形式  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続する場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前を指定する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが既定のインスタンス (名前のないインスタンス) である場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がインストールされているコンピューターの名前または IP アドレスを指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが名前付きインスタンス (SQLEXPRESS など) である場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がインストールされているコンピューターの名前または IP アドレスを指定し、スラッシュとインスタンス名を追加します。  
  
 次の例は、APPHOST という名前のコンピューターで実行されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続します。 名前付きインスタンスを指定する場合は、インスタンス名の SQLEXPRESS を使用します。  
  
 **例:**  
  
|インスタンスの型|サーバー名の入力|  
|----------------------|-------------------------------|  
|既定のプロトコルによる既定のインスタンスへの接続|APPHOST|  
|既定のプロトコルによる名前付きインスタンスへの接続 |APPHOST\SQLEXPRESS|  
|ピリオドを使用して、インスタンスがローカル コンピューター上で実行されていることを示す、同じコンピューター上の既定のインスタンスへの接続。|。|  
|ピリオドを使用して、インスタンスがローカル コンピューター上で実行されていることを示す、同じコンピューター上の名前付きインスタンスへの接続。|.\SQLEXPRESS|  
|localhost を使用して、インスタンスがローカル コンピューター上で実行されていることを示す、同じコンピューター上の既定のインスタンスへの接続。|localhost|  
|localhost を使用して、インスタンスがローカル コンピューター上で実行されていることを示す、同じコンピューター上の名前付きインスタンスへの接続。|localhost\SQLEXPRESS|  
|(local) を使用して、インスタンスがローカル コンピューター上で実行されていることを示す、同じコンピューター上の既定のインスタンスへの接続。|(local)|  
|(local) を使用して、インスタンスがローカル コンピューター上で実行されていることを示す、同じコンピューター上の名前付きインスタンスへの接続。|(local)\SQLEXPRESS|  
|共有メモリ接続を適用している同じコンピューター上の既定のインスタンスへの接続。|lpc:APPHOST|  
|共有メモリ接続を適用している同じコンピューター上の名前付きインスタンスへの接続。|lpc:APPHOST\SQLEXPRESS|  
|IP アドレスを使用した、TCP アドレス 192.168.17.28 をリッスンしている既定のインスタンスへの接続。|192.168.17.28|  
|IP アドレスを使用した、TCP アドレス 192.168.17.28 をリッスンしている名前付きインスタンスへの接続。|192.168.17.28\SQLEXPRESS|  
|使用されているポート (ここでは 2828) の指定による、既定の TCP ポートをリッスンしていない既定のインスタンスへの接続 ([!INCLUDE[ssDE](../../includes/ssde-md.md)] が既定のポート (1433) をリッスンしている場合は、ポート番号を指定する必要はありません)。|APPHOST,2828|  
|指定された TCP ポート (ここでは 2828) 上の名前付きインスタンスへの接続 (ホスト コンピューターで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスが実行されていない場合に、ポート番号の指定が必要になることがよくあります)。|APPHOST,2828|  
|IP アドレスと使用されている TCP ポート (ここでは 2828) の指定による、既定の TCP ポートをリッスンしていない既定のインスタンスへの接続。|192.168.17.28,2828|  
|IP アドレスと使用されている TCP ポート (ここでは 2828) の指定による、名前付きインスタンスへの接続。|192.168.17.28\SQLEXPRESS,2828|  
|TCP 接続を適用する、名前による既定のインスタンスへの接続。|tcp:APPHOST|  
|TCP 接続を適用する、名前による名前付きインスタンスへの接続。|tcp:APPHOST\SQLEXPRESS|  
|名前付きパイプ名の指定による、既定のインスタンスへの接続。|\\\APPHOST\pipe\SQL\query|  
|名前付きパイプ名の指定による、名前付きインスタンスへの接続。|\\\APPHOST\pipe\MSSQL$SQLEXPRESS\SQL\query|  
|名前付きパイプ接続を適用する、名前による既定のインスタンスへの接続。|np:APPHOST|  
|名前付きパイプ接続を適用する、名前による名前付きインスタンスへの接続。|np:APPHOST\SQLEXPRESS|  
  
## <a name="verifying-your-connection-protocol"></a>接続プロトコルの確認  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続している場合、次のクエリは現在の接続に使用されているプロトコルと認証方法 (NTLM または Kerberos) を返し、接続が暗号化されているかどうかを示します。  
  
```sql  
SELECT net_transport, auth_scheme, encrypt_option   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
```  
  
## <a name="related-tasks"></a>Related Tasks  
 [SQL Server インスタンスへのログイン &#40;コマンド プロンプト&#41;](../../database-engine/configure-windows/log-in-to-an-instance-of-sql-server-command-prompt.md)  
  
 以下のリソースは、接続の問題に関するトラブルシューティングに役立ちます。  
  
-   [SQL Server データベース エンジンへの接続のトラブルシューティングの方法](https://social.technet.microsoft.com/wiki/contents/articles/how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx)  
  
-   [SQL の接続問題のトラブルシューティングの手順](/archive/blogs/sql_protocols/steps-to-troubleshoot-sql-connectivity-issues)  
  
## <a name="related-content"></a>関連コンテンツ  
 [認証モードの選択](../../relational-databases/security/choose-an-authentication-mode.md)  
  
 [sqlcmd ユーティリティの使用](../../ssms/scripting/sqlcmd-use-the-utility.md)  
  
 [ログインの作成](../../t-sql/lesson-2-configuring-permissions-on-database-objects.md)
  
