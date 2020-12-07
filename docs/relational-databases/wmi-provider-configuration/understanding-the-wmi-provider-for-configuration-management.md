---
title: WMI Provider for Configuration Management
description: WMI Provider for Configuration Management が WMI を使用して、SQL Server のサービス、サーバーの別名、およびクライアント/サーバーのネットワーク設定を管理する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management, operations supported
ms.assetid: 92323972-7943-4208-bbf4-050774fb6027
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8f915756b2d2e0e340c296e767738f8589fb5a5d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542796"
---
# <a name="understanding-the-wmi-provider-for-configuration-management"></a>WMI Provider for Configuration Management について
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]には、構成管理用の WMI プロバイダーが用意されています。 これにより、WMI (Windows Management Instrumentation) を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のクライアントおよびサーバーのネットワーク設定、およびサーバー別名を管理することができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス、ネットワーク設定、およびエイリアスは、コンピューターの root\Microsoft\SqlServer\ComputerManagement*nn* 名前空間の WMI オブジェクトによって表されます。 指定されたコンピューター上で WMI プロバイダーを使用して接続が確立された後、サービス、ネットワーク設定、別名は、WQL またはスクリプティング言語を使用してクエリを行うことができます。  
  
 WMI プロバイダーは、インスタンス プロバイダーです。 [WMI クラス](../../relational-databases/wmi-provider-configuration-classes/wmi-provider-for-configuration-management-classes.md)のインスタンスを提供し、次の非同期操作をサポートします。  
  
 インスタンスの取得  
 特定のクラス型インスタンスの取得です。  
  
 列挙  
 クラス型のすべてのインスタンスの列挙です。  
  
 変更  
 クラス型の特定のインスタンスの変更です。  
  
 クラスには、クラスのプロパティの変更を許可するメソッドがあります。  
  
 削除  
 クラス型の特定のインスタンスの削除です。  
  
 クエリ処理  
 フィルターに基づいたクラス型のインスタンスの列挙です。  
  
 構成管理用の WMI プロバイダーを使用した管理アプリケーションの例については、「 [Wmi provider For Configuration management での WQL およびスクリプト言語の使用](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md)」を参照してください。  
  
 WMI プロバイダーを使用した管理アプリケーションのプログラミングの詳細については、.NET Framework SDK の WMI のドキュメントを参照してください [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。  
  
## <a name="see-also"></a>参照  
 [WMI Provider for Configuration Management の使用](../../relational-databases/wmi-provider-configuration/working-with-the-wmi-provider-for-configuration-management.md)   
 [WQL およびスクリプティング言語での WMI Provider for Configuration Management の使用](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
