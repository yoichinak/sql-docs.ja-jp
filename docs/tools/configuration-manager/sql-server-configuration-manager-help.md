---
title: SQL Server 構成マネージャーのヘルプ
description: SQL Server 構成マネージャーについて理解します。 これを使用して SQL Server サービスの管理、およびネットワーク接続の構成を行う方法について説明します。
ms.custom: seo-lt-2019
ms.date: 02/01/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Configuration Manager, help
ms.assetid: 6e909911-39a6-469b-b22a-3afdfd08a30b
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: a881d4e40717fa943f0674d5af7c570e41bf2fcc
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88901792"
---
# <a name="sql-server-configuration-manager-help"></a>SQL Server 構成マネージャーのヘルプ
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各種サービスやネットワーク接続を構成します。 データベース オブジェクトの作成または管理、セキュリティの構成、 [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリの作成には、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ツールを使用します。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]の詳細については、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックを参照してください。  

 > [!TIP]
 > Linux で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を構成する必要がある場合は、**mssql-conf** ツールを使用します。 詳しくは、「[mssql-conf ツールを使用して SQL Server on Linux を構成する](../../linux/sql-server-linux-configure-mssql-conf.md)」をご覧ください。

 ここでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーの各ダイアログ ボックスの F1 ヘルプ トピックについて紹介します。  
  
> [!NOTE]
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーで [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] よりも前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を構成することはできません。  
  
## <a name="services"></a>サービス  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に関連する各種サービスを管理します。 これらのタスクの多くは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows の [サービス] ダイアログ ボックスからも実行できますが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーでは、管理対象のサービスに関して追加の操作を実行できます。たとえば、サービス アカウントの変更時に正しい権限を適用することなどが可能です。 また、Windows の通常の [サービス] ダイアログ ボックスから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各種サービスを構成すると、そのサービスが正しく機能しないことがあります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーでは、各種サービスに関する以下のタスクを実行できます。  
  
-   サービスの開始、停止、一時停止  
  
-   サービスの開始を自動にするか手動にするかの構成、サービスの無効化、サービスの他の設定の変更  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各種サービスが使用するアカウントのパスワードの変更  
  
-   トレース フラグ (コマンド ライン パラメーター) を使用した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の開始  
  
-   サービスのプロパティの表示  
  
## <a name="sql-server-network-configuration"></a>SQL Server のネットワーク構成  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、このコンピューター上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各種サービスに関する以下のタスクを実行できます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ネットワーク プロトコルの有効化または無効化  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ネットワーク プロトコルの構成  
  
> [!NOTE]  
>  プロトコルを構成して [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]に接続する方法に関する簡単なチュートリアルについては、「[チュートリアル:データベース エンジンの概要](../../relational-databases/tutorial-getting-started-with-the-database-engine.md)」を参照してください。  
  
## <a name="sql-server-native-client-configuration"></a>SQL Server Native Client の構成  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアントは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ネットワーク ライブラリを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、このコンピューター上のクライアント アプリケーションに関する以下のタスクを実行できます。  
  
-   このコンピューター上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアント アプリケーションに関して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに接続するときのプロトコルの順序を指定できます。  
  
-   クライアント接続プロトコルを構成できます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアント アプリケーションに関して、クライアントからカスタム接続文字列を使用して接続するための [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスの別名を作成できます。  
  
 各タスクの詳細については、各タスクに関する F1 ヘルプを参照してください。  
  
#### <a name="to-open-sql-server-configuration-manager"></a>構成マネージャーを開くには、以下の手順を実行します。  
  
-   **[スタート]** ボタンをクリックし、 **[すべてのプログラム]**、 **[Microsoft SQL Server]** (バージョン)、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。  
  
  
 **[!INCLUDE[win8](../../includes/win8-md.md)] を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーにアクセスするには**  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーは [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理コンソール プログラムのスナップインであり、スタンドアロン プログラムではありません。そのため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行している場合、 [!INCLUDE[win8](../../includes/win8-md.md)]構成マネージャーはアプリケーションとして表示されません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを開くには、**検索** チャームで、**[アプリ]** の下に「**SQLServerManager12.msc**」 ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] の場合) または「**SQLServerManager11.msc**」 ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] の場合) と入力し、**Enter** キーを押します。  
  

## <a name="see-also"></a>参照  
 [[SQL Server のサービス]](../../tools/configuration-manager/sql-server-services.md)   
 [SQL Server のネットワーク構成](../../tools/configuration-manager/sql-server-network-configuration.md)   
 [SQL Native Client 11.0 の構成](../../tools/configuration-manager/sql-native-client-11-0-configuration.md)   
 [ネットワーク プロトコルの選択](/previous-versions/sql/sql-server-2016/ms187892(v=sql.130))  
  
