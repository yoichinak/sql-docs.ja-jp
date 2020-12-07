---
title: 起動 Configuration Manager
description: Analytics Platform System appliance の Configuration Manager ツールを起動する手順。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: be69331ec9f9daa091035d6ef21142c4f40d6a84
ms.sourcegitcommit: 442fbe1655d629ecef273b02fae1beb2455a762e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93235169"
---
# <a name="launch-the-configuration-manager-in-analytics-platform-system"></a>Analytics Platform System の Configuration Manager を起動する
このトピックでは、Analytics Platform System appliance の **Configuration Manager** を起動する手順について説明します。  
  
## <a name="before-you-begin"></a>はじめに  
  
### <a name="prerequisites"></a>前提条件  
Analytics Platform System **Configuration Manager** は、アプライアンスドメイン管理者のみが実行できます。 このツールを実行するには、アプライアンスドメイン管理者のパスワードが必要です。 追加の APS 管理者を作成するには、「aps [ドメイン管理者 &#40;aps&#41;を作成 ](create-an-aps-domain-administrator-aps.md)する」を参照してください。  
  
## <a name="launch-the-configuration-manager-tool"></a><a name="Accessing"></a>Configuration Manager ツールを起動する  
Configuration Manager を実行するには、リモートデスクトップを使用して PDW コントロールノード ( **_PDW_region_ CTL01** ) ノードに接続し、 _appliance_domain_**\Administrator** としてログインします。 **Configuration Manager** プログラムを起動する場合は、[ **管理者として実行** ] オプションを使用して、管理者の資格情報が使用されていることを確認します。  
  
#### <a name="to-launch-from-a-browser-window"></a>ブラウザーウィンドウから起動するには  
  
1.  ブラウザーを開き、ディレクトリに移動し `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100` ます。  
  
2.  [`dwconfig.exe`] を右クリックし、 **[管理者として実行]** をクリックします。  
  
#### <a name="to-launch-from-a-command-prompt"></a>コマンドプロンプトから起動するには  
  
1.  デスクトップで [ **スタート** ] メニューを開き、[ **プログラム** ]、[ **アクセサリ** ] の順にクリックし、[ **コマンドプロンプト** ] を右クリックして、[ **管理者として実行** ] をクリックします。  
  
2.  コマンドプロンプトで、次のコマンドを入力してディレクトリを変更し `cd /d "C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100"` ます。  
  
3.  コマンド プロンプトで、「`dwconfig.exe`」と入力します。  
  
**Configuration Manager** が開始されると、左側のウィンドウに使用可能なすべての機能が表示されます。 このセクションの残りの部分では、ツールで使用できる各アクションを実行する方法について説明します。  
  
**Configuration Manager** を閉じて終了するには、画面の右下隅にある [ **終了** ] をクリックします。  
  
![アプライアンストポロジを示す [Microsoft Analytics Platform System Configuration Manager] ダイアログボックスのスクリーンショット。](./media/launch-the-configuration-manager/SQL_Server_PDW_DWConfig_ApplTop.png "SQL_Server_PDW_DWConfig_ApplTop")  
  
## <a name="see-also"></a>参照  
[管理コンソール &#40;Analytics Platform System&#41;を使用してアプライアンスを監視する ](monitor-the-appliance-by-using-the-admin-console.md)  
  
