---
title: 暗号化された接続を有効にする | Microsoft Docs
ms.custom: contperfq4
ms.date: 08/29/2019
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
description: 通信チャネル全体でデータを暗号化します。 SQL Server 構成マネージャーを使用して、SQL Server データベース エンジンのインスタンスに対して暗号化された接続を有効にします。
helpviewer_keywords:
- connections [SQL Server], encrypted
- SSL [SQL Server]
- Secure Sockets Layer (SSL)
- TLS [SQL Server]
- Transport Layer Security (TLS)
- encryption [SQL Server], connections
- cryptography [SQL Server], connections
- certificates [SQL Server], installing
- requesting encrypted connections
- installing certificates
- security [SQL Server], encryption
- TLS certificates
ms.assetid: e1e55519-97ec-4404-81ef-881da3b42006
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: d147177be88db5bba50955711a8585ff11d872d9
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670972"
---
# <a name="enable-encrypted-connections-to-the-database-engine"></a>データベース エンジンへの暗号化接続の有効化

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  通信チャネル全体でデータを暗号化する方法について説明します。  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] インスタンスへの暗号化接続を有効化し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して証明書を指定します。
 
 サーバー コンピューターには、証明書がプロビジョニングされている必要があります。 サーバー コンピューターで証明書をプロビジョニングするには、Windows に[証明書をインポート](#single-server)します。 クライアント コンピューターは、[証明書のルート証明機関を信頼](#about)するように設定する必要があります。  
  
> [!IMPORTANT]
> SSL (Secure Sockets Layer) は、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降では廃止されています。 代わりに、トランスポート層セキュリティ (TLS) を使用してください。

## <a name="transport-layer-security-tls"></a>トランスポート層セキュリティ (TLS)

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でトランスポート層セキュリティ (TLS) を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスとクライアント アプリケーション間でネットワーク送信されるデータを暗号化できます。 TSL 暗号化はプロトコル レイヤー内で実行され、サポートされるすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアントがこれを使用できます。

TSL は、クライアント接続で暗号化が要求された場合のサーバー検証に使用できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが公的な証明機関から証明書を割り当てられたコンピューターで実行されている場合、そのコンピューターの ID と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスは、信頼されているルート機関につながる証明書のチェーンにより保証されます。 このようなサーバー検証では、サーバーが使用する証明書のルート機関が信頼されるよう、クライアント アプリケーションが実行されているコンピューターが構成されている必要があります。 

自己署名証明書を使用して暗号化を行うことは可能であり、次のセクションで説明していますが、自己署名証明書が提供する保護には制限があります。
TLS で使用される暗号化のレベル (40 ビットまたは 128 ビット) は、アプリケーション コンピューターとデータベース コンピューターで実行されている Microsoft Windows オペレーティング システムのバージョンによって異なります。

> [!WARNING]
> 40 ビットの暗号化レベルの使用は、安全でないと見なされています。

> [!WARNING]
> 自己署名証明書を使用して暗号化される TLS 接続では、強力なセキュリティは提供されません。 man-in-the-middle (中間者) 攻撃を受ける可能性が高くなります。 実稼働環境やインターネットに接続しているサーバーでは、自己署名証明書を使用した TLS 接続は使用しないことをお勧めします。

TLS 暗号化を有効にすると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスとアプリケーション間でネットワーク送信されるデータのセキュリティが強化されます。 ただし、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] とクライアント アプリケーション間のすべてのトラフィックが TLS で暗号化される場合は、次の追加処理が必要です。
-  接続時に、追加のネットワーク ラウンドトリップが必要です。
-  アプリケーションから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに送信されたパケットは、クライアント TLS スタックによって暗号化され、サーバー TLS スタックによって暗号化解除される必要があります。
-  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスからアプリケーションに送信されたパケットは、サーバー TLS スタックによって暗号化され、クライアント TLS スタックによって暗号化解除される必要があります。

## <a name="about-certificates"></a><a name="about"></a>証明書について

 **サーバー認証**用の証明書が発行されている必要があります。 証明書の名前は、コンピューターの完全修飾ドメイン名 (FQDN) である必要があります。  
  
 証明書は、コンピューター上のユーザーにローカルに格納されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が使用する証明書をインストールするには、ローカル管理者特権を持つアカウントで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを実行している必要があります。

 クライアントは、サーバーが使用する証明書の所有権を検証できる必要があります。 サーバー証明書に署名した証明機関の公開キー証明書をクライアントが持っている場合は、それ以上の構成は必要ありません。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows には、多くの証明機関の公開キー証明書が含まれています。 サーバー証明書に署名した公的または私的な証明機関に対する公開キー証明書をクライアントが持っていない場合は、サーバー証明書に署名した証明機関の公開キー証明書をインストールする必要があります。  
  
> [!NOTE]  
> フェールオーバー クラスターで暗号化を使用する場合、フェールオーバー クラスター内のすべてのノードに対して、仮想サーバーの完全修飾 DNS 名を使用してサーバー証明書をインストールする必要があります。 たとえば、***test1.\*\<your company>\*.com*** および ***test2.\*\<your company>\*.com*** というノードを持つ 2 ノードのクラスターと、***virtsql*** という仮想サーバーがあるとします。この場合、***virtsql.\*\<your company>\*.com*** の証明書を両方のノードにインストールする必要があります。 **[SQL Server ネットワークの構成]** の **[virtsql のプロトコル]** プロパティ ボックスの **[強制的に暗号化]** オプションを **[はい]** に設定します。

> [!NOTE]
> Azure VM 上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への Azure Search インデクサーからの暗号化接続を作成するには、「[Azure VM での Azure Search インデクサーから SQL Server への接続の構成](/azure/search/search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers)」を参照してください。 

## <a name="certificate-requirements"></a>証明書の要件

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で TLS 証明書を読み込むには、証明書が次の条件を満たしている必要があります。

- 証明書がローカル コンピューターの証明書ストアまたは現在のユーザーの証明書ストアに存在すること。

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のサービス アカウントに、TLS 証明書にアクセスするアクセス許可があること。

- 現在のシステム時刻が証明書の **[有効期間の開始]** プロパティから証明書の **[有効期間の終了]** プロパティまでの範囲にあること。

- 証明書がサーバー認証に使用されていること。 つまり、証明書の **[拡張キー使用法]** プロパティで **[サーバー認証] (1.3.6.1.5.5.7.3.1)** が指定されている必要があります。

- 証明書が **AT_KEYEXCHANGE** の **KeySpec** オプションを使用して作成されていること。 通常、証明書のキー使用法プロパティ (**KEY_USAGE**) には、キーの暗号化 (**CERT_KEY_ENCIPHERMENT_KEY_USAGE**) も含まれます。

- 証明書の **Subject** プロパティで、共通名 (CN) がサーバー コンピューターのホスト名または完全修飾ドメイン名 (FQDN) と同一であると示されていること。 ホスト名を使用するときは、証明書で DNS サフィックスを指定する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がフェールオーバー クラスターで実行されている場合、共通名は仮想サーバーのホスト名または FQDN と同じである必要があり、証明書がフェールオーバー クラスター内のすべてのノードにプロビジョニングされる必要があります。

- ワイルドカード証明書は、[!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] および [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] Native Client (SNAC) でサポートされています。 その後、SNAC は廃止され、[Microsoft OLE DB Driver for SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) と [Microsoft ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md) に置き換わりました。 他のクライアントでは、ワイルドカード証明書がサポートされていない可能性があります。 詳細については、クライアントのドキュメントと [KB 258858](https://support.microsoft.com/kb/258858) を参照してください。       
  SQL Server 構成マネージャーを使用して、ワイルドカード証明書を選択することはできません。 ワイルドカード証明書を使うには、`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQLServer\SuperSocketNetLib` のレジストリ キーを編集し、**Certificate** の値に証明書の拇印を (スペースを含めずに) 入力する必要があります。  

  > [!WARNING]  
  > [!INCLUDE[ssnoteregistry_md](../../includes/ssnoteregistry-md.md)]  

## <a name="install-on-single-server"></a><a name="single-server"></a>単一サーバーへのインストール

[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] で、SQL Server 構成マネージャーに証明書の管理が統合されました。 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] の SQL Server 構成マネージャーは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の以前のバージョンで使用できます。 単一の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに証明書を追加する方法については、「[証明書の管理 (SQL Server 構成マネージャー)](../../database-engine/configure-windows/manage-certificates.md)」を参照してください。

[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] を介して [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] を使用する場合に、[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] の SQL Server 構成マネージャーが使用できない場合は、次の手順に従ってください。

1. **[スタート]** メニューの **[ファイル名を指定して実行]** をクリックし、 **[名前]** ボックスに「 **MMC** 」と入力して **[OK]** をクリックします。  
  
2. MMC コンソールの **[ファイル]** メニューで、 **[スナップインの追加と削除]** をクリックします。  
  
3. **[スナップインの追加と削除]** ダイアログ ボックスで **[追加]** をクリックします。  
  
4. **[スタンドアロン スナップインの追加]** ダイアログ ボックスで **[証明書]** をクリックし、次に **[追加]** をクリックします。  
  
5. **[証明書スナップイン]** ダイアログ ボックスで **[コンピューター アカウント]** をクリックし、 **[完了]** をクリックします。  
  
6. **[スタンドアロン スナップインの追加]** ダイアログ ボックスで **[閉じる]** をクリックします。  
  
7. **[スナップインの追加と削除]** ダイアログ ボックスで **[OK]** をクリックします。  
  
8. **[証明書]** スナップインで、 **[証明書]** 、 **[個人]** の順に展開し、 **[証明書]** を右クリックします。次に **[すべてのタスク]** をポイントし、 **[インポート]** をクリックします。  

9. インポートした証明書を右クリックし、 **[すべてのタスク]** をポイントして、 **[秘密キーの管理]** をクリックします。 **[セキュリティ]** ダイアログ ボックスで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントが使用するユーザー アカウントに読み取りアクセス許可を追加します。  
  
10. **[証明書のインポート ウィザード]** を完了して証明書をコンピューターに追加し、MMC コンソールを閉じます。 コンピューターへの証明書の追加の詳細については、Windows のマニュアルを参照してください。  

> [!IMPORTANT]
> 運用環境では、証明機関から信頼された証明書を取得することをお勧めします。    
> テスト目的のため、自己署名証明書を使用することもできます。 自己署名証明書を作成するには、[Powershell コマンドレット New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate) または [certreq コマンド](/windows-server/administration/windows-commands/certreq_1)に関するページを参照してください。
  
## <a name="install-across-multiple-servers"></a>複数のサーバーにまたがるインストール

[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] で、SQL Server 構成マネージャーに証明書の管理が統合されました。 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] の SQL Server 構成マネージャーは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の以前のバージョンで使用できます。 フェールオーバー クラスター構成または可用性グループ構成に証明書を追加するには、「[証明書の管理 (SQL Server 構成マネージャー)](../../database-engine/configure-windows/manage-certificates.md)」を参照してください。

[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] を介して [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] を使用する場合に、[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] の SQL Server 構成マネージャーが使用できない場合は、各サーバーに対して、「[1 台のサーバーに証明書をプロビジョニング (インストール) するには](#single-server)」の手順を実行します。

## <a name="export-server-certificate"></a>サーバー証明書のエクスポート  
  
1. **[証明書]** スナップインで、 **[証明書]**  /  **[個人]** フォルダーで証明書を探し、 **[証明書]** を右クリックします。次に **[すべてのタスク]** をポイントし、 **[エクスポート]** をクリックします。  
  
2. **証明書のエクスポート ウィザード**を実行して、証明書ファイルを使いやすい場所に格納します。  
  
## <a name="configure-server"></a>サーバーの構成

暗号化された接続を強制するサーバーを構成します。

> [!IMPORTANT]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サービス アカウントには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で暗号化を強制するために使用される証明書の読み取りアクセス許可が必要です。 特権のないサービス アカウントの場合、読み取りアクセス許可を証明書に追加する必要があります。 この操作に失敗すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを再起動できなくなる可能性があります。
  
1. **SQL Server 構成マネージャー**で、 **[SQL Server ネットワークの構成]** を展開し、 **[** _\<server instance> のプロトコル]_ を右クリックして、 **[プロパティ]** を選択します。  
  
2. **[ _\<instance name>_ のプロトコル]** の **[プロパティ]** ダイアログ ボックスの **[証明書]** タブで、 **[証明書]** ボックスのドロップダウンから必要な証明書を選択し、 **[OK]** をクリックします。  
  
3. **[フラグ]** タブの **[ForceEncryption]** ボックスの一覧の **[はい]** をクリックし、 **[OK]** をクリックしてダイアログ ボックスを閉じます。  
  
4. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを再開します。  

> [!NOTE]
> クライアントとサーバーの間で安全な接続を確立するには、暗号化された接続を要求するようにクライアントを構成します。 詳細については、[この記事の後半で](#configure-client)説明します。

## <a name="configure-client"></a><a name="configure-client"></a>クライアントの構成

暗号化された接続を要求するクライアントを構成します。

1. 元の証明書ファイルまたはエクスポートした証明書ファイルを、クライアント コンピューターにコピーします。  
  
2. クライアント コンピューターで、 **証明書** スナップインを使用して、ルート証明書またはエクスポートした証明書ファイルをインストールします。  
  
3. SQL Server 構成マネージャーを使用する場合、 **[SQL Server Native Client の構成]** を右クリックして、 **[プロパティ]** をクリックします。  
  
4. **[フラグ]** ページの **[プロトコルの暗号化を設定する]** ボックスで、 **[はい]** をクリックします。  
  
## <a name="use-sql-server-management-studio"></a>SQL Server Management Studio の使用 [SQL Server]
  
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] からの接続を暗号化する手順  

1. オブジェクト エクスプローラー ツール バーで **[接続]** をクリックし、 **[データベース エンジン]** をクリックします。  
  
2. **[サーバーへの接続]** ダイアログ ボックスで接続情報を入力し、 **[オプション]** をクリックします。  
  
3. **[接続のプロパティ]** タブで **[暗号化接続]** をクリックします。  

## <a name="internet-protocol-security-ipsec"></a>インターネット プロトコル セキュリティ (IPSec)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータは、IPSec を使用して、転送時に暗号化することができます。 IPSec は、クライアントとサーバーのオペレーティング システムによって提供されます。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は構成する必要がありません。 IPSec の詳細については、Windows のマニュアルまたはネットワークに関するドキュメントを参照してください。

## <a name="next-steps"></a>次のステップ

+ [Microsoft SQL Server の TLS 1.2 サポート](https://support.microsoft.com/kb/3135244)     
+ [SQL Server のアクセスを許可するための Windows ファイアウォールの構成](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)     
+ [Powershell コマンドレット New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate)