---
title: レポート サーバー Windows サービス (MSSQLServer) 107 | Microsoft Docs
description: 'このエラー リファレンス ページでは、イベント ID 107: "Report Server Windows Service (SQL Server) cannot connect to the report server database" (レポート サーバー Windows サービス (SQL Server) はレポート サーバー データベースに接続できません) について説明します。'
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
helpviewer_keywords:
- MSSQLServer 107 error
ms.assetid: 52b5704b-27f9-400a-a821-d8fa0786afe4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4e68ffa14bfe98bc55e5424abe0dbdac944950a1
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91933706"
---
# <a name="report-server-windows-service-mssqlserver-107"></a>レポート サーバー Windows サービス (MSSQLServer) 107
    
## <a name="details"></a>詳細  
  
|カテゴリ|値|  
|-|-|  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|107|  
|イベント ソース|レポート サーバー Windows サービス|  
|コンポーネント|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|メッセージ テキスト|レポート サーバー Windows サービス (MSSQLSERVER) はレポート サーバー データベースに接続できません。|  
  
## <a name="explanation"></a>説明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レポート サーバー サービスは、レポート サーバー データベースに接続できません。 このエラーは、サービスの再起動中、レポート サーバー データベースへの接続を確立できない場合に発生します。 このエラーは、次のような状況で発生します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] サービスが実行されていない場合。  
  
-   リモート接続または TCP/IP プロトコルが無効になっているため、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] サービスへの接続に失敗する場合。  
  
-   レポート サーバー データベースが正しく構成されていない場合。  
  
-   サービス アカウントが正しく構成されていないか、レポート サーバー データベースに対する権限がアカウントにない場合。 この状況は、アカウントやレポート サーバー データベースの設定に [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用しない場合に発生することがあります。  
  
## <a name="user-action"></a>ユーザーの操作  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] サービスが実行されていない場合はこのサービスを開始し、TCP/IP プロトコルでのリモート接続が有効になっていることを確認します。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用して、レポート サーバー データベースとサービス アカウントを構成します。  
  
## <a name="internal-only"></a>内部使用のみ  
  
## <a name="see-also"></a>参照  

 [レポート サーバー サービス アカウントの構成 (レポート サーバー構成マネージャー)](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [レポート サーバー構成マネージャー (ネイティブ モード)](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   

 [レポート サーバー サービスの開始と停止](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)  
  
  
