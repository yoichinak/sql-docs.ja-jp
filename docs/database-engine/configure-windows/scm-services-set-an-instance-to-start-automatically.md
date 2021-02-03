---
title: SCM サービス - インスタンスを自動的に起動するように設定する | Microsoft Docs
description: SQL Server のインスタンスを自動的に起動するように設定する方法について説明します。 既定の構成について説明するとともに、開始モードを [自動] に設定する方法を説明します。
ms.custom: ''
ms.date: 01/06/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- automatic SQL Server startup
- SQL Server, automatic startup
- starting SQL Server, automatically
ms.assetid: aa2b6bde-e76d-4fea-a560-54a63745d9b1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c1f39d69ade90ef871ec6db1d5e0b135a45799fe
ms.sourcegitcommit: b1cec968b919cfd6f4a438024bfdad00cf8e7080
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2021
ms.locfileid: "99236555"
---
# <a name="scm-services---set-an-instance-to-start-automatically"></a>SCM サービス - インスタンスを自動的に起動するように設定する
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で SQL Server 構成マネージャーを使用して、 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] のインスタンスを自動的に開始するように設定する方法について説明します。 セットアップのとき、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は通常、自動的に開始するように構成されます。 手動で開始するように構成した場合、この設定をいつでも変更できます。  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> SQL Server 構成マネージャーの使用  
  
#### <a name="to-set-an-instance-of-sql-server-to-start-automatically"></a>SQL Server のインスタンスを自動的に起動するように設定するには  
  
1.  **[スタート]** メニューで、 **[すべてのプログラム]** 、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーは [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理コンソール プログラムのスナップインであり、スタンドアロン プログラムではないため、新しいバージョンの Windows では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーはアプリケーションとして表示されません。  
    >   
    >  -   **Windows 10**:  
    >          [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを開くには、 **スタート画面** で、「SQLServerManager13.msc」( [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)]の場合) と入力します。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の場合は、13 をより小さい数値に置き換えます。 SQLServerManager13.msc をクリックすると、構成マネージャーが開きます。 スタート画面やタスク バーに構成マネージャーをピン留めするには、SQLServerManager13.msc を右クリックして、 **[ファイルの場所を開く]** をクリックします。 エクスプローラーでは、SQLServerManager13.msc を右クリックし、 **[スタート画面にピン留め]** または **[タスクバーにピン留め]** をクリックします。  
    > -   **Windows 8**:  
    >          [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを開くには、**検索** チャームの **[アプリ]** で、「**SQLServerManager\<version>.msc**」(「**SQLServerManager13.msc**」など) と入力し、**Enter** キーを押します。  
  
2.  **[SQL Server 構成マネージャー]** で **[サービス]** を展開し、 **[SQL Server]** をクリックします。  
  
3.  詳細ペインで、自動的に開始するインスタンスの名前を右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[SQL Server \<**_instancename_**> のプロパティ]** ダイアログ ボックスで、 **[開始モード]** を **[自動]** に設定します。  
  
5.  **[OK]** をクリックして [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを閉じます。  
  
## <a name="see-also"></a>参照  
 [SQL Server のインスタンスの自動開始の回避 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/scm-services-prevent-automatic-startup-of-an-instance.md)   
 [別のコンピューターへの接続 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/scm-services-connect-to-another-computer.md)   
 [SQL Server ツールでサーバーの状態を表示できるようにする WMI の構成](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  
