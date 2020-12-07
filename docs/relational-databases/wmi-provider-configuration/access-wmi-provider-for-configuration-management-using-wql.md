---
title: WQL を使用して WMI プロバイダーにアクセスする
description: この例を使用すると、SQL Server でコンピューター管理用の WMI プロバイダーの Windows Management Instrumentation クエリ言語ステートメントを実行する方法を確認できます。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
ms.assetid: 26499530-d93b-452b-bbe4-217ef1d11e68
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 27b03d13ede2b861f90e194e4939e8c9c77ecafb
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542751"
---
# <a name="access-wmi-provider-for-configuration-management-using-wql"></a>WQL を使用して構成管理の WMI プロバイダーにアクセスする
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このセクションでは、WMI Provider for Computer Management に対して [!INCLUDE[msCoName](../../includes/msconame-md.md)] WQL (Windows Management Instrumentation Query Language) ステートメントを実行する方法について説明します。  
  
 この例では、WQL エディター、WBEMtest.exe を使用して、WMI プロバイダーに対して WQL クエリを実行し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス、ネットワーク プロトコル、および別名を列挙します。  
  
### <a name="querying-services-using-wbemtest"></a>WBEMtest を使用したサービスの照会  
  
1.  [ **スタート** ] メニューの [ **実行**] をクリックし、「 **WBEMtest**」と入力します。  
  
2.  WBEMtest.exe のダイアログ ボックスが表示されます。 **[Connect]** をクリックします。  
  
3.  最初のテキスト フィールドに、WMI Provider for Computer Management の名前空間 (「root\Microsoft\SqlServer\ComputerManagement11」) を入力します。 **[Connect]** をクリックします。  
  
4.  **[クエリ]** をクリックします。 ローカルコンピューターで現在実行されているサービスを返すクエリを入力します: **SELECT \* FROM sqlservice。** **[Apply]** をクリックします。  
  
5.  **WHERE ServiceName = "MSSQLSERVER"** を追加して、クエリをさらに絞り込みます。  
  
  
