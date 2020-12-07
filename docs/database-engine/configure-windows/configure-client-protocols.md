---
title: クライアント プロトコルの構成 | Microsoft Docs
description: SQL Server でクライアント アプリケーションによって使用されるプロトコルを構成するさまざまな方法について説明します。 サポートされるプロトコルには、TCP/IP、名前付きパイプ、共有メモリがあります。
ms.custom: ''
ms.date: 07/27/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- default protocols
- network protocols [SQL Server], client configuration
- TCP/IP [SQL Server], client protocols
- disabling client protocols
- ordering protocols [SQL Server]
- protocols [SQL Server], order for client computers
- configure client protocols
- client protocols [SQL Server]
- protocols [SQL Server], client configuration
- default protocols, client
ms.assetid: 3dfa2702-ba65-43b4-a777-6727846e133a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cdb6f1d2db5a2a390f75a4215dce490625fcc699
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2020
ms.locfileid: "91669628"
---
# <a name="configure-client-protocols"></a>クライアント プロトコルの構成
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 構成マネージャーを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でクライアント アプリケーションによって使用されるクライアント プロトコルを構成する方法について説明します。 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、TCP/IP ネットワーク プロトコルおよび名前付きパイプ プロトコルを介したクライアント通信をサポートしています。 クライアントが、同じコンピューター上で[!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続している場合は、共有メモリ プロトコルも使用できます。 プロトコルの選択には、3 つの一般的な方法があります。  
  
-   すべてのクライアント アプリケーションを、同じネットワーク プロトコルを使用するように構成します。これを行うには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーでプロトコルの順序を設定します。  
  
-   1 つのクライアント アプリケーションを、異なるネットワーク プロトコルを使用するように構成します。これを行うには、別名を作成します。 詳細については、「[クライアントが使用するサーバーの別名の作成または削除 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)」を参照してください。  
  
-   sqlcmd.exe など、一部のクライアント アプリケーションでは、接続文字列の一部としてプロトコルを指定できます。 詳細については、「[sqlcmd によるデータベース エンジンへの接続](../../ssms/scripting/sqlcmd-connect-to-the-database-engine.md)」を参照してください。  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> SQL Server 構成マネージャーの使用  
  
###  <a name="to-enable-or-disable-a-client-protocol"></a><a name="EnableDisable"></a> クライアント プロトコルを有効または無効にするには  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーで、 **[SQL Server Native Client の構成]** を展開し、 **[クライアント プロトコル]** を右クリックして、 **[プロパティ]** をクリックします。  
  
2.  プロトコルを有効にするには、 **[無効なプロトコル]** ボックスでプロトコルをクリックし、 **[有効化]** をクリックします。  
  
3.  プロトコルを無効にするには、 **[有効なプロトコル]** ボックスでプロトコルをクリックし、 **[無効化]** をクリックします。  
  
###  <a name="to-change-the-default-protocol-or-the-protocol-order-for-client-computers"></a><a name="ChangeDefault"></a> 既定のプロトコル、またはクライアント コンピューターのプロトコルの順序を変更するには  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーで、 **[SQL Server Native Client の構成]** を展開し、 **[クライアント プロトコル]** を右クリックして、 **[プロパティ]** をクリックします。  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続するときに試行されるプロトコルの順序を変更するには、 **[有効なプロトコル]** ボックスで、**上へ移動**ボタンまたは**下へ移動**ボタンをクリックします。 **[有効なプロトコル]** ボックスの最上部に表示されているプロトコルが既定のプロトコルです。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーにより、サーバーの別名の構成や既定のクライアント ネットワーク ライブラリのレジストリ エントリが作成されます。 ただし、このアプリケーションでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアント ネットワーク ライブラリもネットワーク プロトコルもインストールされません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアント ネットワーク ライブラリは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ中にインストールされます。また、ネットワーク プロトコルは、Microsoft Windows セットアップの一部として (または**コントロール パネル**の **[ネットワーク接続]** を使用して) インストールされます。 特定のネットワーク プロトコルは、Windows のセットアップ時にインストールされないことがあります。 そのようなネットワーク プロトコルのインストールの詳細については、製造元のマニュアルを参照してください。  
  
###  <a name="to-configure-a-client-to-use-tcpip"></a><a name="Configure"></a> TCP/IP を使用するようにクライアントを構成するには  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーで、 **[SQL Server Native Client の構成]** を展開し、 **[クライアント プロトコル]** を右クリックして、 **[プロパティ]** をクリックします。  
  
2.  **[有効なプロトコル]** ボックスで上矢印と下矢印をクリックして、SQL Server への接続を試行する際のプロトコルの試行順序を変更します。 **[有効なプロトコル]** ボックスの最上部に表示されているプロトコルが既定のプロトコルです。  
  
 共有メモリ プロトコルは、 **[共有メモリ プロトコルを有効にする]** チェック ボックスをオンにすることで、別個に有効にします。  
  
## <a name="see-also"></a>参照  
 [remote login timeout サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md)  
  
