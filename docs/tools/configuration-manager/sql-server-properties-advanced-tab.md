---
title: '[SQL Server のプロパティ] ダイアログ ボックス ([詳細設定] タブ)'
description: データ パス、インスタンス ID、カスタム プロパティなど、[SQL Server のプロパティ] ダイアログ ボックスの [詳細設定] タブのオプションについて説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 2ffd10fd-bac1-478f-9cff-96ed6c8b787f
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 2acca0bd84985700395cb3d073e6476167577b68
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88901175"
---
# <a name="sql-server-properties-advanced-tab"></a>[SQL Server のプロパティ] ダイアログ ボックス ([詳細設定] タブ)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  **[詳細設定]** タブには、以下のプロパティが既定で表示されます。 カスタム プロパティが定義されていれば、そのプロパティと値もこのタブに表示されます。  
  
## <a name="options"></a>Options  
 **クラスター化インデックス**  
 このサービスがクラスター サーバーのリソースとしてインストールされているかどうかが表示されます。  
  
 **[カスタマー フィードバック レポート]**  
 サービス品質の監視がこのサービスで有効になっているかどうかを示します。 カスタマー フィードバック報告の詳細については、オンライン ブックの「エラー レポートと使用状況レポートの設定」を検索してください。  
  
 **[データ パス]**  
 このインストールの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]バイナリへのパスが表示されます。  
  
 **[ダンプ ディレクトリ]**  
 エラー発生時にメモリ ダンプが配置される場所が表示されます。  
  
 **[エラー報告]**  
 **[はい]** に設定した場合、重大な障害が発生したときに、ワトソン博士プログラムによって [!INCLUDE[msCoName](../../includes/msconame-md.md)] またはエラー サーバーに情報が転送されます。 エラー報告の詳細については、オンライン ブックの「エラー レポートと使用状況レポートの設定」を検索してください。 この値を変更するには、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] オブジェクト エクスプローラーでサーバーを右クリックし、 **[プロパティ]** をクリックし、 **[その他のサーバーの設定]** ページをクリックします。 **[エラー報告]** 領域にオプションが表示されます。  
  
 **ファイル バージョン**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 実行可能ファイルのバージョンが表示されます。  
  
 **インストール パス**  
 このインストールの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]バイナリへのパスが表示されます。  
  
 **インスタンス ID**  
 このサービスを使用した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスが表示されます。  
  
 **Language**  
 サーバー メッセージの既定の言語が表示されます。  
  
 **[レジストリ ルート]**  
 このアプリケーションが使用するレジストリ キーの場所が表示されます。  
  
 **[Service Pack のレベル]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のこのインスタンスのサービス パック レベルが表示されます。  
  
 **[SKU 名]**  
 製品の SKU (Stock Keeping Unit、製品のエディションとも呼ばれます) が表示されます。  
  
 **起動時のパラメーター**  
 この [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスが使用する起動時のパラメーターが一覧表示されます。 各パラメーターはセミコロンで区切られます。 既定のパラメーターには、master データベースのデータ ファイル (`master.mdf`) のパス、master データベースのログ ファイル (`mastlog.ldf`) のパス、エラー ログ ファイルのパスが含まれます。 起動時のパラメーターの構文については、オンライン ブックの **「SQL Server サービスのスタートアップ オプションの使用」** を検索してください。  
  
 **[SKU (Stock Keeping Unit)]**  
 製品の SKU (Stock Keeping Unit) 番号が表示されます。  
  
 **Version**  
 この [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスのバージョン番号が表示されます。  
  
 **[仮想サーバー名]**  
 **がクラスター サーバーにインストールされている場合の** 仮想サーバー名 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] です。  
  
  
