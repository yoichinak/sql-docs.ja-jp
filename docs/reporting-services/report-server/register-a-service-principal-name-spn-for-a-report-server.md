---
title: レポート サーバーのサービス プリンシパル名 (SPN) の登録 | Microsoft Docs
description: ネットワークで認証に Kerberos が使用されるとき、ドメイン ユーザーとして実行される場合に、レポート サーバー サービス用の SPN を作成する方法について説明します。
ms.date: 09/24/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: dda91d4f-77cc-4898-ad03-810ece5f8e74
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c87da88bcec8d1fcc29c282a1e012121a81f6f45
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91986708"
---
# <a name="register-a-service-principal-name-spn-for-a-report-server"></a>レポート サーバーのサービス プリンシパル名 (SPN) の登録
  相互認証に Kerberos プロトコルを使用するネットワークに [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を配置する場合に、レポート サーバー サービスをドメイン ユーザー アカウントとして実行するように構成するには、レポート サーバー サービスのサービス プリンシパル名 (SPN) を作成する必要があります。  
  
## <a name="about-spns"></a>SPN について  
 SPN は、Kerberos 認証を使用するネットワークでのサービスの一意識別子です。 サービス クラスとホスト名で構成されますが、ポートが含まれることもあります。 HTTP SPN の場合、ポートは不要です。 Kerberos 認証を使用するネットワークでは、ビルトイン コンピューター アカウント (NetworkService や LocalSystem など) またはユーザー アカウントにサーバーの SPN を登録する必要があります。 ビルトイン アカウントには、自動的に SPN が登録されます。 一方、ドメイン ユーザー アカウントでサービスを実行する場合は、使用するアカウントに手動で SPN を登録する必要があります。  
  
 SPN を作成するには、 **SetSPN** コマンド ライン ユーティリティを使用します。 詳細については、「  
  
-   [Setspn](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc731241(v=ws.11)) (https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc731241(v=ws.11)) 。  
  
-   [サービス プリンシパル名 (SPN) SetSPN の構文 (Setspn.exe)](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx) (https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx) 。  
  
 このユーティリティをドメイン コントローラーで実行するには、ドメイン管理者であることが必要です。  
  
## <a name="syntax"></a>構文  

setspn を使用して SPN を操作する場合は、SPN を正しい形式で入力する必要があります。 HTTP SPN の形式は `http/host` です。 SetSPN ユーティリティを使用してレポート サーバーの SPN を作成する場合は、次のようなコマンド構文を使用します。  
  
```  
Setspn -s http/<computer-name>.<domain-name> <domain-user-account>  
```  
  
 **SetSPN** は、Windows Server で使用できます。 **-s** 引数は、重複する SPN がないことを検証してから、SPN を追加します。 **注: -s** は Windows Server 2008 以降の Windows Server で使用できます。  
  
 **HTTP** はサービス クラスです。 レポート サーバー Web サービスは、HTTP.SYS で実行されます。 HTTP 用に SPN を作成すると、副次的に、HTTP.SYS で実行される同じコンピューター上のすべての Web アプリケーション (IIS でホストされるアプリケーションを含む) に対して、ドメイン ユーザー アカウントに基づいてチケットが付与されます。 これらのサービスを別のアカウントで実行すると、認証要求が失敗します。 この問題を回避するには、すべての HTTP アプリケーションが同じアカウントで実行されるように構成するか、またはアプリケーションごとにホスト ヘッダーを作成し、作成したホスト ヘッダーごとに個別の SPN を作成することを検討してください。 ホスト ヘッダーを構成する場合、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成にかかわらず DNS を変更する必要があります。  
  
 \<*computername*> と \<*domainname*> に指定した値により、レポート サーバーをホストするコンピューターの一意のネットワーク アドレス識別されます。 これは、ローカル ホスト名にすることも、完全修飾ドメイン名 (FQDN) にすることもできます。 ドメインが 1 つしかない場合、コマンド ラインから \<*domainname*> を省略できます。 \<*domain-user-account*> は、レポート サーバー サービスが実行され、SPN を登録する必要があるユーザー アカウントです。  
  
## <a name="register-an-spn-for-domain-user-account"></a>ドメイン ユーザー アカウントに対する SPN の登録  
  
### <a name="to-register-an-spn-for-a-report-server-service-running-as-a-domain-user"></a>ドメイン ユーザーとして実行されるレポート サーバー サービスの SPN を登録するには  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をインストールし、レポート サーバー サービスをドメイン ユーザー アカウントとして実行するように構成します。 この手順が完了しないと、ユーザーはレポート サーバーに接続できないので注意してください。  
  
2.  ドメイン コントローラーにドメイン管理者としてログオンします。  
  
3.  コマンド プロンプト ウィンドウを開きます。  
  
4.  次のコマンドをコピーし、プレースホルダーの値を実際のネットワークで有効な値で置き換えます。  
  
    ```  
    Setspn -s http/<computer-name>.<domain-name> <domain-user-account>  
    ```  
  
    例: `Setspn -s http/MyReportServer.MyDomain.com MyDomainUser`  
  
5.  コマンドを実行します。  
  
6.  **RsReportServer.config** ファイルを開き、 `<AuthenticationTypes>` セクションを探します。  
  
7.  このセクションの最初のエントリとして `<RSWindowsNegotiate/>` を追加し、Kerberos を有効にします。  
  
## <a name="see-also"></a>参照  
 [サービス アカウントの構成 (レポート サーバー構成マネージャー)](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [レポート サーバー サービス アカウントの構成 (レポート サーバー構成マネージャー)](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Reporting Services ネイティブ モードのレポート サーバーの管理](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
  
