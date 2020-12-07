---
title: 構成管理用の WMI プロバイダーの概念
description: Microsoft 管理コンソールおよび Microsoft SQL Server Configuration Manager で SQL Server 構成マネージャーと共に使用される WMI プロバイダーについて説明します。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management
- SQL Server WMI Provider
- configuration management [WMI]
- WMI Provider for Configuration Management, about WMI Provider for Configuration Management
ms.assetid: 7e41db24-b915-4eb8-a1d6-e6948ee915b7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8a93cebef339d72a80139d079f5f14fffaa119f7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545212"
---
# <a name="wmi-provider-for-configuration-management"></a>WMI Provider for Configuration Management
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  WMI プロバイダーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理コンソール (MMC) および Configuration Manager の Configuration Manager スナップインと共に使用される、公開された層です [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 これにより、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーから要求されたレジストリ操作を処理する API 呼び出しは、統一されたインターフェイスで操作できます。また、選択された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスに対して高度な制御および操作を行えます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] WMI プロバイダーは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップによって自動的にコンパイルされる DLL ファイルおよび MOF ファイルです。  
  
 WMI プロバイダーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 次のメソッドを使用して、サービスを制御するために使用されるオブジェクトクラスのセットが含まれています。  
  
-   WQL (Windows Query Language) を埋め込むことができる VBScript、[!INCLUDE[jsprjscript](../../includes/jsprjscript-md.md)]、Perl などのスクリプト言語。  
  
-   SMO マネージド コード プログラム内の <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> オブジェクト。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] WMI プロバイダー スナップインを持つ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーまたは MMC。  
  
## <a name="using-a-script-language"></a>スクリプト言語の使用  
 スクリプト言語の使用には、次のような利点があります。  
  
-   開発環境が不要。  
  
-   スクリプト言語をサポートするファイルが幅広く利用可能。  
  
 スクリプトは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] WMI プロバイダーに加えて、その他の WMI プロバイダーでも機能することができます。 ドメイン管理者は、スクリプトを使用して、ネットワーク上の複数のコンピューターのサービスの設定、ネットワーク設定、および別名設定を行うことができます。  
  
 このセクションでは、スクリプトから構成管理用の WMI プロバイダーにアクセスする方法についてより詳細に説明します。  
  
## <a name="using-the-smo-managedcomputer-object"></a>SMO ManagedComputer オブジェクトの使用  
 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> オブジェクトは、構成管理用 WMI プロバイダーへのアクセスを提供する SMO マネージド オブジェクトです。 SMO プログラムを使用すると、<xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> オブジェクトを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス、ネットワーク設定、別名設定の表示と修正を行うことができます。 詳細については、「 [WMI プロバイダーを使用したサービスとネットワーク設定の管理](../../relational-databases/server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md)」を参照してください。  
  
## <a name="using-the-microsoft-management-console-or-sql-server-configuration-manager"></a>Microsoft 管理コンソールまたは SQL Server 構成マネージャーの使用  
 Microsoft 管理コンソール (MMC) は、スクリプティング言語またはマネージド コード プログラムではなく、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを管理するインターフェイスを提供します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理 MMC スナップインを使用して、サービスの停止や開始、およびサービス アカウントの変更を行うことができます。  
  
 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス、クライアント プロトコルとサーバー プロトコル、およびサーバー別名を管理することができます。  
  
## <a name="see-also"></a>参照  
 [WMI Provider for Configuration Management について](../../relational-databases/wmi-provider-configuration/understanding-the-wmi-provider-for-configuration-management.md)   
 [WMI Provider for Configuration Management の使用](../../relational-databases/wmi-provider-configuration/working-with-the-wmi-provider-for-configuration-management.md)   
 [WQL およびスクリプティング言語での WMI Provider for Configuration Management の使用](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
