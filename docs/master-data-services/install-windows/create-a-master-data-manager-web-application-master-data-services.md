---
title: マスターデータマネージャー web アプリケーションの作成
description: マスターデータマネージャー web アプリケーションは、ユーザーがマスターデータを操作するためのインターフェイスを提供し、管理者が MDS を構成および管理できるようにします。
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 241d46d7-8008-47f6-bebd-0dfff1cc856a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: df266fd09cfdd586d5f2fc438791104bf7097938
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100344825"
---
# <a name="create-a-master-data-manager-web-application-master-data-services"></a>マスターデータマネージャー web アプリケーションを作成する (マスターデータサービス)

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションは、マスター データを操作するためのユーザー用インターフェイスと、MDS を構成および管理するための管理者用インターフェイスを提供します。  
  
 Web アプリケーションは、必ず Web サイトに含める必要があります。 Web アプリケーションを作成するには、次のいずれかを実行する必要があります。  
  
-   既定の Web サイトを使用し、Web アプリケーションを作成する。  
  
-   既存の Web サイトを使用し、Web アプリケーションを作成する。  
  
-   新しい Web サイトを作成する (これにより Web アプリケーションが自動的に作成されます)。  
  
 Web アプリケーションを作成したら、それを [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベースに関連付けます。  
  
## <a name="prerequisites"></a>必須コンポーネント  
  
-   データベースをホストするコンピューターの要件の詳細については、「[Web アプリケーションの要件 &#40;マスター データ サービス&#41;](../../master-data-services/install-windows/web-application-requirements-master-data-services.md)」を参照してください。  
  
## <a name="to-create-a-master-data-manager-web-application-in-a-new-website"></a>新しい Web サイトにマスター データ マネージャー Web アプリケーションを作成するには  
 新しい Web サイトを作成した場合、ルート Web アプリケーションは [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションです。 また、作成された Web アプリケーションは新しいアプリケーション プールに追加されます。  
  
> [!NOTE]  
>  この手順を使用した場合、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションの仮想パスと別名を指定することはできません。 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]の仮想パスと別名を指定する場合は、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションとして構成されていない既存の Web サイトに Web アプリケーションを作成する必要があります。  
  
 また [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] では、HTTP バインドのみを含むサイトの作成もサポートされます。 HTTPS バインドを追加するには、 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] で新しいサイトとアプリケーションを作成します。詳細については、「 [マスター データ マネージャー Web アプリケーションのセキュリティ保護](../../master-data-services/install-windows/secure-a-master-data-manager-web-application.md) 」を参照してください。  
  
#### <a name="to-create-a-master-data-manager-web-application-in-a-new-website"></a>新しい Web サイトにマスター データ マネージャー Web アプリケーションを作成するには  
  
1.  [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]を開きます。  
  
2.  左ペインで **[Web の構成]** をクリックします。  
  
3.  **[Web の構成]** ページにある Web サイトの一覧で、 **[新規 Web サイトの作成]** を選択します。  
  
4.  **[Web サイトの作成]** ダイアログ ボックスで、新しい Web サイトの情報を指定します。 ダイアログ ボックスのユーザー インターフェイス (UI) オプションの詳細については、「[[Web サイトの作成] ダイアログ ボックス &#40;マスター データ サービス構成マネージャー&#41;](../../master-data-services/create-website-dialog-box-master-data-services-configuration-manager.md)」を参照してください。  
  
5.  **[OK]** をクリックします。  
  
## <a name="to-create-a-master-data-manager-web-application-in-an-existing-website"></a>既存の Web サイトにマスター データ マネージャー Web アプリケーションを作成するには  
 既存の Web サイトに Web アプリケーションを作成する場合は、Web アプリケーションの仮想パスと別名を選択できます。 作成された Web アプリケーションは新しいアプリケーション プールに追加されます。  
  
#### <a name="to-create-a-master-data-manager-web-application-in-an-existing-website"></a>既存の Web サイトにマスター データ マネージャー Web アプリケーションを作成するには  
  
1.  [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]を開きます。  
  
2.  左ペインで **[Web の構成]** をクリックします。  
  
3.  **[Web の構成]** ページで、 **[Web サイト]** ボックスの一覧から、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションを作成する Web サイトを選択します。  
  
4.  **[アプリケーションの作成]** をクリックします。  
  
5.  **[Web アプリケーションの作成]** ダイアログ ボックスで、新しい Web アプリケーションの情報を指定します。 ウィザードのユーザー インターフェイス (UI) オプションの詳細については、「[[Web アプリケーションの作成] ダイアログ ボックス &#40;マスター データ サービス構成マネージャー&#41;](../../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md)」を参照してください。  
  
6.  **[OK]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
  
-   Web アプリケーションを [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベースに関連付けます。 詳細については、「 [Master Data Services データベースと Web アプリケーションの関連付け](../../master-data-services/install-windows/associate-a-master-data-services-database-and-web-application.md)」を参照してください。  
  
-   または、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] トランスポート層セキュリティ (TLS) を使用してコンテンツを暗号化する場合は、web アプリケーションをホストする web サイトを構成します (これは Secure Sockets Layer (SSL) と呼ばれます)。 Web サーバーのサーバー証明書を構成し、サイトの HTTPS バインドと TLS 設定を構成するには、IIS マネージャーなどのインターネットインフォメーションサービス (IIS) ツールを使用する必要があります。 詳細については、「 [マスター データ マネージャー Web アプリケーションのセキュリティ保護](../../master-data-services/install-windows/secure-a-master-data-manager-web-application.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [マスター データ サービスのインストール](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
