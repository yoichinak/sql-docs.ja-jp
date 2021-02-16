---
title: 'セキュリティの構成ウィザード: サーバーの選択'
description: データベース ミラーリング セキュリティ構成ウィザードの [サーバーの選択] ページにあるプロパティについて説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: database-mirroring
ms.topic: conceptual
f1_keywords:
- sql13.swb.configdbmsecurwiz.choosesrvrs.f1
ms.assetid: 59e23ff3-d7ee-4e32-9629-0b54d3a258f7
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c2561f81c55ca387f8038ca8ab10f82ea6fce704
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100350708"
---
# <a name="configure-database-mirroring-wizard-choose-servers-to-configure"></a>データベース ミラーリング構成ウィザード: 構成するサーバーを選択する 
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このページを使用すると、構成するサーバー インスタンスを指定できます。 ウィザードを進めるには、少なくとも 1 つのサーバー インスタンスを選択する必要があります。  
  
 サーバー インスタンスのチェック ボックスをオフにすると、このウィザードでは、そのサーバーを変更できなくなります。 ただし、他のサーバー インスタンスの構成の一部としてこのインスタンスの情報を入力し、保存するように求められます。 たとえば、ミラーリング監視サーバー インスタンスのチェック ボックスをオフにした場合でも、ミラーリング監視サーバーの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントを入力するように求められます。これは、プリンシパル サーバー インスタンスおよびミラー サーバー インスタンスに保存するセキュリティ構成の中で、このアカウントのログインを作成する必要があるためです。  
  
 **SQL Server Management Studio を使用してデータベース ミラーリングを構成するには**  
  
-   [Windows 認証を使用してデータベース ミラーリング セッションを確立する &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [データベース ミラーリング セキュリティ構成ウィザードの起動 &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>Options  
 **[プリンシパル サーバー インスタンス]**  
 プリンシパル サーバーのセキュリティを構成する場合に選択します。  
  
 **[ミラー サーバー インスタンス]**  
 ミラー サーバーのセキュリティを構成する場合に選択します。  
  
 **[ミラーリング監視サーバー インスタンス]**  
 ミラーリング監視サーバー (存在する場合) のセキュリティを構成する場合に選択します。  
  
## <a name="see-also"></a>参照  
 [データベース プロパティ &#40;[ミラーリング] ページ&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
