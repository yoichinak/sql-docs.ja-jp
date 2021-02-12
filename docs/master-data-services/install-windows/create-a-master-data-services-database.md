---
title: マスター データ サービス データベースの作成
description: マスターデータマネージャー web アプリケーションとマスターデータサービス web サービスをサポートする新しいデータベースが必要な場合は、マスターデータサービスデータベースを作成します。
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 8373bb35-f0f9-4c3c-a53c-dfaa2ce567ac
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 464bfd4714e7cc7680b2a2800d1c2ae1711feeb1
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100272483"
---
# <a name="create-a-master-data-services-database"></a>マスター データ サービス データベースの作成

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web アプリケーションと [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web サービスをサポートする新しいデータベースが必要な場合は、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベースを作成します。  
  
## <a name="prerequisites"></a>必須コンポーネント  
  
-   データベースをホストするコンピューターの要件の詳細については、「[データベース要件 &#40;マスター データ サービス&#41;](../../master-data-services/install-windows/database-requirements-master-data-services.md)」を参照してください。  
  
### <a name="to-create-a-master-data-services-database"></a>Master Data Services データベースを作成するには  
  
1.  [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]を開きます。  
  
2.  左ペインで **[データベース構成]** をクリックします。  
  
3.  **[データベース構成]** ページで **[データベースの作成]** をクリックします。  
  
4.  データベースを作成および構成する **データベースの作成** ウィザードを完了します。 ウィザードのユーザー インターフェイス (UI) オプションの詳細については、「[データベースの作成ウィザード &#40;マスター データ サービス構成マネージャー&#41;](../../master-data-services/create-database-wizard-master-data-services-configuration-manager.md)」を参照してください。  
  
## <a name="next-steps"></a>次の手順  
  
-   データベースと Web アプリケーションのシステム設定を構成します。 詳細については、「[システム設定 &#40;マスター データ サービス&#41;](../../master-data-services/system-settings-master-data-services.md)」を参照してください。  
  
-   [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションを作成して、このデータベースに関連付けます。 詳細については、「[マスター データ マネージャー Web アプリケーションを作成する方法 &#40;マスター データ サービス&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)」を参照してください。  
  
-   データベースとトランザクション ログをバックアップするように、メンテナンス プランを構成します。 詳細については、「[データベース要件 &#40;マスター データ サービス&#41;](../../master-data-services/install-windows/database-requirements-master-data-services.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [マスター データ サービスのインストール](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
