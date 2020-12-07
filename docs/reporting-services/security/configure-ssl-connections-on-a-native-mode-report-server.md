---
description: ネイティブ モードのレポート サーバーでの TLS 接続の構成
title: ネイティブ モードのレポート サーバーでの TLS 接続の構成 | Microsoft Docs
ms.date: 09/27/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Secure Sockets Layer (SSL)
ms.assetid: 212f2042-456a-4c0a-8d76-480b18f02431
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 15f8fddb50f1cc814c88cc721fd46ceba1581faf
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91934768"
---
# <a name="configure-tls-connections-on-a-native-mode-report-server"></a>ネイティブ モードのレポート サーバーでの TLS 接続の構成

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モードでは、HTTP SSL (Secure Sockets Layer) サービスを使用してレポート サーバーへの暗号化接続を確立します。 トランスポート層セキュリティ (TLS) は、以前は Secure Sockets Layer (SSL) と呼ばれていました。 レポート サーバー コンピューター上のローカルの証明書ストアに証明書 (.cer) ファイルがインストールされている場合、その証明書を [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の URL 予約にバインドして、暗号化チャネルでのレポート サーバー接続をサポートできます。  
  
> [!TIP]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モードを使用している場合、詳細については、SharePoint のマニュアルを参照してください。 たとえば、[SharePoint 2010 Web アプリケーションで TLS を有効にする方法](https://docs.microsoft.com/archive/blogs/sowmyancs/how-to-enable-ssl-on-a-sharepoint-2010-web-application)に関するページを参照してください。  
  
 インターネット インフォメーション サービス (IIS) でも HTTP SSL が使用されるため、IIS と [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を同じコンピューター上で実行する場合は、相互運用性に関する重要な問題について考慮する必要があります。 これらの問題の対処方法については、「IIS との相互運用性の問題」を確認してください。  
  
## <a name="server-certificate-requirements"></a>サーバー証明書の要件  
 コンピューター上にサーバー証明書がインストールされている必要があります (クライアント証明書はサポートされていません)。 Reporting Services には、証明書を要求、生成、ダウンロード、またはインストールするための機能は用意されていません。 Windows Server 2012 以降には証明書スナップインが用意されています。これを使用して、信頼されている証明機関から証明書を要求することができます。  
  
 テスト目的の場合は、ローカルで証明書を生成できます。 **MakeCert** ユーティリティとサンプル コマンドをテンプレートとして使用する場合は、ホストとしてサーバー名を指定し、コマンドの実行前にすべての改行を削除してください。 コマンドを DOS ウィンドウで実行する場合、コマンド全体を含めるためにウィンドウのバッファー サイズを増やす必要があることがあります。  
  
 IIS と [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を同じコンピューター上で実行している場合は、IIS マネージャー コンソール アプリケーションを使用して、証明書をコンピューター上にインストールできます。 IIS マネージャーには、信頼されている証明機関が行う後続の処理のために、証明書要求 (.crt) ファイルを作成およびパッケージ化するオプションが用意されています。 利用している証明機関によって、証明書 (.cer) ファイルが生成されて送り返されます。 IIS 管理コンソールを使用して、その証明書ファイルをローカル ストアにインストールできます。 詳細については、Technet の「 [SSL を使用して資格情報データを暗号化する](https://go.microsoft.com/fwlink/?LinkId=71123) 」を参照してください。  
  
## <a name="interoperability-issues-with-iis"></a>IIS との相互運用性の問題  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] と同じコンピューターに IIS が存在する場合、レポート サーバーへの TLS 接続に大きく影響します。  
  
-   IIS がインストールされている場合、必ず World Wide Web サービス (W3SVC) が実行されている必要があります。 HTTP SSL サービスは、IIS が実行中であることを検出すると、IIS に対する依存関係を作成します。 つまり、IIS と [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] が同じコンピューター上にインストールされている場合にレポート サーバー URL を TLS 接続用に構成する際は、必ず World Wide Web サービス (W3SVC) が実行されている必要があります。  
  
-   IIS をアンインストールすると、TLS がバインドされたレポート サーバー URL に対するサービスが一時的に中断されることがあります。 そのため、IIS をアンインストールした後はコンピューターを再起動することをお勧めします。  
  
     コンピューターの再起動は、すべての TLS セッションをキャッシュから消去するために必要です。 一部のオペレーティング システムでは、TLS セッションが最大 10 時間キャッシュされ、HTTP.SYS で URL 予約から TLS バインドが削除された後も https:// URL が引き続き機能する原因になります。 コンピューターを再起動すると、チャネルを使用するすべての開いている接続が閉じます。  
  
## <a name="bind-tls-to-a-reporting-services-url-reservation"></a>Reporting Services の URL 予約への TLS のバインド  
 次の手順には、証明書の要求、生成、ダウンロード、またはインストールの手順は含まれません。 証明書がインストールされ、使用できるようになっている必要があります。 指定する証明書のプロパティ、証明書を取得する証明機関、および証明書の要求とインストールに使用するツールやユーティリティは、任意に決めることができます。  
  
 証明書は [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用してバインドできます。 証明書がローカル コンピューターのストアに正しくインストールされていれば、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールによって検出され、 **[Web サービス URL]** ページと **[Web ポータル URL]** ページの **[SSL 証明書]** の一覧に表示されます。  
  
### <a name="to-configure-a-report-server-url-for-tls"></a>レポート サーバー URL を TLS 用に構成するには  
  
1.  Reporting Services 構成ツールを起動して、レポート サーバーに接続します。  
  
2.  **[Web サービス URL]** を選択します。  
  
3.  TLS/SSL 証明書の一覧を展開します。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] によって、ローカル ストアにあるサーバー認証証明書が検出されます。 インストールした証明書が一覧に表示されない場合は、サービスの再起動が必要になることがあります。 Reporting Services 構成ツールの **[レポート サーバーの状態]** ページにある **[停止]** ボタンと **[開始]** ボタンを使用して、サービスを再起動できます (トップ ページ)。  
  
4.  証明書を選択します。  
  
5.  **[Apply]** をクリックします。  
  
6.  URL をクリックして機能するかどうかを検証します。  
  
 URL をテストするには、レポート サーバー データベースが構成されている必要があります。 レポート サーバー データベースをまだ作成していない場合は、URL のテスト前に作成してください。  
  
 URL 予約は、Web ポータル URL とレポート サーバー Web サービス URL で別々に構成されます。 Web ポータルへのアクセスを TLS で暗号化されたチャネルで構成する場合も、引き続き次の手順を実行します。  
  
1.  **[Web ポータル URL]** にアクセスします。
  
2.  **[Advanced] \(詳細設定)** を選択します。  
  
3.  **[現在の Reporting Services 機能の複数の HTTPS ID]** で、 **[追加]** を選択します。  
  
4.  証明書を選択し、 **[OK]** を選択してから、 **[適用]** を選択します。  
  
5.  URL をテストして機能することを確認します。  
  
## <a name="how-certificate-bindings-are-stored"></a>証明書のバインドの格納方法  
 証明書のバインドは HTTP.SYS に格納されます。 また、定義したバインドの記述は、RSReportServer.config ファイルの **URLReservations** セクションに格納されます。 構成ファイル内の設定は、他の場所で指定された実際の値を記述しただけのものです。 値を構成ファイル内で直接変更することは避けてください。 構成設定は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツール、またはレポート サーバーの Windows Management Instrumentation (WMI) プロバイダーを使用して証明書をバインドするまで、ファイルには表示されません。  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] で TLS/SSL 証明書とのバインドを構成し、後でコンピューターから証明書を削除する場合は、コンピューターから証明書を削除する前に、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] からバインドを削除してください。 このようにしないと、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールまたは WMI を使用してバインドを削除できなくなり、"無効なパラメーター" エラーが発生します。 コンピューターから証明書を既に削除している場合は、Httpcfg.exe ツールを使用して HTTP.SYS からバインドを削除できます。 Httpcfg.exe の詳細については、Windows の製品マニュアルを参照してください。  
  
 TLS バインドは Microsoft Windows の共有リソースです。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーや、IIS マネージャーなどのその他のツールを使用して行われた変更は、同じコンピューター上の他のアプリケーションに影響を与えます。 バインドを編集するには、バインドを作成するときに使用したものと同じツールを使用することをお勧めします。  たとえば、Configuration Manager を使用して TLS バインドを作成した場合は、Configuration Manager を使用してバインドのライフ サイクルを管理することをお勧めします。 IIS マネージャーを使用してバインドを作成した場合は、IIS マネージャーを使用してバインドのライフ サイクルを管理することをお勧めします。 コンピューターに IIS をインストールしてから [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をインストールする場合は、IIS で TLS 構成を確認してから [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を構成してください。  
  
 レポート サーバー構成マネージャーを使用して [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] に対する TLS バインドを削除すると、インターネット インフォメーション サービス (IIS) が実行されているサーバーまたは別の HTTP.SYS サーバー上の Web サイトに対して、TLS が機能しなくなる場合があります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーによって、次のレジストリ キーが削除されます。**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HTTP\Parameters\SslBindingInfo\0.0.0.0:443** このレジストリ キーが削除されると、IIS の TLS バインドも削除されます。 このバインドがない場合、HTTPS プロトコルに TLS が提供されません。 この問題を診断するには、IIS マネージャーまたは HTTPCFG.exe コマンド ライン ユーティリティを使用します。 問題を解決するには、IIS マネージャーを使用して、Web サイトの TLS バインドを復元します。 今後この問題を防ぐためには、IIS マネージャーを使って TLS バインドを削除してから、IIS マネージャーを使って目的の Web サイトのバインドを復元します。 詳細については、サポート技術情報の記事の [SSL バインドを削除すると SSL が機能しなくなる問題に関するページ (https://support.microsoft.com/kb/956209/n)](https://support.microsoft.com/kb/956209/n) を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [レポート サーバーでの認証](../../reporting-services/security/authentication-with-the-report-server.md)   
 [レポート サーバーを構成および管理する &#40;SSRSネイティブ モード&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [RsReportServer.config 構成ファイル](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [レポート サーバー URL の構成 (レポート サーバー構成マネージャー)](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
