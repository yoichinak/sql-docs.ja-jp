---
title: '[SQL Server Analysis Services のプロパティ] ダイアログ ボックス ([ログオン] タブ)'
description: '[分析サーバーのプロパティ] ダイアログ ボックスの [ログオン] タブについて説明します。 これを使用して SSAS サービス アカウントを指定し、サービスを開始または停止する方法を確認します。'
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: a82e0c98-efaa-4b0b-9582-3c879ee42444
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 412fb42b6756d2a574b78f5695d34e5d8c445b0c
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100349893"
---
# <a name="analysis-server-properties-log-on-tab"></a>[SQL Server Analysis Services のプロパティ] ダイアログ ボックス ([ログオン] タブ)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  **[SQL Server Analysis Services のプロパティ]** ダイアログ ボックスの **[ログオン]** タブでは、 [!INCLUDE[ssAS](../../includes/ssas-md.md)] サービスが使用するアカウントの指定や、そのサービスの開始、停止を行います。  
  
> [!NOTE]  
>  クラスター化されたインスタンス上のサービスで使用する **[アカウント名]** を変更する場合、変更後の新しいアカウントは、そのサービスのセットアップ時に指定したドメイン グループに属している必要があります。または、そのグループにメンバーを追加する権限が与えられている必要があります。 グループのメンバーシップを変更する権限がない場合は、ドメイン管理者に問い合わせてください。  
  
## <a name="options"></a>Options  
 **[ローカル システム アカウント]**  
 ローカル システム アカウントを指定します。このアカウントはパスワードを必要としません。 ただし、ローカル システム アカウントに与えられている特権によっては、そのサービスと他のサーバーとの対話が制限されることもあります。  
  
 **[このアカウント]**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 認証を使用するローカル ユーザー アカウントまたはドメイン ユーザー アカウントを指定します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、サービスを実行できる必要最小限の権限が設定されたドメイン ユーザー アカウントを使用することをお勧めします。 アカウントの選択の詳細については、オンライン ブックの「Windows サービス アカウントの設定」を検索してください。  
  
 **アカウント名**  
 ローカル ユーザー アカウント名またはドメイン ユーザー アカウント名を指定します。  
  
 **パスワード**  
 アカウントのパスワードを入力します。  
  
 **[パスワードの確認入力]**  
 アカウントのパスワードを再度入力します。  
  
 **Start**  
 サービスを開始します。  
  
 **Stop**  
 サービスを停止します。  
  
 **[一時停止]**  
 サービスを一時停止します。  
  
 **[再開]**  
 一時停止したサービスを再開します。  
  
  
