---
description: ODBC 接続マネージャー
title: ODBC 接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.odbcconnection.f1
helpviewer_keywords:
- connections [Integration Services], ODBC
- ODBC connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], ODBC
ms.assetid: e8c77aa7-6772-485e-918e-cef9eeb18c58
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7fe63ad503b49a760823635902b3744a1ae2d85a
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "91719558"
---
# <a name="odbc-connection-manager"></a>ODBC 接続マネージャー

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  ODBC 接続マネージャーを使用すると、パッケージは Open Database Connectivity (ODBC) の仕様を使用して、さまざまなデータベース管理システムに接続できます。  
  
 ODBC 接続をパッケージに追加して接続マネージャーのプロパティを設定すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] によって接続マネージャーが作成され、パッケージの **Connections** コレクションに追加されます。 接続マネージャーは、実行時に物理 ODBC 接続として解決されます。  
  
 接続マネージャーの **ConnectionManagerType** プロパティは、 **ODBC** に設定されます。  
  
 ODBC 接続マネージャーは、次の方法で構成できます。  
  
-   ユーザーまたはシステム データ ソースの名前を参照する、接続文字列を指定します。  
  
-   接続先のサーバーを指定します。  
  
-   接続を実行時に保持するかどうかを示します。  
  
## <a name="configuration-of-the-odbc-connection-manager"></a>ODBC 接続マネージャーの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [ODBC 接続マネージャーの UI リファレンス]()  
  
 プログラムによる接続マネージャーの構成については、「 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 」と「 [プログラムによる接続の追加](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)に設定されます。  
  
## <a name="odbc-connection-manager-ui-reference"></a>ODBC 接続マネージャーの UI リファレンス
  **[ODBC の接続マネージャーの構成]** ダイアログ ボックスを使用すると、接続を ODBC データ ソースに追加できます。  
  
 ODBC 接続マネージャーの詳細については、「 [ODBC Connection Manager](../../integration-services/connection-manager/odbc-connection-manager.md)」を参照してください。  
  
### <a name="options"></a>オプション  
 **[データ接続]**  
 既存の ODBC 接続マネージャーを一覧から選択します。  
  
 **[データ接続のプロパティ]**  
 選択されている ODBC 接続マネージャーのプロパティと値を表示します。  
  
 **新規**  
 **[接続マネージャー]** ダイアログ ボックスを使用して ODBC 接続マネージャーを作成します。 このダイアログ ボックスでは、必要に応じて新しい ODBC データ ソースを作成することもできます。  
  
 **削除**  
 接続を選択し、 **[削除]** ボタンを使用して削除します。  
## <a name="see-also"></a>関連項目  
 [Integration Services &#40;SSIS&#41; の接続](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
