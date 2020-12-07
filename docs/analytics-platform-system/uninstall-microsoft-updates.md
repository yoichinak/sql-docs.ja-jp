---
title: Microsoft の更新プログラムのアンインストール
description: Analytics Platform System (APS) で Microsoft 更新プログラムをアンインストールします。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: a5ebe1ee911f7500505cdbd1962d28c35461a635
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "74399467"
---
# <a name="uninstall-microsoft-updates-in-analytics-platform-system"></a>Analytics Platform System での Microsoft 更新プログラムのアンインストール
この記事では、以前にインストールされた Microsoft update を Analytics Platform System appliance にアンインストールする方法について説明します。  
  
## <a name="before-you-begin"></a>はじめに  
  
### <a name="prerequisites"></a>前提条件  
これらの手順を実行するには、次のものが必要です。  
  
-   アプライアンスを監視するために管理コンソールにアクセスするためのアクセス許可を持つ分析プラットフォームシステムログイン。  
  
-   <em> <Fabric Domain> </em> **-HST01**ノードにログインするためのファブリックドメイン管理者アカウントの情報。  
  
## <a name="to-uninstall-microsoft-updates"></a><a name="HowToUninstallMSFT"></a>Microsoft 更新プログラムをアンインストールするには  
  
1.  <em> <Fabric Domain> </em> ファブリックドメイン管理者として **-HST01**ノードにログインします。  
  
2.  WSUS のアンインストールが承認されているすべての更新プログラムをアンインストールするには、コマンドプロンプトウィンドウを開き、次のコマンドを入力します。 プレースホルダー項目 *<  >* を適切な情報に置き換えます。  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="next-steps"></a>次のステップ
詳細については、次を参照してください。
- [Microsoft Update &#40;Analytics Platform System&#41;をダウンロードして適用します ](download-and-apply-microsoft-updates.md) 
- [Analytics platform system の修正プログラム &#40;analytics Platform System&#41;を適用します ](apply-analytics-platform-system-hotfixes.md)  
- [Analytics platform system の修正プログラム &#40;Analytics Platform System&#41;をアンインストールする ](uninstall-analytics-platform-system-hotfixes.md)  
- [ソフトウェアサービス &#40;Analytics Platform System&#41;](software-servicing.md)  
  
