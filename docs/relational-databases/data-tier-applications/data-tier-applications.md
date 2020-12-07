---
description: データ層アプリケーション
title: データ層アプリケーション | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- designing DACs
- How to [DAC]
- data-tier application [SQL Server], designing
- wizard [DAC]
ms.assetid: a04a2aba-d07a-4423-ab8a-0a31658f6317
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5b13b4fcc5fd0071a5b008f4fa8186379ffecf41
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193052"
---
# <a name="data-tier-applications"></a>データ層アプリケーション
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  データ層アプリケーション (DAC) は、テーブル、ビュー、インスタンス オブジェクト (ログインを含む) など、ユーザーのデータベースに関連付けられたすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトを定義する論理的なデータベース管理エンティティです。 DAC は、データ層の開発者とデータベース管理者が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトを DAC パッケージ (DACPAC とも呼ばれます) という移植可能なアーティファクトにパッケージ化できるようにする自己完結型の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース配置単位です。  
  
 BACPAC は、データベース スキーマおよびデータベースに格納されているデータをカプセル化する関連アーティファクトです。  
  
## <a name="benefits-of-data-tier-applications"></a>データ層アプリケーションの利点  
 ほとんどのデータベース アプリケーションのライフサイクルでは、開発者と DVA が共有および交換するスクリプトと、アプリケーションの更新およびメンテナンス アクティビティ用のアドホック統合メモが使用されます。 これは少数のデータベースでは許容されますが、データベースの数、サイズ、および複雑さが増大するとすぐにスケーラブルでなくなります。  
  
 DAC は、宣言的なデータベース開発で配置と管理を簡略化できるようにするデータベース ライフ サイクル管理および生産性ツールです。 開発者は、SQL Server Data Tools データベース プロジェクトでデータベースを作成してから、DBA に渡すためにデータベースを DACPAC に構築できます。 DBA は、SQL Server Management Studio を使用して DAC を配置して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]のテスト インスタンスまたは実稼働インスタンスをテストできます。 また、DBA は DACPAC を使用して、SQL Server Management Studio で以前に配置したデータベースをアップグレードできます。 ライフサイクルを完了するために、DBA はデータベースを DACPAC に抽出し、開発者に渡して、テストまたは実稼働の調整を反映したり、アプリケーションの変更に応じたデータベース デザインの変更を可能にしたりできます。  
  
 DAC ドリブン配置がスクリプト ドリブンの配置より優れている点は、ツールによって DBA が異なるソースおよびターゲット データベースからの動作を識別および検証できることです。 アップグレード中に、アップグレードによりデータ損失の可能性がある場合にはツールによって DBA に警告され、アップグレード計画も提供されます。 DBA は、計画を評価し、ツールを利用してアップグレードを続行できます。  
  
 DAC では、開発者と DBA がデータベースのライフサイクルにわたってデータベース系列をメンテナンスおよび管理するのに役立つバージョン管理もサポートされます。  
  
## <a name="dac-concepts"></a>DAC の概念  
 DAC を使用すると、次のような点で、アプリケーションをサポートするデータ層要素の開発、配置、および管理が容易になります。  
  
-   データ層アプリケーション (DAC) は、テーブル、ビュー、インスタンス オブジェクトなど、ユーザーのデータベースに関連付けられたすべての SQL Server オブジェクトを定義する論理的なデータベース管理エンティティです。 データ層の開発者と DBA が SQL Server オブジェクトを DAC パッケージまたは .dacpac ファイルと呼ばれる移植可能なアーティファクトにパッケージ化できるようにする自己完結型の SQL Server データベース配置単位です。  
  
-   SQL Server データベースを DAC として扱うには、ユーザー操作によって明示的に、または DAC 操作の 1 つによって暗黙的に登録する必要があります。 データベースが登録されると、DAC バージョンとその他のプロパティがデータベースのメタデータの一部として記録されます。 反対に、データベースを登録解除し、その DAC プロパティを削除することもできます。  
  
-   一般に、DAC ツールでは以前の SQL Server バージョンの DAC ツールによって生成された DACPAC ファイルを読み取ることができ、DACPAC を以前のバージョンの SQL Server に配置することもできます。 一方、以前のバージョンの DAC ツールでは、新しいバージョンの DAC ツールによって生成された DACPAC ファイルを読み取ることができません。 具体的な内容は次のとおりです。  
  
    -   DAC 操作は、SQLServer 2008 R2 で導入されました。 SQL Server 2008 R2 データベースに加えて、ツールでは SQL Server 2008、SQL Server 2005、および SQL Server 2000 データベースからの DACPAC ファイルの生成がサポートされます。  
  
    -   SQL 2016 データベースに加えて、SQL Server 2016 に付属のツールでは、SQL Server 2008 R2 または SQL Server 2012 に付属の DAC ツールで生成された DACPAC ファイルを読み取ることができます。 これには、SQL Server 2014、2012、2008 R2、2008、2005 のデータベースが含まれますが、SQL Server 2000 のデータベースは**含まれません**。  
  
    -   SQL Server 2008 R2 の DAC ツールでは、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] または  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のツールによって生成された DACPAC ファイルを読み取ることはできません。  
  
-   DACPAC は、.dacpac 拡張子を持つ Windows ファイルです。 このファイルでは、DACPAC の生成元、データベース内のオブジェクト、およびその他の特性を詳細に表す複数の XML セクションから構成されるオープン フォーマットがサポートされます。 上級ユーザーは、製品に付属の DacUnpack.exe ユーティリティを使用してファイルをパッケージ解除して、各セクションをより詳細に調査できます。  
  
-   ユーザーがデータベースを作成 (DAC パッケージを配置することによるデータベースの作成を含む) するには、**dbmanager** ロールのメンバーであるか、**CREATE DATABASE** 権限が割り当てられている必要があります。 ユーザーがデータベースを削除するには、**dbmanager** ロールのメンバーであるか、**DROP DATABASE** 権限を割り当てられている必要があります。  
  
## <a name="dac-tools"></a>DAC ツール  
 DACPAC は、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]に付属の複数のツール間でシームレスに使用できます。 これらのツールは、相互運用性の単位として DACPAC を使用して、異なるユーザーの要件に対処します。  
  
-   アプリケーション開発者:  
  
    -   SQL Server データ ツール データベース プロジェクトを使用し、データベースをデザインできます。 このプロジェクトが正常に構築されると、.dacpac ファイルに含まれる DACPAC が生成されます。  
  
    -   DACPAC をデータベース プロジェクトにインポートし、データベースのデザインを続行できます。  
  
        SQL Server データ ツールでは、接続されていないクライアント側データベース アプリケーション配置用のローカル DB もサポートされます。 開発者は、このローカル データベースのスナップショットを作成して、.dacpac ファイルに含まれる DACPAC を作成できます。  
  
    -   それとは別に、開発者は、DACPAC を生成しなくても、データベースにデータベース プロジェクトを直接パブリッシュできます。 パブリッシュ操作の後に、他のツールからの配置操作などの同様の動作が続きます。  
  
-   データベース管理者:  
  
    -   SQL Server Management Studio を使用して、既存のデータベースから DACPAC を抽出でき、その他の DAC 操作を実行することもできます。  
  
    -   また、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] の DBA の場合、DAC 操作に Azure portal を使用できます。  
  
-   独立系ソフトウェア ベンダー:  
  
    -   SQL Server のホスティング サービスおよびその他のデータ管理製品では、DAC 操作に DACFx API を使用できます。  
  
-   IT 管理者:  
  
    -   IT システム インテグレーターと管理者は、DAC 操作に SqlPackage.exe コマンド ライン ツールを使用できます。  
  
## <a name="dac-operations"></a>DAC 操作  
 DAC では、以下のオブジェクトがサポートされています。  
  
-   **EXTRACT**: ユーザーはデータベースを DACPAC に抽出できます。  
  
-   **DEPLOY**: ユーザーは DACPAC をホスト サーバーに配置できます。 配置が SQL Server Management Studio や Azure portal などの管理ツールから行われる場合、ホスト サーバーに生成されるデータベースがデータ層アプリケーションとして暗黙的に登録されます。  
  
-   **REGISTER**: ユーザーはデータベースをデータ層アプリケーションとして登録できます。  
  
-   **UNREGISTER**: DAC として既に登録されているデータベースを登録解除できます。  
  
-   **UPGRADE**: DACPAC を使用してデータベースをアップグレードできます。 アップグレードは、データ層アプリケーションとして登録されていないデータベースでもサポートされますが、アップグレードの結果として、データベースが暗黙的に登録されます。  
  
## <a name="bacpac"></a>BACPAC  
 BACPAC は .bacpac 拡張子を持つ Windows ファイルであり、データベースのスキーマとデータがカプセル化されています。 BACPAC の基本的なユース ケースは、あるサーバーから別のサーバーにデータベースを移動、または[ローカル サーバーからクラウドにデータベースを移行](/azure/azure-sql/database/migrate-to-database-from-sql-server)し、既存のデータベースをオープン フォーマットでアーカイブすることです。  
 DACPAC と同様に、BACPAC ファイル形式は公開されており、BACPAC のスキーマ コンテンツは DACPAC のスキーマ コンテンツと同じです。 BACPAC 内のデータは JSON 形式で格納されます。  
  
 DACPAC と BACPAC は似ていますが、ターゲットとするシナリオは異なります。 DACPAC は、既存のデータベースのアップグレードなど、スキーマのキャプチャと配置に重点を置きます。 DACPAC の主なユースケースは、厳密に定義されたスキーマを開発環境、テスト環境、その後運用環境に配置することです。 またその逆に、運用環境のスキーマをキャプチャし、テスト環境や開発環境に適用して戻します。  
  
 一方、BACPAC は、主に次の 2 つの操作をサポートするスキーマとデータのキャプチャに重点を置きます。  
  
-   **EXPORT**: ユーザーは、BACPAC にスキーマとデータベースのデータをエクスポートできます。  
  
-   **IMPORT**: ユーザーは、スキーマおよびデータをホスト サーバーの新しいデータベースにインポートできます。  
  
 この両方の機能が、データベース管理ツール (SQL Server Management Studio、Azure ポータル、DACFx API) でサポートされます。  
  
## <a name="permissions"></a>アクセス許可  
 データベースを作成 (DAC パッケージを配置することによるデータベースの作成を含む) するには、 **dbmanager** ロールのメンバーであるか、 **CREATE DATABASE** 権限が割り当てられている必要があります。 データベースを削除するには、 **dbmanager** ロールのメンバーであるか、 **DROP DATABASE** 権限が割り当てられている必要があります。  
  
## <a name="data-tier-application-tasks"></a>データ層アプリケーションのタスク  
  
|タスク|トピック|  
|----------------------|-----------|  
|新しい DAC インスタンスを作成するために DAC パッケージ ファイルを使用する方法について説明します。|[データ層アプリケーションの配置](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)|  
|DAC のインスタンスを新しいバージョンにアップグレードするために、新しい DAC パッケージ ファイルを使用する方法について説明します。|[データ層アプリケーションのアップグレード](../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md)|  
|DAC インスタンスを削除する方法について説明します。 関連付けられているデータベースをデタッチまたは削除するか、データベースはそのまま残すかも選択できます。|[データ層アプリケーションの削除](../../relational-databases/data-tier-applications/delete-a-data-tier-application.md)|  
|SQL Server ユーティリティを使用して、現在配置されている DAC の正常性を表示する方法について説明します。|[データ層アプリケーションの監視](../../relational-databases/data-tier-applications/monitor-data-tier-applications.md)|  
|DAC 内のデータとメタデータのアーカイブを含む .bacpac ファイルを作成する方法について説明します。|[データ層アプリケーションのエクスポート](../../relational-databases/data-tier-applications/export-a-data-tier-application.md)|  
|DAC の論理的な復元を実行したり、DAC を[!INCLUDE[ssDE](../../includes/ssde-md.md)]の他のインスタンスまたは [!INCLUDE[ssSDS](../../includes/sssds-md.md)] に移行したりするために DAC アーカイブ ファイル (.bacpac) を使用する方法について説明します。|[BACPAC ファイルのインポートによる新しいユーザー データベースの作成](../../relational-databases/data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database.md)|  
|BACPAC ファイルをインポートして、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内に新しいユーザー データベースを作成する方法について説明します。|[データベースからの DAC の抽出](../../relational-databases/data-tier-applications/extract-a-dac-from-a-database.md)|  
|既存のデータベースを DAC インスタンスに昇格させる方法について説明します。 DAC 定義はビルドされ、システム データベースに格納されます。|[データベースを DAC として登録する方法](../../relational-databases/data-tier-applications/register-a-database-as-a-dac.md)|  
|実稼働システムで DAC パッケージを使用する前に、パッケージの内容と DAC のアップグレードによって行われる動作を確認する方法について説明します。|[DAC パッケージの検証](../../relational-databases/data-tier-applications/validate-a-dac-package.md)|  
|DAC パッケージの内容をフォルダーに配置し、そのフォルダーで、DAC を実稼働サーバーに配置する前に DAC の動作内容をデータベース管理者が確認できるようにする方法について説明します。|[DAC パッケージのアンパック](../../relational-databases/data-tier-applications/unpack-a-dac-package.md)|  
|ウィザードを使用して既存のデータベースを配置する方法について説明します。 ウィザードでは DAC を使用して配置を実行します。|[DAC を使用したデータベースの配置](../../relational-databases/data-tier-applications/deploy-a-database-by-using-a-dac.md)|  
  
## <a name="see-also"></a>参照  
 [SQL Server オブジェクトとバージョンの DAC サポート](/previous-versions/sql/sql-server-2012/ee210549(v=sql.110))  
  
