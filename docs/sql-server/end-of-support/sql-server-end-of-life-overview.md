---
title: サポート終了のオプション
description: SQL Server 2005、SQL Server 2008、SQL Server 2008 R2 など、サポート終了に達した SQL Server 製品で使用できるさまざまなオプションについて学習します。
ms.date: 08/12/2020
ms.prod: sql
ms.technology: install
ms.topic: conceptual
author: cawrites
ms.author: chadam
ms.reviewer: pmasl
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: e465f1e4e8c6cc9e5effb27c1cc97ee7633309eb
ms.sourcegitcommit: ece151df14dc2610d96cd0d40b370a4653796d74
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "96297969"
---
# <a name="sql-server-end-of-support-options"></a>SQL Server のサポート終了オプション 
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

この記事では、サポート終了に達した SQL Server 製品に対処するためのオプションについて説明します。

## <a name="understanding-the-sql-server-lifecycle"></a>SQL Server のライフサイクルについて

各バージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、少なくとも 10 年間のサポートが受けられます。これには、メインストリーム サポートの 5 年間、および延長サポートの 5 年間が含まれます。
-  **メインストリーム サポート** には、機能、パフォーマンス、スケーラビリティ、およびセキュリティ更新プログラムが含まれています。 
-  **延長サポート** には、セキュリティ更新プログラムのみが含まれます。 

**サポートの終了** (有効期間の終了とも呼ばれます) は、製品がそのライフサイクルの終了に達したことと、製品でサービスとサポートを利用できなくなったことを示します。 Microsoft ライフサイクルの詳細については、「[Microsoft ライフサイクル ポリシー](https://support.microsoft.com/hub/4095338/microsoft-lifecycle-policy)」を参照してください。



## <a name="options"></a>Options

ご利用の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がサポートの終了段階に達したら、次のいずれかを選択できます。
- 現在のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にアップグレードする。
- [延長セキュリティ更新プログラムのサブスクリプション](https://www.microsoft.com/cloud-platform/extended-security-updates)を購入する。 
- [無料の延長セキュリティ更新プログラム](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-2008-eos-extend-support)を取得するため、ワークロードをそのまま Azure 仮想マシンに移行する。
- [Azure SQL Database サービス](/azure/sql-database/sql-database-paas-vs-sql-server-iaas)にワークロードを移行する。 

アップグレードまたは移行の計画と自動化を行うための情報、ガイダンス、ツールの詳細については、[SQL Server 2005 のサポート終了](https://www.microsoft.com/sql-server/sql-server-2005)と [SQL Server 2008 のサポート終了](https://www.microsoft.com/cloud-platform/windows-sql-server-2008)に関するページをご覧ください。  

![サポート終了のオプション](media/sql-server-end-of-life-overview/sql-server-upgrade-paths.png)

この記事では、各アプローチの利点と考慮事項、および意思決定プロセスの指針として役立つ追加のリソースについて説明します。

## <a name="upgrade-sql-server"></a>SQL Server をアップグレードする

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がサポート終了に達したら、新しいサポート対象バージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にアップグレードすることを選択できます。 これにより、環境の一貫性が保たれ、最新の機能セットを使用できるようになり、新しいバージョンのサポート ライフサイクルが採用されます。

### <a name="benefits"></a>メリット
- **最新のテクノロジ**:新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バージョンでは、パフォーマンス、スケーラビリティ、高可用性機能、および強化されたセキュリティを含むイノベーションが導入されています。 
- **制御**:ハードウェアとソフトウェアの両方を管理するため、機能とスケーラビリティを最大限制御できます。
- **使い慣れた環境**:以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からアップグレードする場合、これが最も類似した環境になります。
- **広範な適用性**:OLTP システムやデータ ウェアハウスなど、あらゆる種類のデータベース アプリケーションに適用されます。
- **データベース アプリケーションのリスクが低い**:レガシ システムと同じレベルでデータベース互換性を維持することにより、既存のデータベース アプリケーションは、悪影響を及ぼす可能性のある機能やパフォーマンスの変更から保護されます。 新しいデータベース互換性設定でゲートされた機能を使用する必要がある場合にのみ、アプリケーションを完全に再認定する必要があります。 詳細については、「[Compatibility Certification](../../database-engine/install-windows/compatibility-certification.md)」 (互換性証明書) を参照してください。

### <a name="considerations"></a>考慮事項

- **コスト**: このアプローチでは、最大の先行投資と最も継続的な管理が必要です。 独自のハードウェアとソフトウェアを購入、保守、管理する必要があります。
- **ダウンタイム**:アップグレード戦略によっては、ダウンタイムが発生する可能性があります。 また、インプレース アップグレード プロセス中に問題が発生するという固有のリスクもあります。
- **複雑さ**:Windows Server 2008 または [!INCLUDE[winserver2008r2-md](../../includes/winserver2008r2-md.md)] を使用している場合は、新しいバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がこれらの Windows バージョンでサポートされない可能性があるため、OS もアップグレードする必要があります。 OS のアップグレード プロセス中はリスクが増えるため、サイドバイサイド移行を行うのがより賢明ですが、このアプローチにはよりコストがかかる可能性があります。 Windows Server 2008 や [!INCLUDE[winserver2008r2-md](../../includes/winserver2008r2-md.md)] のフェールオーバー クラスター インスタンスでは、インプレース OS アップグレードはサポートされていません。 

  > [!NOTE]
  > クラスター OS のローリング アップグレードは、Windows Server 2016 以降で利用できます。

### <a name="resources"></a>リソース

[インストール メディア](https://www.microsoft.com/evalcenter/evaluate-sql-server-2017-rtm)   
[インストール ウィザードを使用して SQL Server をアップグレードする](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

新機能:
- [SQL Server 2016](../what-s-new-in-sql-server-2016.md)
- [SQL Server 2017](../what-s-new-in-sql-server-2017.md) 
- [SQL Server 2019](../what-s-new-in-sql-server-ver15.md)   

ハードウェア要件:
- [SQL Server 2017 以前](../install/hardware-and-software-requirements-for-installing-sql-server.md)  
- [SQL Server 2019](../install/hardware-and-software-requirements-for-installing-sql-server-ver15.md)    

サポートされているバージョンとエディションのアップグレード:
- [SQL Server 2016](../../database-engine/install-windows/supported-version-and-edition-upgrades.md?view=sql-server-2016&preserve-view=true) 
- [SQL Server 2017](../../database-engine/install-windows/supported-version-and-edition-upgrades-2017.md)
- [SQL Server 2019](../../database-engine/install-windows/supported-version-and-edition-upgrades-version-15.md)

ツール:
-  [Database Experimentation Assistant](../../dea/database-experimentation-assistant-overview.md) は、特定のワークロードのターゲット バージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を評価するのに役立ちます。 
-  [Data Migration Assistant](../../dma/dma-overview.md) は、新しいバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータベース機能に影響する可能性のある互換性の問題を検出するのに役立ちます。 
-  [クエリ調整アシスタント](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)は、データベースの互換性をアップグレードするときに悪影響が及ぶ可能性があるワークロードの調整に役立ちます。

次の図は、数年にわたるさまざまなバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のイノベーションの例を示しています。 

![25 年間の SQL Server イノベーション](media/sql-server-end-of-life-overview/sql-server-version-improvements.png)

## <a name="extend-support"></a>サポートを延長する 

アップグレードの準備ができておらず、クラウドに移行する準備ができていない場合は、延長セキュリティ更新プログラムのサブスクリプションを購入して、サポート終了日を過ぎてから最長 3 年間は **重要な** セキュリティ更新プログラムを受け取ることができます。  

### <a name="benefits"></a>メリット 

- **アプリケーションのサポート**:これは、アプリケーションで新しいバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に対する再認定が必要な場合に最適なオプションです。 [互換性証明書](../../database-engine/install-windows/compatibility-certification.md)を使用しないアプリケーションでは、これが一般的です。 
- **一貫したインフラストラクチャ**:インフラストラクチャを変更する必要はまったくありません。 
- **テクニカル サポート**:ソフトウェア アシュアランス、または別のサポート プランをお持ちの場合は、サポートが終了した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 製品に対する [!INCLUDE[msCoName](../../includes/msconame-md.md)] からのテクニカル サポートを引き続き受けることができます。 これが、[!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] と [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] のサポートを受ける唯一の方法です。 
- **Time**: このオプションは 3 年間利用でき、アプリケーションを認定するための時間を増やすことができます。 

### <a name="considerations"></a>考慮事項 

- **限られた可用性**:このオプションは、ソフトウェア アシュアランスまたはサブスクリプションのライセンスをお持ちのお客様のみご利用いただけます。 
- **コスト**: 延長セキュリティ更新プログラムはオンプレミス ライセンスの年次コストの約 75% であるため、このオプションではコストが高くなることがあります。
- **限られた期間**:このオプションを利用できるのは 3 年間のみであるため、セキュリティとコンプライアンスを確保する必要がある場合は、3 年の期間が終わるときに引き続きアップグレードまたは移行する必要があります。
- **バグの修正プログラムがない**:製品でセキュリティ以外のバグが発生した場合、[!INCLUDE[msCoName](../../includes/msconame-md.md)] ではそのための修正プログラムはリリースされません。 
- **制限付きサポート**:延長セキュリティ更新プログラムには、新機能、機能強化、お客様のご要望による修正プログラムは含まれません。 セキュリティ修正プログラムは、[Microsoft Security Response Center (MSRC)](https://portal.msrc.microsoft.com/) によって重要として評価されたものに限定されます。

### <a name="resources"></a>リソース

[延長セキュリティ更新プログラム (ESU) の概要](sql-server-extended-security-updates.md)       
[ESU に関してよく寄せられる質問の詳細](https://www.microsoft.com/cloud-platform/extended-security-updates)       
[Azure VM にそのまま移行することによる無料のサポート延長](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-2008-eos-extend-support)       
[ソフトウェア アシュアランス](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default)       

## <a name="azure-virtual-machine"></a>Azure Virtual Machine

別の方法として、[SQL Server を実行している Azure 仮想マシン](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview)にワークロードを移行することもできます。 システムをそのまま移行し、サポートが終了した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を維持するか、新しいバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にアップグレードすることができます。 これは、OS レベルのアクセスを必要とする移行とアプリケーションに最適です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 仮想マシンは、最小限の変更または変更なしでクラウドに迅速に移行する必要がある既存のアプリケーションに対して、リフトアンドシフトの準備ができています。 

### <a name="benefits"></a>メリット

- **無料の延長セキュリティ更新プログラム**:[!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] または [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をそのまま維持することを選択した場合は、ソフトウェア アシュアランスがなくても、サポート終了日を過ぎてから 3 年間は無料の延長セキュリティ更新プログラムを取得できます。 
- **コストの節約**:ハードウェアとサーバー ソフトウェアのコストを節約でき、時間単位の使用量に対してのみ料金をお支払いいただけます。 
- **リフト アンド シフト**:最小限の変更または変更なしで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] とアプリケーションのインフラストラクチャをクラウドにリフト アンド シフトすることができます。 
- **ホスト環境**:ハードウェア、およびソフトウェア メンテナンスのオフロードなど、ホスト環境の利点が得られます。 
- **オートメーション**:[!INCLUDE[winserver2008r2-md](../../includes/winserver2008r2-md.md)] 以上をご利用の場合は、修正プログラムの自動適用と自動バックアップの利点が得られます。 
- **OS の制御**:オペレーティング システム環境を制御できますが、その場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の使い慣れた機能セットを使用します。 
- **迅速なデプロイ**:仮想マシン イメージのライブラリからすばやくデプロイすることができます。 
- **ライセンス モビリティ**:ライセンスを持ち込むことができるため、運用コストを削減できます。 
- **高可用性**: 最大 99.99% の稼働率を誇る Azure インフラストラクチャによる組み込みの仮想マシン可用性からの利点が得られるだけでなく、フェールオーバー クラスター インスタンスや Always On 可用性グループなどの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 高可用性オプションを利用することもできます。 
- **データベース アプリケーションのリスクが低い**:レガシ データベースと同じレベルでデータベース互換性を維持することにより、既存のデータベース アプリケーションは、悪影響を及ぼす可能性のある機能やパフォーマンスの変更から保護されます。 新しいデータベース互換性設定でゲートされた機能を使用する必要がある場合にのみ、アプリケーションを完全に再認定する必要があります。 詳細については、「[Compatibility Certification](../../database-engine/install-windows/compatibility-certification.md)」 (互換性証明書) を参照してください。

### <a name="considerations"></a>考慮事項

- **管理性**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] とオペレーティング システム ソフトウェアの両方を引き続き管理する必要があります。 
- **ネットワーク**:ネットワークおよび Active Directory インフラストラクチャと統合するように仮想マシンを構成する必要があります。これにより、複雑さが増します。 
- **共有記憶域の FCI**:Azure 仮想マシンでは、記憶域スペース ダイレクトまたは Premium ファイル共有を使用するフェールオーバー クラスター インスタンスのみがサポートされており、共有記憶域を使用するフェールオーバー クラスター インスタンスはサポートされていません。 そのため、Azure 仮想マシンでは、Windows Server 2012 以上を使用する場合にのみ、フェールオーバー クラスター インスタンスがサポートされます。
- **スケーラビリティのダウンタイム**:CPU およびストレージ リソースの変更中にダウンタイムが発生します。 
- **サイズの制限**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスでは、必要な数のデータベースをサポートできますが、オンプレミスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では 524 PB であるのに対し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の単一インスタンスのすべてのデータベースの累計は 256 TB となります。 

### <a name="resources"></a>リソース

[SQL Server VM の概要](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview)       
[Azure SQL オプションの選択](/azure/sql-database/sql-database-paas-vs-sql-server-iaas)       
[SQL Server を Azure VM に移行する](/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)       
[Azure にそのまま移行するための無料の延長セキュリティ更新プログラム (ESU)](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-2008-eos-extend-support)       
[延長セキュリティ更新プログラム (ESU) の概要](sql-server-extended-security-updates.md)       
[ESU に関してよく寄せられる質問の詳細](https://www.microsoft.com/cloud-platform/extended-security-updates)       
[SQL 仮想マシンの自動修正](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-patching)       
[SQL 仮想マシンの自動バックアップ](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-backup-v2)       
[SQL 仮想マシンの高可用性](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr)       
[SQL 仮想マシンに関してよく寄せられる質問](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-faq)       

## <a name="azure-sql-database-single-database"></a>Azure SQL Database 単一データベース

メンテナンスをオフロードし、コストを削減し、今後アップグレードする必要がないようにする場合は、ワークロードを [Azure SQL Database 単一データベース](/azure/sql-database/sql-database-single-database)に移動できます。 このオプションは、最新のクラウド アプリケーションで、最新の安定した [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 機能を使用する必要があり、開発とマーケティングに時間の制約がある場合に最適です。 

### <a name="benefits"></a>メリット

- **コスト**: 単一データベースは、ハードウェア、ソフトウェア、およびメンテナンスがオフロードされるため、コスト効率に優れ、秒単位または時間単位の使用量に対して料金をお支払いいただけます。 
- **柔軟性**: 単一データベースは、開発者の生産性およびソリューションの迅速な市場投入が重要になる場合や、外部アクセスを必要とする場合に、クラウド用に設計されたアプリケーションに特に適しています。  
- **一般的な機能**:最もよく使用される [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] の機能をご利用いただけますが、SQL Managed Instance の場合ほど多くはありません。  
- **迅速なデプロイ**:単一データベースをすばやくデプロイできます。 
- **スケーラビリティ**:ビジネスに合わせ、必要に応じて迅速かつ簡単にスケール アップおよびダウンできるため、コストをさらに節約できるという利点が得られます。 
- **稼働率**:サービスのコストには、ストレージと高可用性の両方が含まれ、99.995% の稼働率が保証されます。  
- **オートメーション**:修正プログラムの適用とバックアップが自動的に行われ、貴重なメンテナンス時間が節約されます。  
- **Intelligent Insights**:組み込みのインテリジェンス分析によって、データベースのパフォーマンスに関する分析情報を得ることができます。  
- **バージョンレス**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] はバージョンレスです。これは、バージョンが常に最新であり、アップグレードやダウンタイムについて心配する必要がまったくないことを意味します。 さらに、最初にクラウドに最新の安定した機能がリリースされるようになっているため、常に最新かつ最高のものを利用できます。
- **データベース アプリケーションのリスクが低い**:オンプレミス データベースと同じレベルでデータベース互換性を維持することにより、既存のアプリケーションは、悪影響を及ぼす可能性のある機能やパフォーマンスの変更から保護されます。 新しいデータベース互換性設定でゲートされた機能を使用する必要がある場合にのみ、アプリケーションを完全に再認定する必要があります。 詳細については、「[Compatibility Certification](../../database-engine/install-windows/compatibility-certification.md)」 (互換性証明書) を参照してください。

### <a name="considerations"></a>考慮事項

- **限定された移行オプション**:インスタンス全体ではなく、一度に単一のデータベースのみを移行できます。   
- **機能の制限**:最もよく使用される Azure SQL Database の機能を利用できますが、単一データベースの機能セットは、Azure SQL Managed Instance、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の場合ほど完全ではありません。 
- **Transact-SQL の相違点**:単一データベースとオンプレミスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、[!INCLUDE[tsql](../../includes/tsql-md.md)] (T-SQL) の違いがいくつかあります。 
- **サイズの制限**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のサイズが 524 PB であるのに対し、単一データベースの最大データベース サイズは 100 TB となります。 
- **メンテナンス時間**:正確なメンテナンス時間は保証されませんが、ほぼ透過的です。 

### <a name="resources"></a>リソース

[Azure SQL Database の概要](/azure/sql-database/sql-database-technical-overview)       
[Azure SQL オプションの選択](/azure/sql-database/sql-database-paas-vs-sql-server-iaas)       
[SQL Database 機能の比較](/azure/sql-database/sql-database-features)       
[SQL Server を単一データベースに移行する](/azure/sql-database/sql-database-single-database-migrate)       
[より広範な移行プロセス](/azure/cloud-adoption-framework/migrate/expanded-scope/sql-migration)       
[単一データベースの T-SQL の相違点](/azure/sql-database/sql-database-transact-sql-information)       
[仮想コア](/azure/sql-database/sql-database-vcore-resource-limits-single-databases)および [DTU](/azure/sql-database/sql-database-dtu-resource-limits-single-databases) リソースの制限       
[Intelligent Insights](/azure/sql-database/sql-database-intelligent-insights)       

ツール:
- [Data Migration Assistant](../../dma/dma-overview.md)
- [Database Migration Service](/azure/dms/dms-overview)

## <a name="sql-managed-instance"></a>SQL Managed Instance

メンテナンスとコストのオフロードを活用したいが、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] の単一データベースの機能セットの制限が多すぎると思われる場合は、[SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) に移動できます。 マネージド インスタンスは、オンプレミスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によく似ており、ハードウェア障害や修正プログラムの適用を心配する必要はありません。 マネージド インスタンスは、リフト アンド シフトの準備ができている、共有リソース セットを含むシステムおよびユーザー データベースのコレクションであり、クラウドへのほとんどの移行に使用できます。 このオプションは、最新の安定した [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 機能を使用する必要があり、最小限の変更でクラウドに移行する新しいアプリケーションまたは既存のオンプレミス アプリケーションに最適です。 

### <a name="benefits"></a>メリット

- **コスト**: ソフトウェアとハードウェアのメンテナンスをオフロードすることで、コストを節約できます。  
- **リフト アンド シフト**:データベースの変更が発生しないか最小限に抑えられるすべてのデータベースを含め、オンプレミスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス全体をマネージド インスタンスにリフト アンド シフトすることができます。 
- **機能**: マネージド インスタンスの機能セットは、データベース間のクエリ、トランザクション レプリケーションのパブリッシングとディストリビューション、SQL ジョブのスケジュール設定、CLR サポートなど、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のオンプレミス インスタンスのものとよく似ています。 
- **スケーラビリティ**:マネージド インスタンス内のすべてのデータベースでリソースが共有され、ダウンタイムなしでいつでもスケールアップおよびスケールダウンすることができます。   
- **オートメーション**:修正プログラムの適用とバックアップが自動的に行われ、貴重なメンテナンス時間が節約されます。  
- **稼働率**:サービスのコストには、ストレージと高可用性の両方が含まれ、99.99% の稼働率が保証されます。  
- **Intelligent Insights**:組み込みのインテリジェンス分析によって、データベースのパフォーマンスに関する分析情報を得ることができます。  
- **バージョンレス**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] はバージョンレスです。これは、バージョンが常に最新であり、アップグレードやダウンタイムについて心配する必要がまったくないことを意味します。 さらに、最初にクラウドに最新の安定した機能がリリースされるようになっているため、常に最新かつ最高のものを利用できます。
- **データベース アプリケーションのリスクが低い**:オンプレミス データベースと同じレベルでデータベース互換性を維持することにより、既存のデータベース アプリケーションは、悪影響を及ぼす可能性のある機能やパフォーマンスの変更から保護されます。 新しいデータベース互換性設定でゲートされた機能を使用する必要がある場合にのみ、アプリケーションを完全に再認定する必要があります。 詳細については、「[Compatibility Certification](../../database-engine/install-windows/compatibility-certification.md)」 (互換性証明書) を参照してください。

### <a name="considerations"></a>考慮事項

- **コスト**: マネージド インスタンスのオプションは、単一データベースのオプションよりもコストが高くなることがあります。  
- **Transact-SQL の相違点**:単一データベースとオンプレミスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、[!INCLUDE[tsql](../../includes/tsql-md.md)] (T-SQL) の違いがいくつかあります。  
- **デプロイ**:マネージド インスタンスのデプロイには、単一データベースよりも時間がかかることがあります。  
- **機能の制限**:マネージド インスタンスでは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] とほとんどの機能を共有しますが、サポートされていない機能がまだいくつかあります。 
- **サイズの制限**:オンプレミス [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では 524 PB であるのに対し、マネージド インスタンス内のすべてのデータベースの結合ストレージ サイズは、8 TB に制限されています。  
- **ネットワーク**:マネージド インスタンスのネットワーク要件により、インフラストラクチャの複雑さがさらに増し、Azure ExpressRoute または VPN Gateway が必要になります。
- **メンテナンス時間**:正確なメンテナンス時間は保証されませんが、ほぼ透過的です。 

### <a name="resources"></a>リソース

[SQL Managed Instance の概要](/azure/sql-database/sql-database-managed-instance)       
[Azure SQL オプションの選択](/azure/sql-database/sql-database-paas-vs-sql-server-iaas)       
[SQL Database 機能の比較](/azure/sql-database/sql-database-features)       
[SQL Server を Azure SQL Managed Instance に移行する](/azure/sql-database/sql-database-managed-instance-migrate)       
[より広範な移行プロセス](/azure/cloud-adoption-framework/migrate/expanded-scope/sql-migration)       

ツール:
- [Data Migration Assistant](../../dma/dma-overview.md)
- [Database Migration Service](/azure/dms/dms-overview)

## <a name="non-sql-options"></a>SQL 以外のオプション

特定の種類のアプリケーションについては、Azure Cosmos DB や Azure テーブル ストレージなどの非リレーショナルまたは NoSQL ソリューションを検討することもできます。

### <a name="azure-cosmos-db"></a>Azure Cosmos DB

JSON データを使用し、堅牢なクエリ処理とトランザクション データ処理の組み合わせを必要とする最新のスケーラブルなモバイル アプリケーションや Web アプリケーションには、Azure Cosmos DB をご検討ください。 詳細については、「[Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)」を参照してください。 データのインポートの詳細については、[Cosmos DB にデータをインポートする方法](/azure/cosmos-db/import-data/)に関するページを参照してください。

Azure Cosmos DB には、次のような利点があります。
- ドキュメントにはインデックスが作成されるので、使い慣れた SQL 構文を使用してクエリを実行することができます。
- データベースはスキーマ フリーです。
- インデックスを再構築せずに、ドキュメントにプロパティを追加できます。
- データベース エンジンの中でも JSON および JavaScript のサポートを利用できます。
- 地理空間データがネイティブでサポートされており、Azure Search、HDInsight、Data Factory などの他のAzure サービスと統合できます。
- 確保されたスループット レベルで、待機時間の短い、高パフォーマンスのストレージを利用できます。

### <a name="azure-table-storage"></a>Azure Table Storage

ペタバイト単位の半構造化データをコスト効率の高いソリューションで格納する場合は、Azure テーブル ストレージをご検討ください。 詳しくは、「 [テーブル ストレージ](https://azure.microsoft.com/services/storage/tables/)」をご覧ください。

Azure テーブル ストレージには、次のような利点があります。
- データをオフラインにせずに、アプリとテーブル スキーマを改善できます。
- シャーディングせずに、データセットをスケール アップできます。
- 複数の領域間でデータをレプリケートする地理的冗長ストレージを利用できます。

## <a name="lifecycle-dates"></a>ライフサイクルの日付

次の表には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 製品のライフサイクルのおおよその日付が示されています。 より詳しく正確なものについては、「[Microsoft ライフサイクル ポリシー](https://support.microsoft.com/hub/4095338/microsoft-lifecycle-policy)」のページを参照してください。 

| **Version**     | **リリース年** | **メインストリーム サポートの終了年** | **延長サポートの終了年** |
| :---------------| :--------------- | :------------------------------ | :---------------------------- |
| [SQL Server 2019](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202019) | 2019 | 2025 | 2030 |
| [SQL Server 2017](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202017) | 2017 | 2022 | 2027 |
| [SQL Server 2016](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202016) | 2016 | 2021 | 2026 |
| [SQL Server 2014](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202014) | 2014 | 2019 | 2024 |
| [SQL Server 2012](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202012) | 2012 | 2017 | 2022 |
| [SQL Server 2008 R2](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202008%20R2) | 2010 | 2012 | [2019](https://www.microsoft.com/sql-server/sql-server-2008) |
| [SQL Server 2008](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202008) | 2008 | 2012 | [2019](https://www.microsoft.com/sql-server/sql-server-2008) |
| [SQL Server 2005](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202005) | 2006 | 2011 | [2016](https://www.microsoft.com/sql-server/sql-server-2005) |
| [SQL Server 2000](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202000) | 2000 | 2005 | [2013](/archive/blogs/cdnitmanagers/sql-server-2000-end-of-support-april-2013) |

> [!IMPORTANT]
> この表と、[!INCLUDE[msCoName](../../includes/msconame-md.md)] ライフサイクルのページが一致しない場合は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] ライフサイクルがこの表よりも優先されます。これは、この表がおおまかな参照としての使用を目的としているためです。  

## <a name="next-steps"></a>次の手順  
[SQL Server 2019](https://www.microsoft.com/sql-server/sql-server-2019)   
[SQL Server 2005 のサポート終了](https://www.microsoft.com/sql-server/sql-server-2005)   
[SQL Server 2008 のサポート終了](https://www.microsoft.com/cloud-platform/windows-sql-server-2008)   
[延長セキュリティ更新プログラム (ESU) の概要](sql-server-extended-security-updates.md)   
[Azure にそのまま移行するための無料の延長セキュリティ更新プログラム (ESU)](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-2008-eos-extend-support)   
[SQL Server VM の概要](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview)   
[Azure SQL Database の概要](/azure/sql-database/sql-database-technical-overview)