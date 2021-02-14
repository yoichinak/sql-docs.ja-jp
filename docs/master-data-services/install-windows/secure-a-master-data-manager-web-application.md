---
title: マスター データ マネージャー Web アプリケーションのセキュリティ保護
description: SQL Server では、HTTPS を使用してマスターデータマネージャー web アプリケーションをセキュリティで保護することができます。 管理者である必要があります。 web サーバーに MDS をインストールする必要があります。
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: e360ba3a-e96b-4f85-b588-ed1f767fa973
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 5e941ce4f06961f19e0d5f4a0dc96aff31039647
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100344749"
---
# <a name="secure-a-master-data-manager-web-application"></a>マスター データ マネージャー Web アプリケーションのセキュリティ保護

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  HTTPS を使用して [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションをセキュリティ保護できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションは、HTTP または HTTPS のいずれかを使用できますが、両方を使用することはできません。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 この手順を実行するには  
  
-   [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] がインストールされている Web サーバーの管理者である必要があります。  
  
-   MDS が Web サーバーにインストールされていて、Web アプリケーションが存在する必要があります。 詳細については、「 [マスター データ サービスのインストール](../../master-data-services/install-windows/install-master-data-services.md) 」および「 [マスター データ マネージャー Web アプリケーションの作成 &#40;マスター データ サービス&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)」を参照してください。  

- [Windows 認証の IIS 拡張保護を](/iis/configuration/system.webserver/security/authentication/windowsauthentication/extendedprotection/) 有効にしないでください。 

- 使用可能なすべての IP アドレスでリッスンするように web サーバーを構成します。 特定の IP アドレスでリッスンするように Web サーバーを構成しないでください。 

### <a name="to-secure-the-master-data-manager-web-application-with-https"></a>HTTPS を使用してマスター データ マネージャー Web アプリケーションをセキュリティ保護するには  
  
1.  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションが HTTP を使用して正しく構成されていることを確認した後、IIS で証明書を作成します。 詳細については、「 [IIS 7 でサーバー証明書を構成する](https://technet.microsoft.com/library/cc732230\(WS.10\).aspx)」を参照してください。  
  
2.  **[接続]** ペインの **[サイト]** で、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションをホストするサイトをクリックします。  
  
3.  **[操作]** ウィンドウで、**[バインド]** をクリックします。  
  
4.  **[追加]** をクリックします。  
  
5.  一覧から、 **[https]** を選択します。  
  
6.  TLS/SSL 証明書を選択します。  
  
7.  **[OK]** をクリックします。  
  
8.  任意。 HTTP を削除してユーザーが HTTPS のみを使用してサイトにアクセスできるようにするには、一覧の **[http]** の行をクリックします。 **[削除]** をクリックし、確認のダイアログ ボックスで **[はい]** をクリックします。  
  
    > [!IMPORTANT]  
    >  HTTP を削除した後に basicHttp 構成および wsHttpBinding 構成を変更する必要があります。  
  
9. **[サイト バインド]** ダイアログ ボックスを閉じるには、 **[閉じる]** をクリックします。  
  
10. ここで、 *ドライブ*:\Program Files\Microsoft SQL Server\130\Master Data Services\WebApplication にある web.config ファイルを開きます。  
  
11. " `<security mode="Message">` " という文字列を探して、" `<security mode="Transport">`" に変更します。  

12. Silverlight クライアントで発生する可能性がある問題を回避するには、`<serviceMetadata httpGetEnable="true" httpsGetEnabled="false">` を `<serviceMetadata httpGetEnable="false" httpsGetEnabled="true">` に変更します。

13. ファイルを保存して閉じます。 エラーが発生した場合は、UAC が有効になっている可能性があります。 これで、ユーザーが HTTPS を使用してサイトにアクセスできるようになりました。  

  
## <a name="see-also"></a>参照  
 [マスター データ マネージャー Web アプリケーションの作成 &#40;マスター データ サービス&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
