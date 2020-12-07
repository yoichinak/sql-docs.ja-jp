---
title: 延長セキュリティ更新プログラムとは
description: サポートとライフサイクルが終了した SQL Server 2008 や SQL Server 2008 R2 などの SQL Server 製品について、SQL Server レジストリを使用して延長セキュリティ更新プログラムを入手する方法を説明します。
ms.custom: ''
ms.date: 11/24/2020
ms.prod: sql
ms.technology: install
ms.topic: conceptual
author: cawrites
ms.author: chadam
ms.reviewer: pmasl
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: f3a337395be09743be335dd01ac80caf9dc98be0
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96121270"
---
# <a name="what-are-extended-security-updates-for-sql-server"></a>SQL Server 用の延長セキュリティ更新プログラムとは
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

この記事では、SQL Server レジストリ サービスを使用して [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] と [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] の延長セキュリティ更新プログラムを受け取る方法について説明します。 その他のオプションの詳細については、[サポート終了オプション](sql-server-end-of-life-overview.md)に関するページを参照してください。 

## <a name="overview"></a>概要
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のサポート ライフサイクルが終了したら、サーバーの延長セキュリティ更新プログラム (ESU) サブスクリプションにサインアップして、新しいバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にアップグレードまたは [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] に移行する準備ができるまで、最大 3 年間保護された状態を維持することができます。 このサブスクリプションは、次の 2 つの方法で利用できます。
-  オンプレミスまたはホスト環境のサーバーについて購入できます。
-  オンプレミスのサーバーを Azure Virtual Machines に移行する場合は無料であり、既定で有効になります。 次に、Azure portal で **SQL Server レジストリ** サービスを使用して、サポートが終了した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを登録し、更新プログラムが利用可能になったときにダウンロードすることができます。 

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを保護された状態に保つために、ESU 修正プログラムが利用可能になったらすぐに適用することをお勧めします。 ESU の詳細については、[ESU の FAQ のページ](https://www.microsoft.com/cloud-platform/extended-security-updates)を参照してください。

> [!IMPORTANT]
> [SQL Server 2008 および 2008 R2 の延長サポートは 2019 年 7 月 10 日をもって終了しました](https://www.microsoft.com/cloud-platform/windows-sql-server-2008)。 これらのバージョンについては、この記事で説明されている延長セキュリティ更新プログラムまたはその他の移行オプションを使用することをご検討ください。 詳細については、[サポート終了オプション](sql-server-end-of-life-overview.md)に関するページを参照してください。

## <a name="what-are-extended-security-updates"></a>延長セキュリティ更新プログラムとは
[!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] および [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] 用の延長セキュリティ更新プログラム (ESU) には、延長サポート更新プログラムのサブスクリプションをご購入いただいたお客様に対する、セキュリティ更新プログラムの提供が含まれています。

ESU は、セキュリティの脆弱性が検出され、[Microsoft Security Response Center (MSRC)](https://portal.msrc.microsoft.com) によって **クリティカル** と評価されると、**必要に応じて** 利用可能になります。 そのため、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ESU に定期的なリリース周期はありません。

ESU に含まれないもの:
- 新機能
- 機能強化
- お客様のご要望による修正

### <a name="support"></a>サポート
ESU にテクニカル サポートは含まれていませんが、オンプレミスを維持することを選択した場合は、[ソフトウェア アシュアランス](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default?activetab=software-assurance-default-pivot%3aprimaryr3)または [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] / [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] の Premier サポートや統合サポートなどのアクティブなサポート契約を使用して、ESU の対象となるワークロードのテクニカル サポートを受けることができます。 または、Azure でホスティングする場合は、Azure サポート プランを使用してテクニカル サポートを受けることができます。 

  > [!NOTE]
  > Microsoft では、ESU サブスクリプションの対象になっていない [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] および [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] インスタンス (オンプレミスとホスト環境の両方) に対してテクニカル サポートを提供することはできません。 

## <a name="esu-availability-and-deployment"></a>ESU の可用性とデプロイ
ESU は、Azure、オンプレミス、またはホスト環境でワークロードを実行しているお客様にご利用いただけます。

### <a name="azure-virtual-machines"></a>Azure Virtual Machines
ワークロードを Azure Virtual Machines (IaaS) に移行すると、サポート終了後最大 3 年間、[!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] と [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] のセキュリティ更新プログラムにアクセスできます。仮想マシンの実行コストを上回る **追加料金はかかりません**。 お客様が Azure で延長セキュリティ更新プログラムを受け取るためにソフトウェア アシュアランスは必要ありません。 

**Windows Server 2008 R2 以降** で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行している Azure Virtual Machines では、[自動修正](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-patching)を使用するよう仮想マシンが構成されている場合、既存の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新プログラム チャネルを通じて自動的に ESU を受け取ります。

**Windows Server 2008** 上で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行している Azure Virtual Machines (VM)、または **[自動修正](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-patching)が構成されて _いない_** 仮想マシンの場合、「[オンプレミスまたはホスト環境](#on-premises-or-hosted-environments)」セクションの説明に従って ESU 修正プログラムを手動でダウンロードして展開する必要があります。

### <a name="on-premises-or-hosted-environments"></a>オンプレミスまたはホスト環境
ソフトウェア アシュアランスをご利用の場合は、Enterprise Agreement (EA)、エンタープライズ サブスクリプション契約 (EAS)、サーバーおよびクラウド加入契約 (SCE)、または教育ソリューション加入契約 (EES) のもとで、サポート終了日から最大 3 年間の延長セキュリティ更新プログラム (ESU) サブスクリプションをご購入いただけます。 ESU は、対象にする必要があるサーバー用にのみご購入いただけます。 ESU は、Microsoft または Microsoft のライセンス パートナーから直接お買い求めいただけます。 

ESU 契約の対象となるお客様は、次の手順に従って ESU 修正プログラムをダウンロードして展開する必要があります。
-  **[SQL Server レジストリ](#create-sql-server-registry)** に [対象のインスタンスを登録](#register-instances-for-esus)します。 
-  登録が完了すると、ESU 修正プログラムがリリースされるたびに、パッケージをダウンロードするためのダウンロード リンクが Azure portal に表示されます。 
-  ダウンロードしたパッケージは、手動で、または組織内で使用されている Microsoft Endpoint Configuration Manager (旧称 System Center Configuration Manager) などの任意の更新プログラム オーケストレーション ソリューションを使用して、オンプレミスまたはホスト環境に展開できます。 

> [!NOTE]
> これは、自動更新プログラムを受信するように構成されていない Azure Stack および Azure Virtual Machines についても、お客様が従う必要があるプロセスです。

詳細については、「[拡張セキュリティ更新プログラムのよくある質問 (FAQ)](https://www.microsoft.com/cloud-platform/extended-security-updates)」を参照してください。 

## <a name="create-sql-server-registry"></a>SQL Server レジストリの作成
ESU が有効な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを登録するには、まず Azure portal で SQL Server レジストリを作成する必要があります。 

> [!IMPORTANT]
> [自動更新](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-patching)用に構成された Azure 仮想マシンを実行している場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを ESU 用に登録する必要はありません。 

SQL Server レジストリを作成するには、次の手順に従います。

1. [Azure Portal](https://portal.azure.com) にサインインします。 
1. **リソースを作成する** オプションを選択します。 
1. 検索ボックスに、「`SQL Server registry`」と入力します。  
1. [!INCLUDE[msCoName](../../includes/msconame-md.md)] によって公開されている **SQL Server レジストリ** オプションを選択し、 **[作成]** を選択します。 

   ![SQL Server レジストリの作成方法が表示されている Auzre portal のスクリーンショット。](media/sql-server-extended-security-updates/sql-server-registry-service.png)

1. **[プロジェクトの詳細]** で、お使いのサブスクリプションをドロップダウンから選択します。 次に、既存の **リソース グループ** を選択するか、 **[新規作成]** を選択して新しい SQL Server レジストリ サービス用の新しいリソース グループを作成します。 
1. **[サービスの詳細]** で、新しい **SQL Server レジストリ** リソースの名前とリージョンを指定します。 

   ![[基本] タブが表示されている SQL Server レジストリのスクリーンショット。](media/sql-server-extended-security-updates/create-new-sql-server-registry.png)

1. **[確認および作成]** を選択して、**SQL Server レジストリ** の詳細を確認します。 検証に合格したら、 **[作成]** を選択します。 

## <a name="register-instances-for-esus"></a>ESU 用にインスタンスを登録する

**SQL Server レジストリ** リソースがデプロイされた後、[1 つ](#single-sql-server-instance)の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを登録するか、複数の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを [一括](#multiple-sql-server-instances-in-bulk)で登録することができます。 ESU パッケージをダウンロードするには、少なくとも 1 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスが SQL Server レジストリのスコープに登録されている必要があります。 

### <a name="single-sql-server-instance"></a>1 つの SQL Server インスタンス

1 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを登録するには、次の手順に従います。

1. [Azure Portal](https://portal.azure.com) にサインインします。 
1. **SQL Server レジストリ** リソースに移動します。 
1. **[概要]** ペインで **[+ 登録]** を選択します。 

   ![[登録] を選択して SQL Server の 1 つのインスタンスを登録する](media/sql-server-extended-security-updates/register-single-sql-server-instance.png)

1. この表に示されているように必要な情報を入力し、 **[登録]** を選択します。 

   |**Value**| **説明**|
   | :-------| :------------- |
   | **インスタンス** | コマンド `SELECT @@SERVERNAME` の出力 (`MyServer\Instance01` など) を入力します。 | 
   | **SQL バージョン** | ドロップダウンから 2008 または 2008 R2 のいずれかを選択します。 | 
   | **のエディション** | ドロップダウンから該当するエディションを選択します: Datacenter、Developer (ESU をご購入いただいた場合は無料でデプロイすることができます)、Enterprise、Standard、Web、Workgroup。 | 
   | **コア** | このインスタンスのコア数を入力します | 
   | **ホストの種類** | ドロップダウンから該当するホストの種類を選択します: 仮想マシン (オンプレミス)、物理サーバー (オンプレミス)、Azure Virtual Machine、Amazon EC2、Google Compute Engine、その他。 |
   | **SubscriptionID**<sup>1</sup> | VM が作成される SubscriptionID を入力します。  |
   | **リソース グループ**<sup>1</sup> | VM が作成されるリソース グループを入力します。  | 
   | **Azure VM 名**<sup>1</sup>  | VM リソース名を入力します。  | 
   | **Azure VM オペレーティング システム**<sup>1</sup> | ドロップダウンから、該当する Windows Server オペレーティング システムのバージョンを選択します。 | 

   <sup>1</sup> Azure 仮想マシンの場合にのみ必要です。 

これで、新しく登録された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスが、 **[概要]** ペインの **[SQL Server インスタンスの登録]** セクションに表示されます。 

![登録された SQL Server インスタンス](media/sql-server-extended-security-updates/registered-sql-instance.png)

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスが登録されると、 **[セキュリティ更新プログラム]** セクションが使用できるようになります。 利用可能な ESU がそこに通知されます。 

### <a name="multiple-sql-server-instances-in-bulk"></a>一括での複数の SQL Server インスタンス

.CSV ファイルをアップロードすることによって、複数の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを一括で登録できます。 [.CSV ファイルの形式を正しく設定](#formatting-requirements-for-csv-file)したら、次の手順に従って、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを SQL Server レジストリ リソースに一括登録できます。 

1. [Azure Portal](https://portal.azure.com) にサインインします。 
1. **SQL Server レジストリ** リソースに移動します。 
1. **[概要]** ペインから **[一括登録]** を選択します。  

   ![[一括登録] を選択して SQL Server の複数のインスタンスを登録する](media/sql-server-extended-security-updates/bulk-register-sql-server-instances.png)

1. ファイルのアイコンを選択して .CSV ファイルの場所を参照します。 .CSV ファイルを選択します。 次に、 **[登録]** を選択してファイルをアップロードし、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のインスタンスを登録します。 

   ![CSV ファイルをアップロードして SQL Server の複数のインスタンスを登録する](media/sql-server-extended-security-updates/upload-csv-file-for-bulk-registration.png)

### <a name="formatting-requirements-for-csv-file"></a>CSV ファイルの形式設定の要件
- 値がコンマで区切られている
- 値が一重引用符または二重引用符で囲まれていない
- 列名は大文字と小文字が区別されませんが、次のように **名前を付ける** 必要があります。 
  - name
  - version
  - edition
  - cores
  - hostType
  - subscriptionID<sup>1</sup>
  - resourceGroup<sup>1</sup>
  - azureVmName<sup>1</sup>
  - AzureVmOS<sup>1</sup>

<sup>1</sup> Azure 仮想マシンの場合にのみ必要です。 

#### <a name="csv-example-1---on-premises"></a>CSV の例 1 - オンプレミス

オンプレミスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの場合、CSV ファイルは次のようになります。 

```csv
name,version,edition,cores,hostType
Server1\SQL2008,2008,Enterprise,12,Physical Server
Server1\SQL2008R2,2008 R2,Enterprise,12,Physical Server
Server2\SQL2008R2,2008 R2,Enterprise,24,Physical Server
Server3\SQL2008R2,2008 R2,Enterprise,12,Virtual Machine
Server4\SQL2008,2008,Developer,8,Physical Server  
```

CSV ファイルの例については、[MyPhysicalServers.csv](https://github.com/microsoft/sql-server-samples/blob/master/samples/manage/sql-server-extended-security-updates/scripts/MyPhysicalServers.csv) を参照してください。

#### <a name="csv-example-2---azure-vm"></a>CSV の例 2 - Azure VM

Azure Virtual Machine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの場合、CSV ファイルは次のようになっている必要があります。 

```csv
name,version,edition,cores,hostType,subscriptionId,resourceGroup,azureVmName,azureVmOS    
ProdServerUS1\SQL01,2008 R2,Enterprise,12,Azure Virtual Machine,61868ab8-16d4-44ec-a9ff-f35d05922847,RG,VM1,2012    
ProdServerUS1\SQL02,2008 R2,Enterprise,24,Azure Virtual Machine,61868ab8-16d4-44ec-a9ff-f35d05922847,RG,VM1,2012    
ServerUS2\SQL01,2008,Enterprise,12,Azure Virtual Machine,61868ab8-16d4-44ec-a9ff-f35d05922847,RG,VM2,2012 R2    
ServerUS2\SQL02,2008,Enterprise,8,Azure Virtual Machine,61868ab8-16d4-44ec-a9ff-f35d05922847,RG,VM2,2012 R2    
SalesServer\SQLProdSales,2008 R2,Developer,8,Azure Virtual Machine,61868ab8-16d4-44ec-a9ff-f35d05922847,RG,VM3,2008 R2  
```

Azure VM を対象にした CSV ファイルの例については、[MyAzureVMs.csv](https://github.com/microsoft/sql-server-samples/blob/master/samples/manage/sql-server-extended-security-updates/scripts/MyAzureVMs.csv) を参照してください。 


> [!TIP]
> 必要な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの登録情報を .CSV ファイルに生成できる [!INCLUDE[tsql](../../includes/tsql-md.md)] と PowerShell のサンプル スクリプトについては、[ESU 登録スクリプトの例](https://github.com/microsoft/sql-server-samples/blob/master/samples/manage/sql-server-extended-security-updates/scripts.md)を参照してください。 

## <a name="download-esus"></a>ESU のダウンロード

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスが SQL Server レジストリ サービスに登録されたら、Azure portal に示されているリンクを使用して、延長セキュリティ更新プログラム パッケージが利用可能な場合に、利用可能になった時点でダウンロードできます。 

ESU をダウンロードするには、次の手順に従います。 

1. [Azure Portal](https://portal.azure.com) にサインインします。 
1. **SQL Server レジストリ** リソースに移動します。 
1. ナビゲーション ペインで、 **[セキュリティ更新プログラム]** を選択します。 

   ![[セキュリティ更新プログラム] ペインで利用可能な更新プログラムを確認する](media/sql-server-extended-security-updates/security-updates-sql-registry.png)

1. セキュリティ更新プログラムが利用可能な場合、利用可能になった時点で、こちらからダウンロードしてください。 

## <a name="supported-regions-and-data-residency"></a>サポートされているリージョンとデータ所在地

**SQL Server レジストリ** サービス (プレビュー) は、Azure リージョンのサブセットで利用できます。 次の表に示すリージョンと、それぞれにおけるデータ所在地の種類が、サポートされています。

| **リージョン** | **データの保存場所** |
|:--|:--|
|オーストラリア東部|ジオ (主要地域)|
|オーストラリア南東部|ジオ (主要地域)|
|カナダ中部|ジオ (主要地域)|
|フランス中部|ジオ (主要地域)|
|東日本|ジオ (主要地域)|
|西日本|ジオ (主要地域)|
|韓国中部|ジオ (主要地域)|
|韓国南部|ジオ (主要地域)|
|米国中北部|ジオ (主要地域)|
|北ヨーロッパ|ジオ (主要地域)|
|米国中南部|ジオ (主要地域)|
|東南アジア|単一リージョン|
|インド南部|ジオ (主要地域)|
|南アフリカ北部|ジオ (主要地域)|
|英国南部|ジオ (主要地域)|
|英国西部|ジオ (主要地域)|
|米国西部|ジオ (主要地域)|
|米国東部|ジオ (主要地域)|
|米国中部|ジオ (主要地域)|
|東アジア|ジオ (主要地域)|
|西ヨーロッパ|ジオ (主要地域)|
|米国中西部|ジオ (主要地域)|
|米国西部 2|ジオ (主要地域)|
|米国東部 2|ジオ (主要地域)|

リージョンに地理的な所在地が含まれる場合は、SQL レジストリ サービスによって geo 冗長ストレージ アカウント (GRS) にデータ バックアップが保持されます。  リージョンに含まれるのが単一のリージョン所在地である場合は、SQL レジストリ サービスによってゾーン冗長ストレージ アカウント (ZRS) にデータ バックアップが保持されます。 詳細については、[トラスト センター](https://azuredatacentermap.azurewebsites.net/)に関するページを参照してください。

## <a name="configure-regional-redundancy"></a>リージョン冗長を構成する 

**SQL Server レジストリ** に対するリージョン冗長を必要とするお客様は、2 つの異なるリージョンに登録データを作成できます。 その後、お客様は、**SQL Server レジストリ** サービスの可用性に基づいて、いずれかのリージョンからセキュリティ更新プログラムをダウンロードできます。 

リージョン冗長を使用するには、**SQL Server レジストリ** サービスを 2 つの異なるリージョンに作成する必要があり、SQL Server のインベントリをこれら 2 つのサービス間で分割する必要があります。 これにより、SQL Server の半分は一方のリージョンのレジストリ サービスに登録され、SQL Server の残りの半分はもう一方のリージョンのレジストリ サービスに登録されます。 

リージョン冗長を構成するには、次の手順のようにします。

1. SQL Server 2008 または 2008 R2 のインベントリを、2 つのファイル (upload1.csv と upload2.csv など) に分割します。 
  
   :::image type="content" source="media/sql-server-extended-security-updates/two-upload-files-for-regional-redundancy.png" alt-text="アップロード ファイルの例":::

1. 1 つのリージョンに最初の **SQL Server レジストリ** サービスを作成し、csv ファイルの 1 つをそれに一括登録します。 たとえば、最初の **SQL Server レジストリ** サービスを **米国西部** リージョンに作成し、upload1.csv ファイルを使用して SQL Server を一括登録します。 
1. 2 番目の **SQL Server レジストリ** サービスを第 2 のリージョンに作成し、他の csv ファイルをそこに一括登録します。 たとえば、2 番目の **SQL Server レジストリ** サービスを **米国東部** リージョンに作成し、upload2.csv ファイルを使用して SQL Server を一括登録します。 


データが 2 つの異なる **SQL Server レジストリ** リソースに登録されると、サービスの可用性に基づいて、いずれかのリージョンからセキュリティ更新プログラムをダウンロードできるようになります。 


## <a name="faq"></a>よく寄せられる質問

延長セキュリティ更新プログラムに関してよく寄せられる一般的な質問については、「[拡張セキュリティ更新プログラムのよくある質問 (FAQ)](https://www.microsoft.com/cloud-platform/extended-security-updates)」を参照してください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に特定のよく寄せられる質問を以下に示します。 

**SQL Server 2008 と 2008 R2 のサポートが終了したのはいつですか?**

[!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] および [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] のサポート終了日は 2019 年 7 月 9 日です。 

**サポート終了とは何を意味しますか?**

Microsoft ライフサイクル ポリシーでは、ビジネスおよび開発者向け製品 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] や Windows Server など) に対して 10 年間のサポート (5 年間のメインストリーム サポートと 5 年間の延長サポート) が提供されます。 そのポリシーに従い、延長サポート期間が終了した後は、修正プログラムやセキュリティ更新プログラムは提供されません。これにより、セキュリティとコンプライアンスの問題が発生する可能性があり、お客様のアプリケーションやビジネスを重大なセキュリティ リスクにさらすことになりかねません。

**SQL Server のどのエディションが延長セキュリティ更新プログラムの対象になりますか?**

[!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] および [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] の Enterprise、Datacenter、Standard、Web、Workgroup の各エディション (x86 バージョンと x64 バージョンの両方) が、延長セキュリティ更新プログラムの対象になります。 

**延長セキュリティ更新プログラムはいつ提供されますか?**

延長セキュリティ更新プログラムをご購入いただけるようになりました。[!INCLUDE[msCoName](../../includes/msconame-md.md)] または [!INCLUDE[msCoName](../../includes/msconame-md.md)] ライセンス パートナーにご注文いただけます。 延長セキュリティ更新プログラムの配信は、サポート終了日を過ぎてから、利用可能な場合に、利用可能になった時点で開始されます。 Azure への移行に関心があるお客様は、すぐに移行することができます。 

**延長セキュリティ更新プログラムには何が含まれていますか?** 

延長セキュリティ更新プログラムでは、2019 年 7 月 9 日から最大 3 年間、[Microsoft Security Response Center (MSRC)](https://portal.msrc.microsoft.com/) によって **クリティカル** と評価されたセキュリティ更新プログラムとセキュリティ情報が提供されます。 延長セキュリティ更新プログラムは、利用可能な場合に利用可能になった時点で配信されます。 延長セキュリティ更新プログラムにはテクニカル サポートは含まれていませんが、延長セキュリティ更新プログラムの対象となるワークロードに関する [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] および [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] の質問には、[!INCLUDE[msCoName](../../includes/msconame-md.md)] の他のサポート プランを使用できます。 延長セキュリティ更新プログラムには、新機能や機能強化、またはお客様のご要望による修正プログラムは含まれません。 ただし、[!INCLUDE[msCoName](../../includes/msconame-md.md)] には、必要と見なされたセキュリティ以外の修正プログラムが含まれる場合があります。

**SQL Server 2008 および 2008 R2 の延長セキュリティ更新プログラムでは、なぜ "クリティカル" な更新プログラムのみが提供されるのですか?**

これまでのサポート終了時には、エンタープライズのお客様のコンプライアンス基準を満たす、重要なセキュリティ更新プログラムのみを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で提供してきました。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、一般的な月単位のセキュリティ更新プログラムは提供されません。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、MSRC の情報で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が影響を受ける製品として特定されている場合に、対応するオンデマンドの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ更新プログラム (GDR) のみを提供しています。
新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の重要な更新プログラムが提供されず、お客様は緊急と判断するが MSRC では緊急としない状況が発生した場合は、ケースバイケースでお客様と相談のうえ、適切な軽減処置をご提案します。

**どのライセンス プログラムが延長セキュリティ更新プログラムの対象となりますか?**

ソフトウェア アシュアランスをご利用のお客様は、Enterprise Agreement (EA)、エンタープライズ サブスクリプション契約 (EAS)、サーバーおよびクラウド加入契約 (SCE)、または教育ソリューション加入契約 (EES) のもとで、オンプレミスの延長セキュリティ更新プログラムをご購入いただけます。 ソフトウェア アシュアランスと同じ加入契約である必要はありません。

**SQL Server ユーザーが延長セキュリティ更新プログラムのメリットを活用するためには、最新の Service Pack を実行している必要がありますか?**

はい。延長セキュリティ更新プログラムを適用するには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Windows Server 2008 および 2008 R2 を最新の Service Pack を使用して実行している必要があります。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] は、最新の Service Pack に適用可能な更新プログラムのみを作成します。

**ソフトウェア アシュアランスを利用していない SQL Server ユーザーの場合、どのようなオプションがありますか?** 

ソフトウェア アシュアランスをご利用でないお客様の場合、延長セキュリティ更新プログラムにアクセスするための代替オプションとして、Azure に移行することができます。 変動するワークロードの場合、お客様にお勧めするのは従量課金制で Azure に移行することです。これにより、いつでもスケールアップまたはスケールダウンできます。 予測可能なワークロードの場合、お客様にはサーバー サブスクリプションと予約インスタンスを使用して Azure に移行することをお勧めします。
  
**このオファーは SQL Server 2005 にも適用されますか?**

いいえ。 このような以前のバージョンの場合は、最新バージョンにアップグレードすることをお勧めしますが、お客様はこのオファーのメリットを活用するために、[!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] バージョンまたは [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] バージョンにアップグレードすることができます。

**新しい SQL Server 2008 または 2008 R2 のインスタンスを Azure にデプロイした場合も、延長セキュリティ更新プログラムを入手できますか?**

はい。お客様は、Azure 仮想マシンで新しい [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] または [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] インスタンスを開始し、延長セキュリティ更新プログラムにアクセスできます。

**延長セキュリティ更新プログラムを購入せずに、サポート終了後に SQL Server 2008 または 2008 R2 のテクニカル サポートを受けることはできますか?**

いいえ。 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] または [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] をご利用のお客様が、延長セキュリティ更新プログラムをご購入いただかず、移行中にオンプレミスのままにすることを選択した場合、サポート プランをお持ちでもサポート チケットを作成することができません。 ただし、Azure に移行する場合は、Azure サポート プランを使用してサポートを受けることができます。

**SQL Server 2008 および 2008 R2 のユーザーが、自分のライセンスを持ち込む (BYOL) 必要がある場合、ソフトウェア アシュアランスを保有している必要がありますか?**

はい。お客様がライセンス モビリティ プログラムの一部として Azure Virtual Machines 上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で BYOL プログラムを活用するためには、ソフトウェア アシュアランスをご利用いただく必要があります。 ソフトウェア アシュアランスをお持ちでないお客様には、[!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 環境を対象に Azure SQL Managed Instance への移行をお勧めします。 お客様は、従量課金制の Azure Virtual Machines に移行することもできます。 SQL をコア単位でライセンスするソフトウェア アシュアランスのお客様は、Azure ハイブリッド特典 (AHB) を使用して Azure に移行することもできます。

Azure SQL Managed Instance は、オンプレミス [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] とのほぼ 100% の互換性を提供する Azure のサービスです。 Managed Instance には、組み込みの高可用性およびディザスター リカバリー機能に加え、インテリジェントなパフォーマンス機能と、即座にスケーリングする機能が用意されています。 また Managed Instance では、手動でのセキュリティ修正プログラムの適用やアップグレードの必要性を解消する、バージョンに関係しないエクスペリエンスが提供されます。 BYOL プログラムの詳細については、Azure の料金ガイダンスのページを参照してください。

**Azure で SQL Server を実行するには、どのようなオプションがありますか?**

お客様は、従来の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境をフル マネージドのデータ プラットフォーム サービス (PaaS) である Azure SQL Managed Instance (サポート終了日に関する懸念が解消される "バージョンに関係しない" オプションが提供されます) に移行するか、セキュリティ更新プログラムにアクセスできる Azure Virtual Machines に移行することができます。 移行したデータベースとレガシ システムとの互換性が維持されます。 詳細については、「[Compatibility Certification](../../database-engine/install-windows/compatibility-certification.md)」 (互換性証明書) を参照してください。

延長セキュリティ更新プログラムは、2019 年 7 月 9 日のサポート終了日後の次の 3 年間、Azure Virtual Machines の [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] と [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] で利用できます。 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] と [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] からアップグレードしようとしているお客様については、以降のすべてのバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がサポートされます。 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] については、お客様はサポートされている最新の Service Pack を適用済みである必要があります。 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 以降では、最新の累積更新プログラムを適用することが推奨されます。 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 以降では、Service Pack を使用できず、累積更新プログラムと一般配布リリース (GDR) のみを利用できることに注意してください。

Azure SQL Managed Instance は、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] でのインスタンスをスコープとするデプロイ オプションで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エンジンの互換性とネイティブ仮想ネットワーク (VNET) の最も幅広いサポートを提供するものです。そのため、アプリを変更することなく [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースを Managed Instance に移行できます。 充実した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセキュリティと、インテリジェントなフル マネージド サービスの運用上および財務上の利点が組み合わされています。 新しい Azure Database Migration Service を利用すると、アプリケーション コードの変更をほとんどまたはまったく行わずに、[!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] と [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] を Azure SQL Managed Instance に移行できます。

**SQL Server 2008 バージョンと 2008 R2 バージョンの Azure ハイブリッド特典を利用することはできますか?**

はい。アクティブなソフトウェア アシュアランスまたはそれに相当するサーバー サブスクリプションをお持ちのお客様は、Azure ハイブリッド特典をご利用いただけます。既存のオンプレミス ライセンスへの投資を利用して、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] および Azure Virtual Machines で実行している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でコストを削減できます。

**Azure Government リージョンで無料の延長セキュリティ更新プログラムを入手できますか?**

はい。延長セキュリティ更新プログラムは Azure Government リージョンの Azure Virtual Machines で利用できます。

**Azure Stack では、無料の延長セキュリティ更新プログラムを入手できますか?**

はい。お客様は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Windows Server 2008、[!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] を Azure Stack に移行し、サポート終了日後に追加コストなしで延長セキュリティ更新プログラムを受け取ることができます。

**共有ストレージを使用している 2008 と 2008 R2 の SQL クラスター ユーザーの場合、Azure に移行するためのガイダンスは何ですか?**

Azure では現在のところ、共有ストレージのクラスタリングをサポートしていません。 Azure で可用性が高い [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを構成する方法については、[SQL Server 高可用性ガイド](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr)を参照してください。

**サード パーティのホストを使用して SQL Server の延長セキュリティ更新プログラムを利用できますか?**

[!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 環境を他のクラウド プロバイダーの PaaS 実装に移行した場合、延長セキュリティ更新プログラムを利用することはできません。 仮想マシン (IaaS) に移行しようとしているお客様の場合は、ソフトウェア アシュアランスを通じて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のライセンス モビリティを利用して移行し、[!INCLUDE[msCoName](../../includes/msconame-md.md)] から延長セキュリティ更新プログラムをご購入いただき、承認された SPLA ホスト側サーバーの VM (IaaS) で実行されている [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] インスタンスに修正プログラムを手動で適用することができます。 しかし、Azure の無料更新プログラムの方がより魅力的なオファーです。

**Azure Virtual Machines で SQL Server のパフォーマンスを強化するためのベスト プラクティスは何ですか?** 

Azure Virtual Machines で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のパフォーマンスを最適化する方法については、[SQL Server 最適化ガイド](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance)を参照してください。 

## <a name="see-also"></a>関連項目

- [SQL Server 2008/2008 R2 のライフサイクルのページ](https://support.microsoft.com/lifecycle/search?alpha=sql%20server%202008)
- [SQL Server 2008/2008 R2 のサポート終了のページ](https://aka.ms/sqleos)
- [拡張セキュリティ更新プログラムのよくある質問 (FAQ)](https://aka.ms/sqleosfaq)
- [Microsoft Security Response Center (MSRC)](https://portal.msrc.microsoft.com/security-guidance/summary)
- [Azure Automation を使用して Windows 更新プログラムを管理する](/azure/automation/update-management/overview)
- [SQL Server VM の自動修正](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-patching)
- [Microsoft データ移行ガイド](https://datamigration.microsoft.com/)
- [Azure Migrate: 現在の SQL Server 2008/2008 R2 を Azure VM に移行するためのリフトアンドシフトのオプション](https://azure.microsoft.com/services/azure-migrate/)
- [SQL 移行のクラウド導入フレームワーク](/azure/cloud-adoption-framework/migrate/expanded-scope/sql-migration)
- [GitHub の ESU 関連スクリプト](https://github.com/microsoft/sql-server-samples/tree/master/samples/manage/sql-server-extended-security-updates/scripts)

