---
description: SQL Server Management Studio から SQL Server コンポーネントへの接続
title: SQL Server コンポーネントに接続する | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], SQL Server Management Studio
- saving connections
- components [SQL Server], connections
- SQL Server Management Studio [SQL Server], connections
ms.assetid: 5eeb41bd-b25b-4d3b-a005-a7d9e4b5978e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: 3df8294e7028573518fe349d8c490fe6b5a266d1
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92034911"
---
# <a name="connect-to-any-sql-server-component-from-sql-server-management-studio"></a>SQL Server Management Studio から SQL Server コンポーネントへの接続

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各コンポーネントを管理する機能があります。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用して、以下のコンポーネントに接続します。  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]のインスタンス。  
  
-   [https://login.microsoftonline.com/consumers/]([!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)])  
  
-   [https://login.microsoftonline.com/consumers/]([!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)])  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] では、データ ソースへの接続を確立していなくてもクエリの編集は行えますが、他のほとんどのタスクの場合には接続が必要です。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] では **[サーバーへの接続]** ダイアログ ボックスを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントへの接続プロパティを設定できます。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] の起動時には **[サーバーへの接続]** ダイアログ ボックスが表示され、サーバーへの接続を求められます。 **[サーバーへの接続]** ダイアログ ボックスには最後に使用したときの接続設定が保持されます。  
  
> [!NOTE]  
> この機能をオフにして、接続を自動的に開始しないようにすることもできます。 詳細については、「 [データベース エンジン サービスのスタートアップ オプション](../../database-engine/configure-windows/database-engine-service-startup-options.md)」を参照してください。  
  
## <a name="saving-connections"></a>接続の保存  
登録済みサーバーで特定のサーバーへの接続を保存することや、ソリューション エクスプローラーでプロジェクトの接続を保存することができます。  
  
### <a name="saving-connections-in-registered-servers"></a>登録済みサーバーでの接続の保存  
サーバーを登録すると、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] によって [登録済みサーバー] に接続情報が保存されます。 登録済みサーバーに接続するには、[登録済みサーバー] 内のサーバー名をダブルクリックします。 サーバーへの接続が行われ、オブジェクト エクスプローラーにそのサーバーが表示されます。  
  
### <a name="saving-connections-in-solution-explorer"></a>ソリューション エクスプローラーでの接続の保存  
ソリューション エクスプローラーでは、プロジェクト内に、関連するクエリ、スクリプト、接続、その他の関連情報を格納することができます。 スクリプト プロジェクトには **[接続]** というノードがあり、ここに 1 つ以上の接続を保存できます。 接続を追加するには、 **[接続]** を右クリックして、 **[新しい接続]** を選択します。 保存した接続にアクセスするには、 **[接続]** を展開して対象の接続をダブルクリックします。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] によって、その接続に関連付けられたクエリ ウィンドウが開かれます。 スクリプトを保存すると、そのスクリプトには特定の接続との関連が保持されます。  
  
## <a name="see-also"></a>参照  
[SQL Server Management Studio の使用 [SQL Server]](../sql-server-management-studio-ssms.md)  
[[オブジェクト エクスプローラー]](../../ssms/object/object-explorer.md)  
