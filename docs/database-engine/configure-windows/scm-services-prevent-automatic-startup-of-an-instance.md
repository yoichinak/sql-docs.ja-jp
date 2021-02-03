---
title: SCM サービス - インスタンスの自動開始を回避する | Microsoft Docs
description: SQL Server のインスタンスが自動的に開始されないようにする方法について説明します。 このタスクを実行するために開始モードを手動に設定する方法を示します。
ms.custom: ''
ms.date: 01/06/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- automatic SQL Server startup
- SQL Server, stopping
- SQL Server, automatic startup
- canceling automatic startup
- stopping SQL Server
- preventing automatic startups [SQL Server]
ms.assetid: 782663cf-f3d7-4cc6-b621-21e4550f0322
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b103099bf785b3fb8ed44c553db6b2fad5f60b2f
ms.sourcegitcommit: b1cec968b919cfd6f4a438024bfdad00cf8e7080
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2021
ms.locfileid: "99236566"
---
# <a name="scm-services---prevent-automatic-startup-of-an-instance"></a>SCM サービス - インスタンスの自動開始を回避する
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で SQL Server 構成マネージャーを使用して、 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] のインスタンスが自動的に開始されないようにする方法について説明します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は通常、自動的に開始するように構成されます。 インスタンスの開始モードを手動に設定することによって、その構成を変更できます。  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> SQL Server 構成マネージャーの使用  
  
#### <a name="to-prevent-automatic-startup-of-an-instance-of-sql-server"></a>SQL Server のインスタンスの自動開始を回避するには  
  
1.  **[スタート]** メニューで、 **[すべてのプログラム]** 、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーは [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理コンソール プログラムのスナップインであり、スタンドアロン プログラムではないため、新しいバージョンの Windows では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーはアプリケーションとして表示されません。  
    >   
    >  -   **Windows 10**:  
    >          [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを開くには、 **スタート画面** で、「SQLServerManager13.msc」( [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)]の場合) と入力します。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の場合は、13 をより小さい数値に置き換えます。 SQLServerManager13.msc をクリックすると、構成マネージャーが開きます。 スタート画面やタスク バーに構成マネージャーをピン留めするには、SQLServerManager13.msc を右クリックして、 **[ファイルの場所を開く]** をクリックします。 エクスプローラーでは、SQLServerManager13.msc を右クリックし、 **[スタート画面にピン留め]** または **[タスクバーにピン留め]** をクリックします。  
    > -   **Windows 8**:  
    >          [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを開くには、**検索** チャームの **[アプリ]** で、「**SQLServerManager\<version>.msc**」(「**SQLServerManager13.msc**」など) と入力し、**Enter** キーを押します。  
  
2.  [SQL Server 構成マネージャー] で **[サービス]** を展開し、 **[SQL Server]** をクリックします。  
  
3.  詳細ペインで、 **[MSSQLServer]** を右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[全般]** ボックスの **[サービス]** タブの **[SQL Server \<**_instancename_**> のプロパティ]** ダイアログ ボックスで、 **[開始モード]** の値を **[手動]** に設定します。  
  
5.  **[OK]** をクリックして **[SQL Server \<**_instancename_**> のプロパティ]** ダイアログ ボックスを閉じ、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを閉じます。  
  
## <a name="see-also"></a>参照  
 [データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
