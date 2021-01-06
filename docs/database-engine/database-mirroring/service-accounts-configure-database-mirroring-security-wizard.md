---
title: 'セキュリティの構成ウィザード: サービス アカウント'
description: SQL Server Management Studio の [データベース ミラーリング セキュリティ構成ウィザード] の [サービス アカウント] ページについて説明します。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: database-mirroring
ms.topic: conceptual
f1_keywords:
- sql13.swb.configdbmsecurwiz.serviceaccounts.f1
ms.assetid: d58d8f93-7888-4d66-af4d-969ef6a2dbee
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e3493525e67edcaf75ca6bbe7e3f3ef087ea71c0
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/17/2020
ms.locfileid: "97641304"
---
# <a name="configure-database-mirroring-security-wizard-service-accounts"></a>データベース ミラーリング セキュリティ構成ウィザード: サービス アカウント
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Windows 認証でサーバー インスタンスが別のアカウントを使用している場合に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のサービス アカウントを指定します。 これらのサービス アカウントは、すべて (同じドメインまたは信頼関係のあるドメインの) ドメイン アカウントである必要があります。  
  
 すべてのサーバー インスタンスが同じアカウントを使用している場合、または証明書ベースの認証を使用している場合、フィールドは空のままにします。 **[完了]** をクリックするだけで、現在のウィザードのアカウントに基づいてアカウントが自動的に構成されます。  
  
> [!IMPORTANT]  
>  サーバー インスタンスのデータベース ミラーリング エンドポイントで証明書を使用するように構成されている場合は、サービス アカウント フィールドをすべて空にする必要があります。  
  
 **SQL Server Management Studio を使用してデータベース ミラーリングを構成するには**  
  
-   [Windows 認証を使用してデータベース ミラーリング セッションを確立する &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [データベース ミラーリング セキュリティ構成ウィザードの起動 &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>Options  
 **プリンシパル**  
 プリンシパル サーバー インスタンスのサービス アカウントを指定します。 ドメイン名を大文字で入力します。  
  
 *DOMAINNAME*\\*username*  
  
 **ミラー**  
 ミラー サーバー インスタンスのサービス アカウントを指定します。 ドメイン名を大文字で入力します。  
  
 *DOMAINNAME*\\*username*  
  
 **ミラーリング監視サーバー**  
 ミラーリング監視サーバー インスタンスのサービス アカウントを指定します。 ドメイン名を大文字で入力します。  
  
 *DOMAINNAME*\\*username*  
  
## <a name="see-also"></a>参照  
 [データベース プロパティ &#40;[ミラーリング] ページ&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [データベース ミラーリング モニターの起動 &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [データベース ミラーリングまたは Always On 可用性グループのログイン アカウントの設定 &#40;SQL Server&#41;](../../database-engine/database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md)  
  
  
