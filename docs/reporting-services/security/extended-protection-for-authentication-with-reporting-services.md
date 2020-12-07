---
description: Reporting Services での認証の拡張保護
title: Reporting Services での認証の拡張保護 | Microsoft Docs
ms.date: 06/22/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
ms.assetid: eb5c6f4a-3ed5-430b-a712-d5ed4b6b9b2b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7f152bf79c030fee3ce480d455c54fbdfad4b719
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91935481"
---
# <a name="extended-protection-for-authentication-with-reporting-services"></a>Reporting Services での認証の拡張保護

  拡張保護は、最新バージョンの [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows オペレーティング システムに追加された一連の拡張機能です。 拡張保護により、アプリケーションで資格情報と認証を保護する方法の幅が広がります。 この機能自体は、資格情報の転送をはじめとする特定の攻撃を直接防ぐものではありませんが、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] などのアプリケーションに対し、認証の拡張保護を適用するためのインフラストラクチャを提供します。  
  
 拡張保護に含まれる認証の拡張機能を代表するのが、サービス バインドとチャネル バインドです。 チャネル バインドでは、チャネル バインド トークン (CBT) を使用して、2 つのエンド ポイント間に確立されたチャネルに問題が生じていないかどうかを確認します。 サービス バインドでは、サービス プリンシパル名 (SPN) を使用して認証トークンの目的の送信先を検証します。 拡張保護の詳細な背景情報については、「 [拡張保護付き統合 Windows 認証](https://go.microsoft.com/fwlink/?LinkId=179922)」を参照してください。  
  
SQL Server Reporting Services (SSRS) でサポートおよび適用されるのは、オペレーティング システムで有効化し、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] で構成した拡張保護です。 既定では、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] はネゴシエート認証または NTLM 認証を指定する要求を受け入れるため、オペレーティング システムでの拡張保護のサポートと [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の拡張保護機能を活用できます。  
  
> [!IMPORTANT]  
>  既定では、Windows の拡張保護は有効になっていません。 Windows で拡張保護を有効にする方法の詳細については、「 [認証に対する保護の強化](https://go.microsoft.com/fwlink/?LinkID=178431)」を参照してください。 認証を成功させるためには、オペレーティング システムとクライアントの認証スタックが両方とも拡張保護をサポートしている必要があります。 旧バージョンのオペレーティング システムを使用している場合は、拡張保護に対応したコンピューターを準備するために、1 つ以上の更新プログラムのインストールが必要になることがあります。 拡張保護の最新情報については、 [こちら](https://go.microsoft.com/fwlink/?LinkId=183362)を参照してください。  

## <a name="reporting-services-extended-protection-overview"></a>Reporting Services の拡張保護の概要

SSRS では、オペレーティング システムで有効になっている拡張保護がサポートされ、適用されます。 オペレーティング システムが拡張保護をサポートしていないか、拡張保護機能がオペレーティング システムで有効化されていない場合、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の拡張保護機能を使用した認証は失敗します。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の拡張保護では、TLS/SSL 証明書も必要になります。 詳細については、「[ネイティブ モードのレポート サーバーでの TLS 接続の構成](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)」をご覧ください  
  
> [!IMPORTANT]  
>  既定では、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の拡張保護は有効になっていません。 この機能を有効にするには、 **rsreportserver.config** 構成ファイルを変更するか、WMI API を使用して構成ファイルを更新します。 SSRS には、拡張保護の設定を変更または確認するためのユーザー インターフェイスが用意されていません。 詳細については、このトピックの [構成設定に関するセクション](#ConfigurationSettings) を参照してください。  
  
 拡張保護の設定に加えた変更や設定の不適切な構成が原因で一般的な問題が発生しても、目に見えるエラー メッセージやダイアログ ウィンドウで示されることはありません。 拡張保護の構成や互換性に関係する問題が生じると、認証に失敗し、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のトレース ログにエラーが記録されます。  
  
> [!IMPORTANT]
>  一部のデータ アクセス テクノロジでは、拡張保護がサポートされないことがあります。 データ アクセス テクノロジは、SQL Server データ ソースおよび [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] カタログ データベースへの接続に使用されます。 データ アクセス テクノロジで拡張保護がサポートされない場合、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] に次のような影響が生じます。  
> 
>  -   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] カタログ データベースを実行する SQL Server は拡張保護を有効にできません。つまり、レポート サーバーがカタログ データベースへの接続に失敗し、認証エラーが返されます。  
> -   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート データ ソースとして使用される SQL Server は拡張保護を有効にできません。つまり、レポート サーバーがレポート データ ソースへの接続に失敗し、認証エラーが返されます。  
> 
>  データ アクセス テクノロジのドキュメントには、拡張保護のサポートに関する情報が記載されています。  
  
### <a name="upgrade"></a>アップグレード  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サーバーを SQL Server 2016 にアップグレードすると、既定値の設定された構成設定が **rsreportserver.config** ファイルに追加されます。 既存の設定がある場合は、SQL Server 2016 のインストールにより、その設定が **rsreportserver.config** ファイルで保持されます。  
  
-   構成設定が **rsreportserver.config** 構成ファイルに追加されると、既定の動作として [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の拡張保護機能が無効になるため、このトピックの説明に従って有効にする必要があります。 詳細については、このトピックの [構成設定に関するセクション](#ConfigurationSettings) を参照してください。  
  
-   **RSWindowsExtendedProtectionLevel** 設定の既定値は **Off**です。  
  
-   **RSWindowsExtendedProtectionScenario** 設定の既定値は **Proxy**です。  
  
-   アップグレード アドバイザーは、オペレーティング システムまたは [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の現在のインストールで拡張保護のサポートが有効かどうかを確認しません。  
  
### <a name="what-reporting-services-extended-protection-does-not-cover"></a>Reporting Services の拡張保護でサポートされない機能とシナリオ  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の拡張保護機能では、次の機能領域とシナリオがサポートされません。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のカスタム セキュリティ拡張機能の作成者は、拡張保護のサポートをカスタム セキュリティ拡張機能に追加する必要があります。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインストールで使用または追加されるコンポーネントを開発したサード パーティ ベンダーは、そのコンポーネントを更新して拡張保護をサポートする必要があります。 詳細については、サード パーティ ベンダーに問い合わせてください。  
  
## <a name="deployment-scenarios-and-recommendations"></a>配置のシナリオと推奨事項  
 以下のシナリオでは、さまざまな配置とトポロジを紹介します。また、それらを [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の拡張保護でセキュリティ保護するにあたっての推奨構成も示します。  
  
### <a name="direct"></a>直接  
 このシナリオでは、イントラネット環境などでのレポート サーバーへの直接的な接続について説明します。  
  
|シナリオ|シナリオを表した図|セキュリティ保護の方法|  
|--------------|----------------------|-------------------|  
|直接的な TLS 通信を使用します。<br /><br /> レポート サーバーにより、クライアントからレポート サーバーへのチャネル バインドが適用されます。|![RS_ExtendedProtection_DirectSSL](../../reporting-services/security/media/rs-extendedprotection-directssl.gif "RS_ExtendedProtection_DirectSSL")<br /><br /> 1) クライアント アプリケーション<br /><br /> 2) レポート サーバー|**RSWindowsExtendedProtectionLevel** を **Allow** または **Require**に設定します。<br /><br /> **RSWindowsExtendedProtectionScenario** を **Direct**に設定します。<br /><br /> <br /><br /> -チャネル バインドには TLS チャネルが使用されるため、サービス バインドは不要です。|  
|直接的な HTTP 通信を使用します。 レポート サーバーにより、クライアントからレポート サーバーへのサービス バインドが適用されます。|![RS_ExtendedProtection_Direct](../../reporting-services/security/media/rs-extendedprotection-direct.gif "RS_ExtendedProtection_Direct")<br /><br /> 1) クライアント アプリケーション<br /><br /> 2) レポート サーバー|**RSWindowsExtendedProtectionLevel** を **Allow** または **Require**に設定します。<br /><br /> **RSWindowsExtendedProtectionScenario** を **Any**に設定します。<br /><br /> <br /><br /> -TLS チャネルが存在しないため、チャネル バインドは適用できません。<br /><br /> \- サービス バインドの検証は可能ですが、チャネル バインドがないため完全な保護は不可能です。サービス バインド自体で防ぐことができるのは、基本的な脅威のみです。|  
  
### <a name="proxy-and-network-load-balancing"></a>プロキシとネットワーク負荷分散  
 クライアント アプリケーションは、TLS を実行するデバイスまたはソフトウェアに接続し、認証のためにサーバーに資格情報を渡します。たとえば、エクストラネット、インターネット、セキュリティで保護されたイントラネットなどです。 クライアントはプロキシに接続します。つまり、すべてのクライアントがプロキシを使用します。  
  
 この状況は、ネットワーク負荷分散 (NLB) デバイスを使用する場合と同じです。  
  
|シナリオ|シナリオを表した図|セキュリティ保護の方法|  
|--------------|----------------------|-------------------|  
|HTTP 通信を使用します。 レポート サーバーにより、クライアントからレポート サーバーへのサービス バインドが適用されます。|![RS_ExtendedProtection_Indirect](../../reporting-services/security/media/rs-extendedprotection-indirect.gif "RS_ExtendedProtection_Indirect")<br /><br /> 1) クライアント アプリケーション<br /><br /> 2) レポート サーバー<br /><br /> 3) プロキシ|**RSWindowsExtendedProtectionLevel** を **Allow** または **Require**に設定します。<br /><br /> **RSWindowsExtendedProtectionScenario** を **Any**に設定します。<br /><br /> <br /><br /> -TLS チャネルが存在しないため、チャネル バインドは適用できません。<br /><br /> \- レポート サーバーは、サービス バインドが適切に適用されていることを確認するために、プロキシ サーバーの名前を把握できるように構成する必要があります。|  
|HTTP 通信を使用します。<br /><br /> レポート サーバーによって、クライアントからプロキシへのチャネル バインドと、クライアントからレポート サーバーへのサービス バインドが適用されます。|![RS_ExtendedProtection_Indirect_SSL](../../reporting-services/security/media/rs-extendedprotection-indirect-ssl.gif "RS_ExtendedProtection_Indirect_SSL")<br /><br /> 1) クライアント アプリケーション<br /><br /> 2) レポート サーバー<br /><br /> 3) プロキシ|オン <br />                    **RSWindowsExtendedProtectionLevel** を **Allow** または **Require**に設定します。<br /><br /> **RSWindowsExtendedProtectionScenario** を **Proxy**に設定します。<br /><br /> <br /><br /> -プロキシへの TLS チャネルを利用できるため、プロキシへのチャネル バインドを適用できます。<br /><br /> \- サービス バインドも適用できます。<br /><br /> \- レポート サーバーがプロキシ名を把握できる必要があります。レポート サーバーの管理者は、ホスト ヘッダーを使用してプロキシの URL 予約を作成するか、Windows レジストリ エントリ **BackConnectionHostNames**でプロキシ名を構成する必要があります。|  
|セキュリティで保護されたプロキシとの間接的な HTTPS 通信を使用します。 レポート サーバーによって、クライアントからプロキシへのチャネル バインドと、クライアントからレポート サーバーへのサービス バインドが適用されます。|![RS_ExtendedProtection_IndirectSSLandHTTPS](../../reporting-services/security/media/rs-extendedprotection-indirectsslandhttps.gif "RS_ExtendedProtection_IndirectSSLandHTTPS")<br /><br /> 1) クライアント アプリケーション<br /><br /> 2) レポート サーバー<br /><br /> 3) プロキシ|オン <br />                    **RSWindowsExtendedProtectionLevel** を **Allow** または **Require**に設定します。<br /><br /> **RSWindowsExtendedProtectionScenario** を **Proxy**に設定します。<br /><br /> <br /><br /> -プロキシへの TLS チャネルを利用できるため、プロキシへのチャネル バインドを適用できます。<br /><br /> \- サービス バインドも適用できます。<br /><br /> \- レポート サーバーがプロキシ名を把握できる必要があります。レポート サーバーの管理者は、ホスト ヘッダーを使用してプロキシの URL 予約を作成するか、Windows レジストリ エントリ **BackConnectionHostNames**でプロキシ名を構成する必要があります。|  
  
### <a name="gateway"></a>Gateway  
 このシナリオでは、TLS を実行してユーザーを認証するデバイスまたはソフトウェアに接続するクライアント アプリケーションについて説明します。 このデバイスまたはソフトウェアは、ユーザー コンテキストまたは別のユーザー コンテキストを偽装したうえで、レポート サーバーに対して要求を行います。  
  
|シナリオ|シナリオを表した図|セキュリティ保護の方法|  
|--------------|----------------------|-------------------|  
|間接的な HTTP 通信を使用します。<br /><br /> ゲートウェイによって、クライアントからゲートウェイへのチャネル バインドが適用されます。 ゲートウェイとレポート サーバーの間にはサービス バインドが確立されます。|![RS_ExtendedProtection_Indirect_SSL](../../reporting-services/security/media/rs-extendedprotection-indirect-ssl.gif "RS_ExtendedProtection_Indirect_SSL")<br /><br /> 1) クライアント アプリケーション<br /><br /> 2) レポート サーバー<br /><br /> 3) ゲートウェイ デバイス|**RSWindowsExtendedProtectionLevel** を **Allow** または **Require**に設定します。<br /><br /> **RSWindowsExtendedProtectionScenario** を **Any**に設定します。<br /><br /> <br /><br /> \- ゲートウェイがコンテキストを偽装し、新しい NTLM トークンを作成するため、クライアントからレポート サーバーへのチャネル バインドは確立できません。<br /><br /> -ゲートウェイとレポート サーバーの間で TLS が使用されないため、チャネル バインドは適用できません。<br /><br /> \- サービス バインドを適用できます。<br /><br /> \- 管理者は、チャネル バインドを適用するようにゲートウェイ デバイスを構成する必要があります。|  
|セキュリティで保護されたゲートウェイとの間接的な HTTPS 通信を使用します。 ゲートウェイによってクライアントからゲートウェイへのチャネル バインドが適用され、レポート サーバーによってゲートウェイからレポート サーバーへのチャネル バインドが適用されます。|![RS_ExtendedProtection_IndirectSSLandHTTPS](../../reporting-services/security/media/rs-extendedprotection-indirectsslandhttps.gif "RS_ExtendedProtection_IndirectSSLandHTTPS")<br /><br /> 1) クライアント アプリケーション<br /><br /> 2) レポート サーバー<br /><br /> 3) ゲートウェイ デバイス|**RSWindowsExtendedProtectionLevel** を **Allow** または **Require**に設定します。<br /><br /> **RSWindowsExtendedProtectionScenario** を **Direct**に設定します。<br /><br /> <br /><br /> \- ゲートウェイがコンテキストを偽装し、新しい NTLM トークンを作成するため、クライアントからレポート サーバーへのチャネル バインドは確立できません。<br /><br /> \- ゲートウェイとレポート サーバーの間では TLS が使用されるため、チャネル バインドを適用できます。<br /><br /> \- サービス バインドは不要です。<br /><br /> \- 管理者は、チャネル バインドを適用するようにゲートウェイ デバイスを構成する必要があります。|  
  
### <a name="combination"></a>組み合わせ  
 このシナリオでは、クライアントがプロキシに接続するエクストラネット環境またはインターネット環境について説明します。 これは、クライアントがレポート サーバーに接続するイントラネット環境と組み合わせたシナリオです。  
  
|シナリオ|シナリオを表した図|セキュリティ保護の方法|  
|--------------|----------------------|-------------------|  
|クライアントからレポート サーバー サービスへの間接的なアクセスと直接的なアクセスを行います。クライアントからプロキシ、またはクライアントからレポート サーバーへの接続で TLS を使用しません。|1) クライアント アプリケーション<br /><br /> 2) レポート サーバー<br /><br /> 3) プロキシ<br /><br /> 4) クライアント アプリケーション|**RSWindowsExtendedProtectionLevel** を **Allow** または **Require**に設定します。<br /><br /> **RSWindowsExtendedProtectionScenario** を **Any**に設定します。<br /><br /> <br /><br /> \- クライアントからレポート サーバーへのサービス バインドを適用できます。<br /><br /> \- レポート サーバーがプロキシ名を把握できる必要があります。レポート サーバーの管理者は、ホスト ヘッダーを使用してプロキシの URL 予約を作成するか、Windows レジストリ エントリ **BackConnectionHostNames**でプロキシ名を構成する必要があります。|  
|クライアントからレポート サーバーへの間接的なアクセスと直接的なアクセスを行います。その際、クライアントからプロキシまたはレポート サーバーへの TLS 接続を確立します。|![RS_ExtendedProtection_CombinationSSL](../../reporting-services/security/media/rs-extendedprotection-combinationssl.gif "RS_ExtendedProtection_CombinationSSL")<br /><br /> 1) クライアント アプリケーション<br /><br /> 2) レポート サーバー<br /><br /> 3) プロキシ<br /><br /> 4) クライアント アプリケーション|**RSWindowsExtendedProtectionLevel** を **Allow** または **Require**に設定します。<br /><br /> **RSWindowsExtendedProtectionScenario** を **Proxy**に設定します。<br /><br /> <br /><br /> \- チャネル バインドを適用できます。<br /><br /> \- レポート サーバーがプロキシ名を把握できる必要があります。レポート サーバーの管理者は、ホスト ヘッダーを使用してプロキシの URL 予約を作成するか、Windows レジストリ エントリ **BackConnectionHostNames**でプロキシ名を構成する必要があります。|  
  
## <a name="configuring-reporting-services-extended-protection"></a>Reporting Services の拡張保護の構成  
 **rsreportserver.config** ファイルには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の拡張保護の動作を制御する構成値が含まれています。  
  
 **rsreportserver.config** ファイルの使用と編集の詳細については、「 [RsReportServer.config 構成ファイル](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)」を参照してください。 拡張保護の設定は、WMI API を使用して変更および確認することもできます。 詳細については、「 [SetExtendedProtectionSettings Method &#40;WMI MSReportServer_ConfigurationSetting&#41; (SetExtendedProtectionSettings メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;)](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md)」を参照してください。  
  
 構成設定の検証が失敗した場合、 **RSWindowsNTLM**、 **RSWindowsKerberos** 、および **RSWindowsNegotiate** の各認証の種類がレポート サーバーで無効になります。  
  
###  <a name="configuration-settings-for-reporting-services-extended-protection"></a><a name="ConfigurationSettings"></a> Reporting Services の拡張保護の構成設定  
 次の表では、拡張保護の **rsreportserver.config** に含まれる構成設定について説明します。  
  
|設定|説明|  
|-------------|-----------------|  
|**RSWindowsExtendedProtectionLevel**|拡張保護の適用レベルを指定します。 有効な値は次のとおりです。<br /><br /> **Off**:既定値。 チャネル バインドまたはサービス バインドの検証は行われません。<br /><br /> **Allow** は拡張保護をサポートしますが、要求しません。  以下を指定します。<br /><br /> \- 拡張保護がサポートされているオペレーティング システムで実行中のクライアント アプリケーションに対し、拡張保護が適用されます。 保護の適用方法は、 **RsWindowsExtendedProtectionScenario**設定によって決まります<br /><br /> \- 拡張保護がサポートされていないオペレーティング システムで実行中のアプリケーションに対し、認証が許可されます。<br /><br /> **Require** は以下を指定します。<br /><br /> \- 拡張保護がサポートされているオペレーティング システムで実行中のクライアント アプリケーションに対し、拡張保護が適用されます。<br /><br /> \- 拡張保護がサポートされていないオペレーティング システムで実行中のアプリケーションに対し、認証は許可 **されません** 。|  
|**RsWindowsExtendedProtectionScenario**|検証する拡張保護の形式を指定します。チャネル バインド、サービス バインド、またはその両方を指定します。 有効な値は次のとおりです。<br /><br /> **Proxy**:既定値。 以下を指定します。<br /><br /> \- チャネル バインド トークンが存在する場合は、Windows NTLM 認証、Kerberos 認証、およびネゴシエート認証が行われます。<br /><br /> \- サービス バインドが適用されます。<br /><br /> **Any** は以下を指定します。<br /><br /> \- Windows NTLM 認証、Kerberos 認証、およびネゴシエート認証とチャネル バインドは要求されません。<br /><br /> \- サービス バインドが適用されます。<br /><br /> **Direct** は以下を指定します。<br /><br /> -CBT と、現在のサービスへの TLS 接続が存在し、TLS 接続の CBT が NTLM、Kerberos、またはネゴシエート トークンの CBT に一致する場合に、それぞれ Windows NTLM 認証、Kerberos 認証、またはネゴシート認証が行われます。<br /><br /> \- サービス バインドは適用されません。<br /><br /> <br /><br /> 注:**RsWindowsExtendedProtectionLevel** を **OFF** に設定した場合、**RsWindowsExtendedProtectionScenario** 設定は無視されます。|  
  
 **rsreportserver.config** 構成ファイル内のエントリの例を次に示します。  
  
```  
<Authentication>  
         <RSWindowsExtendedProtectionLevel>Allow</RSWindowsExtendedProtectionLevel>  
         <RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionLevel>  
</Authentication>  
```  
  
## <a name="service-binding-and-included-spns"></a>サービス バインドと含まれる SPN  
 サービス バインドでは、サービス プリンシパル名 (SPN) を使用して認証トークンの目的の送信先を検証します。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] は、既存の URL 予約情報を使用して、有効と見なされる SPN のリストを作成します。 SPN と URL 予約の両方の検証に URL 予約情報を使用することにより、システム管理者による一元管理が可能になります。  
  
 有効な SPN のリストが更新されるのは、レポート サーバーを起動したとき、拡張保護の構成設定を変更したとき、またはアプリケーション ドメインをリサイクルしたときです。  
  
 有効な SPN のリストは、各アプリケーションに固有です。 たとえば、レポート マネージャーとレポート サーバーでは、有効な SPN のリストが別々に計算されます。  
  
 アプリケーションに対して計算される有効な SPN のリストは、次の要素によって決定されます。  
  
-   各 URL 予約。  
  
-   Reporting Services サービス アカウント用にドメイン コントローラーから取得した各 SPN。  
  
-   URL 予約にワイルドカード文字 (* または +) が含まれている場合は、レポート サーバーによってホスト コレクションから各エントリが追加されます。  
  
### <a name="hosts-collection-sources"></a>ホスト コレクションのソース  
 次の表に、ホスト コレクションのソースとなり得るものを示します。  
  
|ソースの種類|説明|  
|--------------------|-----------------|  
|ComputerNameDnsDomain|ローカル コンピューターに割り当てられた DNS ドメインの名前。 ローカル コンピューターがクラスター内のノードである場合、クラスターの仮想サーバーの DNS ドメイン名が使用されます。|  
|ComputerNameDnsFullyQualified|ローカル コンピューターを一意に識別する完全修飾 DNS 名。 この名前は、 *HostName*.*DomainName*という形式で DNS ホスト名と DNS ドメイン名を組み合わせたものです。 ローカル コンピューターがクラスター内のノードである場合、クラスターの仮想サーバーの完全修飾 DNS 名が使用されます。|  
|ComputerNameDnsHostname|ローカル コンピューターの DNS ホスト名。 ローカル コンピューターがクラスター内のノードである場合、クラスターの仮想サーバーの DNS ホスト名が使用されます。|  
|ComputerNameNetBIOS|ローカル コンピューターの NetBIOS 名。 ローカル コンピューターがクラスター内のノードである場合、クラスターの仮想サーバーの NetBIOS 名が使用されます。|  
|ComputerNamePhysicalDnsDomain|ローカル コンピューターに割り当てられた DNS ドメインの名前。 ローカル コンピューターがクラスター内のノードである場合、クラスターの仮想サーバーの名前ではなく、ローカル コンピューターの DNS ドメイン名が使用されます。|  
|ComputerNamePhysicalDnsFullyQualified|コンピューターを一意に識別する完全修飾 DNS 名。 ローカル コンピューターがクラスター内のノードである場合、クラスターの仮想サーバーの名前ではなく、ローカル コンピューターの完全修飾 DNS 名が使用されます。<br /><br /> この完全修飾 DNS 名は、 *HostName*.*DomainName*という形式で DNS ホスト名と DNS ドメイン名を組み合わせたものです。|  
|ComputerNamePhysicalDnsHostname|ローカル コンピューターの DNS ホスト名。 ローカル コンピューターがクラスター内のノードである場合、クラスターの仮想サーバーの名前ではなく、ローカル コンピューターの DNS ホスト名が使用されます。|  
|ComputerNamePhysicalNetBIOS|ローカル コンピューターの NetBIOS 名。 ローカル コンピューターがクラスター内のノードである場合、クラスターの仮想サーバーの名前ではなく、ローカル コンピューターの NetBIOS 名が使用されます。|  
  
詳細については、「[レポート サーバーのサービス プリンシパル名 &#40;SPN&#41; の登録](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md)」および「[URL の予約と登録について &#40;レポート サーバーの構成マネージャー&#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md)」を参照してください。  
  
## <a name="next-steps"></a>次のステップ

[拡張保護を使用したデータベース エンジンへの接続](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)   
[認証の拡張保護の概要](https://go.microsoft.com/fwlink/?LinkID=177943)   
[拡張保護付き統合 Windows 認証](https://go.microsoft.com/fwlink/?LinkId=179922)   
[マイクロソフト セキュリティ アドバイザリ:認証の拡張保護](https://go.microsoft.com/fwlink/?LinkId=179923)   
[Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)   
[RsReportServer.config 構成ファイル](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[SetExtendedProtectionSettings Method &#40;WMI MSReportServer_ConfigurationSetting&#41; (SetExtendedProtectionSettings メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;)](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
