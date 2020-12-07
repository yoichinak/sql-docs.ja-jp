---
title: SQL Server 2016 および 2017:ハードウェアとソフトウェアの要件
description: SQL Server 2016 および SQL Server 2017 をインストールして実行するためのハードウェア、ソフトウェア、およびオペレーティング システムの要件の一覧。
ms.custom: seo-lt-2019
ms.date: 02/19/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- Setup [SQL Server], software
- software [SQL Server]
- installing SQL Server, software
- operating systems [SQL Server], SQL Server requirements
- Setup [SQL Server], cross-language support
- operating systems [SQL Server], cross-language support
- network connections [SQL Server], requirements
- disk space [SQL Server], SQL Server installations
- WOW [SQL Server]
- Setup [SQL Server], hardware
- dependencies [SQL Server], SQL Server installations
- cluster hardware requirements [SQL Server]
- endpoints [SQL Server], SQL Server installations
- Internet [SQL Server], SQL Server installations
- hardware [SQL Server]
- Windows on Windows [SQL Server]
- installing SQL Server, hardware
- Setup Configuration Checker
- SCC [SQL Server]
- operating systems [SQL Server]
- space [SQL Server], SQL Server installations
- system configuration checker
- installing SQL Server, cross-language support
- Internet [SQL Server]
- space [SQL Server]
- extended system support [SQL Server]
- 64-bit edition [SQL Server]
- failover clustering [SQL Server]
- failover clustering [SQL Server], hardware requirements
- 32-bit edition [SQL Server]
- locales [SQL Server], SQL Server installations
- cross-language support
- disk space [SQL Server]
- localized SQL Server versions
ms.assetid: 09bcf20b-0a40-4131-907f-b61479d5e4d8
ms.author: chadam
author: cawrites
ms.openlocfilehash: a2fb4a36b5ef11a67f9896584ed7fb101d4a042e
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96127532"
---
# <a name="sql-server-2016-and-2017-hardware-and-software-requirements"></a>SQL Server 2016 および 2017:ハードウェアとソフトウェアの要件
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

この記事には、Windows オペレーティング システムで SQL Server 2016 および SQL Server 2017 をインストールして実行するための、ハードウェアとソフトウェアの最小要件が一覧表示されています。  

他のバージョンの SQL Server のハードウェアとソフトウェアの要件については、以下を参照してください。
- [SQL Server 2019](hardware-and-software-requirements-for-installing-sql-server-ver15.md)
- [SQL Server on Linux](../../linux/sql-server-linux-setup.md#system)

## <a name="hardware-requirements"></a>ハードウェア要件

 SQL Server 2016 および SQL Server 2017 には、次のハードウェア要件が適用されます。 
  
|コンポーネント|要件|  
|---------------|-----------------|  
|ハード ディスク|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] では 6 GB 以上のハード ディスク空き容量が必要です。<br/><br/> 必要となるディスク空き容量は、インストールする [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] のコンポーネントに応じて異なります。 詳細については、この記事で後述する「[必要なハード ディスク空き容量](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace)」を参照してください。 データ ファイルでサポートされているストレージの種類の詳細については、「 [Storage Types for Data Files](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes)」を参照してください。 <br/><br/> NTFS または ReFS ファイル形式のコンピューターに SQL Server をインストールすることをお勧めします。 FAT32 ファイル システムはサポートされていますが、NTFS または ReFS ファイル システムよりも安全性が低いため、お勧めできません。 <br/><br/>  読み取り専用、マップ、または圧縮されたドライブは、インストール時にブロックされます。 |  
|ドライブ|ディスクからインストールする場合は、DVD ドライブが必要です。  |  
|モニター|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] では Super-VGA (800x600) 以上の解像度のモニターが必要です。|  
|インターネット|インターネット機能にはインターネット アクセス (有料) が必要です。|  
|メモリ \*|**最小:**<br/><br/> Express Edition: 512 MB<br/><br/> 他のすべてのエディション: 1 GB<br/><br/> **推奨:**<br/><br/> Express Edition: 1 GB<br/><br/> 他のすべてのエディション: 4 GB 以上。最適なパフォーマンスを確保するために、データベースのサイズが大きくなるにつれて増やす必要があります。|  
|プロセッサの速度|**最小:** x64 プロセッサ:1.4 GHz<br/><br/> **推奨:** 2.0 GHz 以上|  
|プロセッサの種類|x64 プロセッサ: AMD Opteron、AMD Athlon 64、Intel Xeon (Intel EM64T 対応)、Intel Pentium IV (EM64T 対応)|  
  
> [!NOTE]  
> [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] は x64 プロセッサでのみイントールできます。 X86 プロセッサではインストールできません。  
  
 \*[!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) の [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] コンポーネントをインストールする場合の最小メモリ要件は 2 GB の RAM で、[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] の最小メモリ要件とは異なります。 DQS のインストールの詳細については、「 [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)」を参照してください。  
  
  
##  <a name="software-requirements"></a><a name="hwswr"></a> ソフトウェア要件  

このセクションの表には、SQL Server を実行するためのソフトウェアの最小要件が一覧表示されています。 [最適なパフォーマンス](https://support.microsoft.com/help/4465518/recommended-updates-and-configurations-for-sql-server)を得るための推奨される構成オプションもあります。 

次のソフトウェア要件は、すべてのインストールに適用されます。  
  
|コンポーネント|要件|  
|---------------|-----------------|  
|.NET Framework|[!INCLUDE[sql2016](../../includes/sssql15-md.md)] 以降では、データベース エンジン、マスター データ サービス、レプリケーションのために [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6 が必要になります。 SQL Server セットアップで [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] が自動的にインストールされます。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Microsoft .NET Framework 4.6 (Web Installer) for Windows [から](https://support.microsoft.com/kb/3045560)を手動でインストールすることもできます。<br/><br/> [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6 の詳細、推奨事項、ガイダンスについては、「 [.NET Framework 配置ガイド (開発者向け)](https://msdn.microsoft.com/library/ee942965\(v=vs.110\).aspx)」を参照してください。<br/><br/>[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6 をインストールするには、[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)] と [!INCLUDE[winblue_server_2](../../includes/winblue-server-2-md.md)] に [KB2919355](https://support.microsoft.com/kb/2919355) が必要になります。|  
|ネットワーク ソフトウェア|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] でサポートされるオペレーティング システムにはネットワーク ソフトウェアが組み込まれています。 スタンドアロン インストールの名前付きおよび既定のインスタンスでは、次のネットワーク プロトコルがサポートされています。共有メモリ、名前付きパイプ、TCP/IP、および VIA。<br/><br/> **注:** VIA プロトコルはフェールオーバー クラスターではサポートされません。 SQL Server インスタンスと同じフェールオーバー クラスターのノード上で実行されているクライアントまたはアプリケーションは、そのローカル パイプ アドレスを使用して SQL Server に接続するために、共有メモリ プロトコルを使用することができます。 ただし、この種の接続はクラスターに対応しないため、インスタンスのフェールオーバー後に失敗します。 したがって、これは非推奨であり、非常に限られたシナリオでのみ使用する必要があります。<br/><br/> **重要:** VIA プロトコルは非推奨とされます。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]<br/><br/> ネットワーク プロトコルとネットワーク ライブラリの詳細については、「 [Network Protocols and Network Libraries](../../sql-server/install/network-protocols-and-network-libraries.md)」を参照してください。|  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップを実行すると、製品に必要な以下のソフトウェア コンポーネントがインストールされます。  
  
   - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client    
   - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ サポート ファイル  

  
  
> [!IMPORTANT]
> PolyBase 機能には、ハードウェアとソフトウェアに追加の要件があります。 詳細については、「 [PolyBase 入門](../../relational-databases/polybase/polybase-guide.md)」を参照してください。  
  



## <a name="operating-system-support"></a>オペレーティング システムのサポート

次の表では、Windows のバージョンと SQL Server 2016 と 2017 のエディションとの互換性を示します。  
  
| SQL Server のエディション:               | Enterprise | Developer | Standard | Web | Express |  
| :------------------------         | :--------- | :-------- | :------- | :-- | :------ | 
| Windows Server 2019 Datacenter    |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2019 Standard      |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2019 Essentials    |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2016 Datacenter    |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2016 Standard      |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2016 Essentials    |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2012 R2 Datacenter |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2012 R2 Standard   |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2012 R2 Essentials |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2012 R2 Foundation |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2012 Datacenter    |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2012 Standard      |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2012 Essentials    |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2012 Foundation    |    はい     |    はい    |    はい   | はい |   はい   |
| Windows 10 IoT Enterprise         |    いいえ      |    はい    |    はい   | いいえ  |   はい   |
| Windows 10 Enterprise             |    いいえ      |    はい    |    はい   | いいえ  |   はい   |
| Windows 10 Professional           |    いいえ      |    はい    |    はい   | いいえ  |   はい   |
| Windows 10 Home                   |    いいえ      |    はい    |    はい   | いいえ  |   はい   |
| Windows 8.1 Enterprise            |    いいえ      |    はい    |    はい   | いいえ  |   はい   |
| Windows 8.1 Pro                   |    いいえ      |    はい    |    はい   | いいえ  |   はい   |
| Windows 8.1 Enterprise            |    いいえ      |    はい    |    はい   | いいえ  |   はい   |
| Windows 8 Pro                     |    いいえ      |    はい    |    はい   | いいえ  |   はい   |
| Windows 8                         |    いいえ      |    はい    |    はい   | いいえ  |   はい   | 

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を [!INCLUDE[win8srv](../../includes/win8srv-md.md)] または [!INCLUDE[win8](../../includes/win8-md.md)] にインストールするための最低限のバージョン要件については、[ Windows Server 2012 または Windows 8 への SQL Server のインストール](https://support.microsoft.com/kb/2681562)に関するページを参照してください。 


### <a name="server-core-support"></a>Server Core のサポート

SQL Server 2016 および 2017 の Server Core モードでのインストールは、次のエディションの Windows Server でサポートされます。

:::row:::
    :::column:::
        Windows Server 2019 Standard
    :::column-end:::
    :::column:::
        Windows Server 2019 Datacenter
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        Windows Server 2016 Standard
    :::column-end:::
    :::column:::
        Windows Server 2016 Datacenter
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        Windows Server 2012 R2 Standard
    :::column-end:::
    :::column:::
        Windows Server 2012 R2 Datacenter
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        Windows Server 2012 Standard
    :::column-end:::
    :::column:::
        Windows Server 2012 Datacenter
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

Server Core への SQL Server のインストールの詳細については、「[Server Core への SQL Server のインストール](../../database-engine/install-windows/install-sql-server-on-server-core.md)」を参照してください。  

### <a name="wow64-support"></a>WOW64 のサポート
  
 WOW64 (Windows 32-bit on Windows 64-bit) は 64 ビット版 Windows の機能で、32 ビット アプリケーションをネイティブの 32 ビット モードで実行することができます。 つまり、基盤となるオペレーティング システムが 64 ビット オペレーティング システムであっても、アプリケーションは 32 ビット モードで動作します。 WOW64 は、 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] インストールではサポートされていません。 ただし、管理ツールは WOW64 でサポートされています。  

  
### <a name="features-supported-on-32-bit-client-operating-systems"></a>32 ビット クライアント オペレーティング システムでサポートされている機能 
 Windows 10 や Windows 8.1 など、Windows クライアント オペレーティング システムは 32 ビットまたは 64 ビットのアーキテクチャとして利用できます。   すべての SQL Server 機能は 64 ビット クライアント オペレーティング システムでサポートされています。 サポートされている 32 ビット クライアント オペレーティング システムでは、マイクロソフトは次の機能をサポートします。  
  
-   Data Quality クライアント
-   クライアント ツール接続
-   Integration Services
-   クライアント ツールの旧バージョンとの互換性
-   クライアント ツール SDK
-   Documentation コンポーネント
-   分散再生コンポーネント
-   分散再生コントローラー
-   分散再生クライアント
-   SQL クライアント接続 SDK
  
 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 以降のサーバー オペレーティング システムは 32 ビットのアーキテクチャとして利用できません。 サポートされているサーバー オペレーティング システムはすべて 64 ビットのみを利用できます。 すべての機能は 64 ビット サーバー オペレーティング システムでサポートされています。  


##  <a name="cross-language-support"></a><a name="CrossLanguageSupport"></a> 言語間サポート  
 各言語にローカライズされた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールする場合の言語間サポートと注意点の詳細については、「 [SQL Server のローカル言語版](../../sql-server/install/local-language-versions-in-sql-server.md)」を参照してください。  
  
##  <a name="disk-space-requirements"></a><a name="HardDiskSpace"></a> ディスク領域の要件  
 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]のインストール中は、Windows インストーラーによってシステム ドライブ上に一時ファイルが作成されます。 したがって、セットアップを実行して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をインストールまたはアップグレードする前に、これらの一時ファイル用に 6.0 GB 以上の空き容量がシステム ドライブにあることを確認してください。 この要件は、既定以外のドライブに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントをインストールする場合にも適用されます。  
  
 実際に必要なハード ディスク空き容量は、システム構成と、インストールする機能によって異なります。 次の表は、 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] の各コンポーネントに必要なディスク空き容量を示しています。  
  
|**機能**|**必要なディスク空き容量**|  
|-----------------|--------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] とデータ ファイル、レプリケーション、フルテキスト検索、および Data Quality Services|1480 MB|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] (上記と同じ) と R Services (データベース内)|2744 MB|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] (上記と同じ) と外部データ用 PolyBase クエリ サービス|4194 MB|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] およびデータ ファイル|698 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|967 MB|  
|[!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] (スタンドアロン)|280 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - SharePoint|1203 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 製品用アドイン|325 MB|  
|[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]|121 MB|  
|クライアント ツール接続|328 MB|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|306 MB|  
|クライアント コンポーネント ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブック コンポーネントと Integration Services ツール以外)|445 MB|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|280 MB|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブック コンポーネント (ヘルプ コンテンツを表示し、管理する)*|27 MB|  
|すべての機能|8030 MB|  
  
 *ダウンロードされるオンライン ブック コンテンツに必要なディスク領域は 200 MB です。  
  
##  <a name="storage-types-for-data-files"></a><a name="StorageTypes"></a> データ ファイルのストレージの種類  
 データ ファイルでサポートされているストレージの種類は、次のとおりです。  
  
-   ローカル ディスク 
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は現在、標準のネイティブ セクター サイズである 512 バイトと 4 KB のディスク ドライブに対応しています。  ハード ディスクのセクター サイズが 4 KB を超える場合、それに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ ファイルを格納しようとするとエラーが発生することがあります。  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でサポートされているハード ディスク セクターのサイズに関する詳細については、[SQL Server でのハード ディスク ドライブ セクターのサイズのサポート範囲](https://support.microsoft.com/kb/926930)に関するページを参照してください。 
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターのインストールでは、tempdb ファイルをインストールする場合のみローカル ディスクがサポートされます。 tempdb のデータ ファイルおよびログ ファイルに指定されたパスが、すべてのクラスター ノードで有効であることを確認してください。 フェールオーバー中に、tempdb のディレクトリがフェールオーバーのターゲット ノード上で利用できない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リソースはオンラインへの移行に失敗します。
-   ストレージの共有  
-   [記憶域スペース ダイレクト \(S2D\)](/windows-server/storage/storage-spaces/storage-spaces-direct-overview)  
-   SMB ファイル共有  
    - スタンドアロン インストールやクラスター化されたインストールでは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ ファイルに対して SMB ストレージはサポートされていません。 代わりに、直接アタッチされたストレージ、ストレージ エリア ネットワーク、または S2D を使用してください。 
    - SMB ストレージは、Windows ファイル サーバーまたはサード パーティ SMB ストレージ デバイスによってホストされます。 Windows ファイル サーバーが使用される場合、Windows ファイル サーバーのバージョンは 2008 以降である必要があります。 ストレージ オプションとして SMB ファイル共有をとして使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストールの詳細については、「 [SQL Server をストレージ オプションとして SMB ファイル共有にインストールする](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md)のインストールおよび実行に必要な最低限のハードウェア要件とソフトウェア要件について説明します。  
  
  
  
##  <a name="installing-ssnoversion-on-a-domain-controller"></a><a name="DC_support"></a>ドメイン コントローラーへの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール  
 セキュリティ上の理由から、ドメイン コントローラーには [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] をインストールしないことをお勧めします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ時にインストールが中止されることはありませんが、次の制限事項が適用されます。  
  
-   ローカル サービス アカウントを使用して、ドメイン コントローラー上で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを実行することはできません。    
-   コンピューターに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールした後で、そのコンピューターをドメイン メンバーからドメイン コントローラーに変更することはできません。 ホスト コンピューターをドメイン コントローラーに変更する前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をアンインストールする必要があります。    
-   コンピューターに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールした後で、そのコンピューターをドメイン コントローラーからドメイン メンバーに変更することはできません。 ホスト コンピューターをドメイン メンバーに変更する前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をアンインストールする必要があります。   
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスは、クラスター ノードがドメイン コントローラーの場合はサポートされません。   
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、読み取り専用ドメイン コントローラーではサポートされません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップでは、読み取り専用ドメイン コントローラーにセキュリティ グループを作成したり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントを準備したりすることはできません。 この場合、セットアップは失敗します。 

  > [!NOTE]
  > この制限は、ドメイン メンバー ノードへのインストールにも適用されます。

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスは、読み取り専用ドメイン コントローラーのみにアクセスできる環境ではサポートされません。 

  > [!NOTE]
  > この制限は、ドメイン メンバー ノードへのインストールにも適用されます。

## <a name="installation-media"></a>インストール メディア

関連するインストール メディアは、次の場所から入手できます。 
  
- [SQL Server 評価センター](https://www.microsoft.com/evalcenter/evaluate-sql-server-2017-rtm)
- [最新の累積的な更新プログラム](../../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md)

[SQL Server を既に実行している Azure 仮想マシン](/azure/virtual-machines/windows/sql/quickstart-sql-vm-create-portal)を作成することもできます。しかし、仮想マシン上の SQL Server は、仮想化のオーバーヘッドのためにネイティブで実行するよりも低速になります。
  
  
## <a name="next-steps"></a>次のステップ

SQL Server のインストールのためのハードウェアとソフトウェアの要件を確認したら、[SQL Server のインストール計画](../../sql-server/install/planning-a-sql-server-installation.md)を開始したり、[SQL Server のセキュリティに関する考慮事項](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)を確認したりできます。