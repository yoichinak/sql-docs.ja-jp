---
title: サポートされているバージョンとエディションのアップグレード (SQL Server 2017)
description: SQL Server 2017 のサポートされているバージョンとエディションのアップグレード。
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- components [SQL Server], adding to existing installations
- versions [SQL Server], upgrading
- upgrading SQL Server, upgrades supported
- cross-language support
ms.assetid: 702359c4-6ca9-42a8-860c-a95a802898a1
author: cawrites
ms.author: chadam
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 4d78e73c3beab2b45ecacf27e18695d6de719b08
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100341804"
---
# <a name="supported-version--edition-upgrades-sql-server-2017"></a>サポートされているバージョンとエディションのアップグレード (SQL Server 2017)

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]
  
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]、および [!INCLUDE[sssql15-md](../../includes/sssql16-md.md)] からアップグレードできます。 この記事では、これらの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バージョンからのサポートされているアップグレード パスと、サポートされている [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] へのエディションのアップグレードを示します。  
  
## <a name="pre-upgrade-checklist"></a>アップグレード前のチェック リスト  
  
-   [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] のいずれかのエディションから別のエディションへアップグレードする前に、現在使用している機能が移動先のエディションでサポートされているかどうかを確認します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をアップグレードする前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの Windows 認証を有効にし、既定の構成 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのサービス アカウントが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sysadmin グループのメンバーであること) を確認してください。  
  
-   [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]にアップグレードするには、サポート対象のオペレーティング システムを実行している必要があります。 詳細については、「[SQL Server のインストールに必要なハードウェアおよびソフトウェア](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)」を参照してください。  
  
-   再起動を保留している場合はアップグレードがブロックされます。  
  
-   Windows インストーラー サービスが実行されていない場合は、アップグレードがブロックされます。  
  
## <a name="unsupported-scenarios"></a>サポートされないシナリオ  
  
-   [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] の複数バージョンにまたがるインスタンスの使用はサポートされていません。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] コンポーネントのバージョン番号は、[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] のインスタンス内で同一である必要があります。  
  
-   [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] は、64 ビット プラットフォームでのみ利用できます。 クロスプラットフォームのアップグレードはサポートされていません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 32 ビット インスタンスをネイティブ 64 ビットにアップグレードすることはできません。 ただし、データベースがレプリケーションでパブリッシュされていない場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の 32 ビット インスタンスのデータベースをバックアップまたはデタッチしてから、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新しいインスタンス (64 ビット) に復元またはアタッチすることができます。 master、msdb、および model の各システム データベースにある、すべてのログインとその他のユーザー オブジェクトを再作成する必要があります。  
  
-   既存の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスのアップグレード中は、新しい機能を追加できません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] にアップグレードした後、[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] のセットアップを使用して機能を追加できます。 詳細については、「[SQL Server のインスタンスへの機能の追加 &#40;セットアップ&#41;](./add-features-to-an-instance-of-sql-server-setup.md)」を参照してください。  
 
-   フェールオーバー クラスターは、WOW モードでサポートされていません。  
    
## <a name="upgrades-from-earlier-versions-to-sssql17-md"></a>以前のバージョンから [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]  
 
[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] では、次のバージョンの SQL Server からのアップグレードがサポートされます。
 
- SQL Server 2008 SP4 以降
- SQL Server 2008 R2 SP3 以降
- SQL Server 2012 SP2 以降
- SQL Server 2014 以降 
- SQL Server 2016 以降
 

  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] でデータベースをアップグレードするには、 [2005 のサポート](#SupportFor2005)を参照してください。  
  
 次の表に示すのは、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]への、サポートされるアップグレード シナリオです。  
  
|アップグレード元|サポートされているアップグレード パス|  
|:------|:------|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Enterprise|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Developer|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Developer|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Standard|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Small Business|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Web|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Web|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Workgroup|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Express |[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Web <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Express|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Datacenter|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Enterprise|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Developer|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Developer|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Small Business|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Standard|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Web|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Web|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Workgroup|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Express |[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Web <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Enterprise|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Developer|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Developer <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Web <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Standard|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Web|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Web|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Express |[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Web <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Express <br/> <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Business Intelligence|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Evaluation|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Web <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Developer|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Developer <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Web <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Web|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express |[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Web <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Express <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Developer|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Evaluation|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Web <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Developer|
|[!INCLUDE[sssql16-md](../../includes/sssql16-md.md)] Enterprise|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/> |  
|[!INCLUDE[sssql16-md](../../includes/sssql16-md.md)] Developer|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Developer <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Web <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/> |  
|[!INCLUDE[sssql16-md](../../includes/sssql16-md.md)] Standard|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard|  
|[!INCLUDE[sssql16-md](../../includes/sssql16-md.md)] Web|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Web|  
|[!INCLUDE[sssql16-md](../../includes/sssql16-md.md)] Express |[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Web <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Express <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Developer|  
|[!INCLUDE[sssql16-md](../../includes/sssql16-md.md)] Business Intelligence|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/> |  
|[!INCLUDE[sssql16-md](../../includes/sssql16-md.md)] Evaluation|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Web <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Developer|
|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] リリース候補 * |[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise |  
|[!INCLUDE [sssql17-md](../../includes/sssql17-md.md)] Developer |[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise | 

 \* Microsoft では、特に Technology Adoption Program (TAP) に参加したお客様向けに、リリース候補版ソフトウェアからのアップグレードをサポートしています。 

   
###  <a name="sssql17-md-support-for-ssversion2005"></a><a name="SupportFor2005"></a> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] に対する [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] のサポート  
 ここでは、 [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] に対する [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]のサポートについて説明します。 [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]では、次の作業を実行できます。  
  
-   データベース エンジンの [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスに、 [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] データベース (mdf/ldf ファイル) をアタッチします。  
  
-   バックアップからデータベース エンジンの [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスに [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] データベースを復元します。  
  
-   [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] キューブをバックアップし、[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] で復元します。  
  
[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] データベースを [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] にアップグレードすると、そのデータベースの互換性レベルは 90 から 100 に変更されます ([!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] のデータベース互換性レベルの有効な値は 100、110、120、130、および 140 です)。[ALTER DATABASE Compatibility Level &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) は、互換性レベルの変更が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アプリケーションに与える影響について説明します。  
  
上記の一覧で説明されていないどのシナリオもサポートされていませんが、以下のシナリオに限定されるものではありません。  
  
- 同じコンピューターへの [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] と [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] の (サイド バイ サイド) インストール。  
  
- [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスに参加するレプリケーション トポロジのメンバーとして [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] インスタンスを使用する。  
  
- [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] インスタンスと [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスの間でのデータベース ミラーリングの構成。  
  
- [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] インスタンスと [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスの間でのログ配布によるトランザクション ログのバックアップ。  
  
- [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] インスタンスと [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスの間でのリンク サーバーの構成。  
  
- [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Management Studio からの [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] インスタンスの管理。  
  
- [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] Management Studio 内での [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] キューブのアタッチ。  
  
- [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] Management Studio から [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] への接続  
  
- [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] Management Studio からの [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] サービスの管理。  
  
- [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] のサード パーティのカスタム Integration Services コンポーネントに対するサポート (実行とアップグレードなど)。  
  
## <a name="sssql17-md-edition-upgrade"></a>[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] エディションのアップグレード  
次の表に示すのは、 [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]でサポートされるエディションのアップグレード シナリオです。  
  
エディションのアップグレードを実行する手順については、「[Upgrade to a Different Edition of SQL Server &#40;Setup&#41;](../../database-engine/install-windows/upgrade-to-a-different-edition-of-sql-server-setup.md)」 (SQL Server の別のエディションへのアップグレード &#40;セットアップ&#41;) を参照してください。  
  
|アップグレード元|アップグレード先|  
|------------------|----------------|  
|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise (Server+CAL および Core)**|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise |  
|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Evaluation Enterprise**|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise (Server+CAL または Core ライセンス) <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Developer <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Web <br/> <br/> Evaluation (無償エディション) からいずれかの有償エディションへのアップグレードは、スタンドアロン インストールではサポートされていますが、クラスター化インストールではサポートされていません。 この制限は、可用性グループに参加している Windows フェールオーバー クラスターにインストールされているスタンドアロン インスタンスには適用されません。|  
|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard**|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise (Server+CAL または Core ライセンス)|  
|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Developer**|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise (Server+CAL または Core ライセンス) <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Web <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard|  
|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Web|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise (Server+CAL または Core ライセンス) <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard|  
|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Express*|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise (Server+CAL または Core ライセンス) <br/><br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Developer <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard <br/> <br/> [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Web|  
  
 さらに、 [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise (Server+CAL ライセンス) と [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise (Core License) の間でエディションのアップグレードも実行できます。  
  
|エディションのアップグレード元|エディションのアップグレード先|  
|--------------------------|------------------------|  
|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise (Server+CAL ライセンス)**|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise (Core ライセンス)|  
|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise (Core ライセンス)|[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise (Server+CAL ライセンス)|  
  
 \*[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Express with Tools および [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Express with Advanced Services についても同様です。  
  
 ** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] フェールオーバー クラスターのエディションの変更は制限されています。 次のシナリオは、 [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] フェールオーバー クラスターではサポートされていません。  
  
-   [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Enterprise から [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Developer、Standard、または Evaluation への変更  
  
-   [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Developer から [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard または Evaluation への変更  
  
-   [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard から [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Evaluation への変更  
  
-   [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Evaluation から [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] Standard への変更  
  
## <a name="see-also"></a>参照  

 [SQL Server 2017 の各エディションとサポートされる機能](../../sql-server/editions-and-components-of-sql-server-2017.md)
 
 [SQL Server のインストールに必要なハードウェアおよびソフトウェア](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 
 [SQL Server のアップグレード](../../database-engine/install-windows/upgrade-sql-server.md)  
  
