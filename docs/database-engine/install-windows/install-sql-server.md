---
title: SQL Server のインストール ガイド
description: SQL Server と関連コンポーネントを、インストール ウィザード、コマンド プロンプト、または Sysprep などのオプションを使用してインストールするのに役立つコンテンツのインデックスです。
ms.custom: ''
ms.date: 11/14/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- AdventureWorks sample database
- installing SQL Server, preparing to install
- installation [SQL Server]
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
author: cawrites
ms.author: chadam
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 46a83efe3efcab212d3569c5f2f32c232f1962c5
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125870"
---
# <a name="sql-server-installation-guide"></a>SQL Server のインストール ガイド

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]

この記事では、Windows に SQL Server をインストールするためのガイダンスを提供するコンテンツのインデックスです。

その他の展開シナリオは次のとおりです。

- [Linux](../../linux/sql-server-linux-setup.md)
- [Docker コンテナー](../../linux/sql-server-linux-docker-container-deployment.md)
- [Kubernetes - ビッグ データ クラスター](../../big-data-cluster/deploy-get-started.md)

[!INCLUDE[sssql15](../../includes/sssql15-md.md)] 以降、[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] は 64 ビット アプリケーションでのみ使用できるようになりました。 SQL Server の入手およびインストールの方法に関する重要な詳細情報を次に示します。

## <a name="getting-started"></a>作業の開始
  
* **エディションと機能**:SQL Server のさまざまなエディションとバージョンでサポートされている機能を確認し、ビジネス ニーズに最適な製品を決定してください。 
    - [[!INCLUDE[ss2019](../../includes/sssqlv15-md.md)]](~/sql-server/editions-and-components-of-sql-server-version-15.md).  
    - [[!INCLUDE[ss2017](../../includes/sssqlv14-md.md)]](~/sql-server/editions-and-components-of-sql-server-2017.md).  
    - [[!INCLUDE[ss2016](../../includes/sssql15-md.md)]](~/sql-server/editions-and-components-of-sql-server-2016.md).  
    - [[!INCLUDE[ss2014](../../includes/sssql14-md.md)]](https://docs.microsoft.com/previous-versions/sql/2014/getting-started/features-supported-by-the-editions-of-sql-server-2014)

*  **要件**: [SQL Server 2016、2017](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)、[SQL Server 2019](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md) または [SQL Server on Linux](../../linux/sql-server-linux-setup.md) に対するハードウェアとソフトウェアのインストール要件と、「[SQL Server のインストール計画](../../sql-server/install/planning-a-sql-server-installation.md)」に記載されているシステム構成チェック、セキュリティ上の考慮事項を確認してください。 


  
* **サンプル データベースとサンプル コード**: 
    * これらは存在しますが、既定では SQL Server セットアップの一環としてインストールされません 
    * SQL Server の Express 以外のエディションをインストールするには、「[サンプルの場所](../../samples/sql-samples-where-are.md)」を参照してください
    

## <a name="installation-media"></a>インストール メディア

[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] のダウンロード場所は、エディションによって異なります。

* **SQL Server Enterprise、Standard、Express の各エディション** は、運用環境用にライセンスされます。 Enterprise および Standard Edition のインストール メディアについては、ソフトウェア販売元に問い合わせてください。 購入に関する情報および Microsoft パートナーのディレクトリについては、[マイクロソフトのライセンス ページ](https://www.microsoft.com/licensing/product-licensing/sql-server)をご覧ください。
* [無料版 - 最新](https://www.microsoft.com/sql-server/sql-server-downloads)
* [無料版 - その他](https://www.microsoft.com/evalcenter/evaluate-sql-server)


その他の SQL Server コンポーネントはこちらにあります。 

* [すべての累積的な更新プログラム](https://sqlserverbuilds.blogspot.com/)
* [SQL Server Reporting Services](https://www.microsoft.com/download/details.aspx?id=100122)。 
* [SQL Server Management Studio](https://aka.ms/ssmsfullsetup)
* [Azure Data Studio](https://go.microsoft.com/fwlink/?linkid=2109256)


## <a name="considerations"></a>考慮事項

-   リモート デスクトップ接続で、RDC クライアントのローカル リソースのメディアを使用して、セットアップを起動した場合、インストールは失敗します。 リモートでインストールするには、メディアをネットワーク共有に配置するか、物理または仮想マシンのローカルに配置する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール メディアは、ネットワーク共有、マッピングされたドライブ、またはローカル ドライブに配置するか、仮想マシンに ISO として配置する必要があります。  
  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップを実行すると、製品に必要な以下のソフトウェア コンポーネントがインストールされます。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client    
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ サポート ファイル  

## <a name="sql-server-installation"></a>SQL Server のインストール


|[アーティクル]|説明|  
|-----------|-----------------|  
|[インストール ウィザードからの SQL Server&2016; のインストール (セットアップ)](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)|setup.exe セットアップ メディアから起動するインストール ウィザード GUI を使用して SQL Server をインストールします。 |  
|[コマンド プロンプト](./install-sql-server-from-the-command-prompt.md)|コマンド プロンプトから SQL Server インストールを実行するためのサンプルの構文とインストール パラメーター。 | 
|[Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md)|Windows Server Core に [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] をインストールします。|  
|[システム構成チェッカーの検査パラメーター](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)|システム構成チェッカー (SCC) の機能について説明します。|   
|[構成ファイル](./install-sql-server-using-a-configuration-file.md)|構成ファイルからセットアップを実行するためのサンプルの構文とインストール パラメーター。|  
|[SysPrep](../../database-engine/install-windows/install-sql-server-using-sysprep.md)|SysPrep からセットアップを実行するためのサンプルの構文とインストール パラメーター。|
|[インスタンスへの機能の追加](./add-features-to-an-instance-of-sql-server-setup.md)|[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] の既存のインスタンスのコンポーネントを更新します。|  
|[SQL Server フェールオーバー クラスターのインストール](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)| SQL Server フェールオーバー クラスター インスタンスをインストールします。  | 
|[失敗した [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] のインストールを修復する](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)|失敗した [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] のインストールを修復します。|  
|[SQL Server をホストしているコンピューターの名前を変更する](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)|SQL Server のスタンドアロン インスタンスをホストしているコンピューターのホスト名が変更された後、sys.servers に格納されているシステム メタデータを更新します。 |  
|[[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] サービス更新プログラムをインストールする](../../database-engine/install-windows/install-sql-server-servicing-updates.md)|[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] の更新プログラムをインストールします。|  
|[セットアップ ログ ファイル](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)| SQL Server セットアップ ログ ファイルのエラーを表示し、読みます。 |  
|[インストールの検証](../../database-engine/install-windows/validate-a-sql-server-installation.md)|コンピューターにインストールされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能を確認するための SQL の検出レポートの使用方法を確認します。|  
  
  
## <a name="individual-component-installation"></a>個々のコンポーネント インストール 
  
|[アーティクル]|説明|  
|-----------|-----------------|  
|[SQL Server データベース エンジン](../../database-engine/install-windows/install-sql-server-database-engine.md)|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] をインストールし、構成します。|  
|[SQL Server レプリケーション](../../database-engine/install-windows/install-sql-server-replication.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レプリケーションをインストールし、構成します。|  
|[分散再生](../../tools/distributed-replay/install-distributed-replay-overview.md)|分散再生の機能のインストールに関する記事を一覧表示します。|  
|[SQL Server 管理ツールと SSMS](../../ssms/download-sql-server-management-studio-ssms.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理ツールをインストールし、構成します。|  
|[SQL Server PowerShell](../../database-engine/install-windows/install-sql-server-powershell.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell コンポーネントのインストールに関する考慮事項。|  
  

## <a name="sql-server-configuration"></a>SQL Server の構成 
  
|[アーティクル]|説明|  
|-----------|-----------------|  
|[Windows ファイアウォールの構成 (SQL Server)](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|ファイアウォール構成の概要と、SQL Server へのアクセスを許可するように Windows ファイアウォールを構成する方法。|  
|[Windows ファイアウォールの構成 (SSAS)](/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] または [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint へのアクセスを許可するためにポートとファイアウォールの両方の設定を構成します。|  
|[マルチホーム コンピューターの構成](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|マルチホーム環境内の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにネットワーク接続できるように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] とセキュリティが強化された Windows ファイアウォールを構成します。|  

 
## <a name="see-also"></a>関連項目  

[[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] のアップグレード](../../database-engine/install-windows/upgrade-sql-server.md)   
[[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] のアンインストール](../../sql-server/install/uninstall-sql-server.md)   
[SQL Server Reporting Services (SSRS) のインストール](../../reporting-services/install-windows/install-reporting-services.md)   
[SQL Server Analysis Services (SSAS) のインストール](/analysis-services/instances/install-windows/install-analysis-services)   
[[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] のビジネス インテリジェンス機能のインストール](../../sql-server/install/install-sql-server-business-intelligence-features.md)   
[高可用性ソリューション &#40;SQL Server&#41;](../sql-server-business-continuity-dr.md)