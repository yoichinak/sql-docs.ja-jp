---
title: '[SQL Server のプロパティ] ダイアログ ボックス ([ログオン] タブ)'
description: '[SQL Server のプロパティ] ダイアログ ボックスの [ログオン] タブについて説明します。 このタブを使用して、SQL Server によって使用されるアカウントを指定し、サービスを開始または停止します。'
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 405073fc-eaa3-43c6-bf82-2cd58cacc1c3
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 63e71e0a0e4c53b77b3c1f11225f49abb250c585
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100345987"
---
# <a name="sql-server-properties-log-on-tab"></a>[SQL Server のプロパティ] ダイアログ ボックス ([ログオン] タブ)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  **[SQL Server のプロパティ]** ダイアログ ボックスの **[ログオン]** タブでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスが使用するアカウントの指定、アカウントのパスワードの変更、およびそのサービスの開始、停止を行います。 アカウントのパスワードを変更すると、その変更はすぐに有効になります。  
  
> [!NOTE]  
>  クラスター化されたインスタンス上のサービスで使用するアカウント名を変更する場合、新しいアカウントは、そのサービスのセットアップ時に指定したドメイン グループに属している必要があります。または、そのグループにメンバーを追加する権限が与えられている必要があります。 グループのメンバーシップを変更する権限がない場合は、ドメイン管理者に問い合わせてください。  
>   
>  サービスを実行するアカウントの選択の詳細については、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「Windows サービス アカウントの設定」を参照してください。  
  
## <a name="options"></a>Options  
 **[ビルトイン アカウント]**  
 **Local System**  
 -   ローカル システム アカウントを指定します。 このアカウントはパスワードを必要としません。 ただし、ローカル システム アカウントに与えられている特権によっては、そのサービスが他のサーバーと対話できないこともあります。  
  
 **Local Service**  
 -   ローカル サービス アカウントを指定します。 このアカウントはパスワードを必要としません。 ただし、ローカル サービス アカウントに与えられている特権によっては、そのサービスが他のサーバーと対話できないこともあります。  
  
 **Network Service**  
 -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスには、ネットワーク サービス アカウントを使用しないことをお勧めします。 これらのサービスには、ローカル ユーザー アカウントまたはドメイン ユーザー アカウントの方が適しています。  
  
 **[このアカウント]**  
 Windows 認証を使用するローカル ユーザー アカウントまたはドメイン ユーザー アカウントを指定します。 サービスを実行できる必要最小限の権限が設定されたドメイン ユーザー アカウントを使用することをお勧めします。  
  
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
  
> [!IMPORTANT]  
>  サービスを開始、停止、一時停止、再開、または再起動できるのは、既定ではローカル管理者グループのメンバーだけです。 管理者以外のユーザーがサービスを管理できるようにする方法については、「 [[HOWTO] Windows Server 2003 でサービスを管理する権利をユーザーに付与する](https://support.microsoft.com/kb/325349)」をご覧ください (Windows の他のバージョンでも処理は同じです)。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動時に、"実装されていません (not implemented) [0x80004001]" という語句を含む WMI エラーが発生する場合は、ターゲット コンピューターに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がインストールされていない可能性があります。  
  
  
