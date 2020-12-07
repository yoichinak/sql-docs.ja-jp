---
title: 可用性グループ リスナーに接続する
description: プライマリ レプリカや読み取り専用のセカンダリ レプリカへの接続方法、TLS/SSL や Kerberos の使用方法など、Always On 可用性グループ リスナーへの接続について説明します。
ms.custom: contperfq1
ms.date: 02/27/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- read-only routing
- read-intent connections [AlwaysOn Availability Groups]
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], read-only routing
- Availability Groups [SQL Server], client connectivity
ms.assetid: 76fb3eca-6b08-4610-8d79-64019dd56c44
author: cawrites
ms.author: chadam
ms.openlocfilehash: b26671e24cb0419f6737d1f41a5eb2a168dcfe7b
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584236"
---
# <a name="connect-to-an-always-on-availability-group-listener"></a>Always On 可用性グループ リスナーに接続する 
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  
[可用性グループ リスナーを構成](create-or-configure-an-availability-group-listener-sql-server.md)したら、接続文字列を更新して Always On 可用性グループ リスナーに接続する必要があります。 これにより、すべてのフェールオーバー後に接続文字列を手動で更新しなくても、アプリケーションから目的のレプリカに自動的にトラフィックがルーティングされます。 
  

##  <a name="connect-to-the-primary-replica"></a><a name="ConnectToPrimary"></a> プライマリ レプリカに接続する  

読み取り/書き込みアクセスでプライマリ レプリカに接続するには、可用性グループ リスナーの DNS 名を接続文字列で指定します。 

たとえば、リスナーを介して SQL Server Management Studio のプライマリ レプリカに接続するには、サーバー名フィールドにリスナー DNS 名を入力します。 

![SSMS のリスナーに接続する](media/listeners-client-connectivity-application-failover/connect-to-listener-in-ssms.png)


フェールオーバー中にプライマリ レプリカが変更されると、リスナーへの既存の接続が切断され、新しい接続が新しいプライマリ レプリカにルーティングされます。  

ADO.NET プロバイダー (System.Data.SqlClient) の基本的な接続文字列の例を次に示します。 
  
```  
Server=tcp: AGListener,1433;Database=MyDB;Integrated Security=SSPI  
```  

次の Transact-SQL (T-SQL) コマンドを実行して、リスナーを介して現在接続されているレプリカを確認できます。

```sql
SELECT @@SERVERNAME
```

たとえば、SQLVM1 が自分のプライマリ レプリカの場合は、次のようになります。 

![レプリカの接続を確認する](media/listeners-client-connectivity-application-failover/replica-server-name.png)


可用性グループ リスナーを使用する代わりに、プライマリ レプリカまたはセカンダリ レプリカのインスタンス名を使用して、SQL Server のインスタンスに引き続き直接接続することもできます。 ただし、新しい接続が新しい現在のプライマリ レプリカに自動的にルーティングされるという利点がなくなります。 さらに、`read-intent` で指定された接続が読み取り可能なセカンダリ レプリカに自動的にルーティングされる、読み取り専用ルーティングの利点は失われます。 

##  <a name="connect-to-a-read-only-replica"></a><a name="ConnectToSecondary"></a> 読み取り専用レプリカに接続する 

"_読み取り専用ルーティング_" とは、読み取り専用ワークロードを許可するように構成されている読み取り可能なセカンダリ レプリカに、着信リスナー接続を自動的にルーティングすることを意味します。 

次の条件に該当する場合、接続は読み取り専用レプリカに自動的にルーティングされます。 
 
-   少なくとも 1 つのセカンダリ レプリカが読み取り専用アクセスに設定され、各読み取り専用セカンダリ レプリカとプライマリ レプリカが[読み取り専用ルーティングをサポートするように構成されている](configure-read-only-routing-for-an-availability-group-sql-server.md)。 

-   接続文字列は、可用性グループに含まれるデータベースを参照します。 これに代わる方法は、接続に使うログインで、データベースを既定のデータベースとして構成することです。 詳しくは、[読み取り専用ルーティングでのアルゴリズムの動作に関するこちらの記事](/archive/blogs/mattn/calculating-read_only_routing_url-for-alwayson)をご覧ください。

-   接続文字列は可用性グループ リスナーを参照し、着信接続のアプリケーションの目的が読み取り専用に設定されている (たとえば、ODBC または OLEDB の接続文字列、接続属性、またはプロパティで **Application Intent=ReadOnly** キーワードを使用している)。 

アプリケーションの目的の属性は、ログイン中にクライアントのセッションに格納されます。その後、SQL Server のインスタンスがこの目的を処理し、可用性グループの構成およびセカンダリ レプリカ内のターゲット データベースの現在の読み取り/書き込み状態に基づいて、実行する操作を決定します。  

たとえば、SQL Server Management Studio を使用して読み取り専用レプリカに接続するには、 **[サーバーに接続]** ダイアログ ボックスで **[オプション]** を選択し、 **[追加の接続パラメーター]** タブを選択して、テキストボックスに `ApplicationIntent=ReadOnly` を指定します。

![SSMS の読み取り専用接続](media/listeners-client-connectivity-application-failover/read-only-intent-in-ssms.png)
  
読み取り専用のアプリケーションの目的を指定する ADO.NET プロバイダー (System.Data.SqlClient) の接続文字列の例を次に示します。 

```  
Server=tcp:AGListener;Database=AdventureWorks;Integrated Security=SSPI;ApplicationIntent=ReadOnly  
```  
  
詳細については、[可用性レプリカでの読み取り専用アクセスの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)に関するページを参照してください。  

## <a name="non-default-port"></a>既定以外のポート

リスナーを作成するときに、リスナーで使用するポートを指定します。 ポートが既定のポート 1433 である場合は、リスナーに接続するときにポート番号を指定する必要はありません。 ただし、ポートが 1433 以外の場合は、次のように `listenername,port` の形式の接続文字列でポートを指定する必要があります。

![既定以外のポートを使用して接続する](media/listeners-client-connectivity-application-failover/specify-port-in-ssms.png)

リスナーの既定以外のポートを指定する ADO.NET プロバイダー (System.Data.SqlClient) の接続文字列の例を次に示します。 

```  
Server=tcp:AGListener,1445;Database=AdventureWorks;Integrated Security=SSPI 
```  

##  <a name="bypass-listeners"></a><a name="BypassAGl"></a> リスナーをバイパスする  

可用性グループ リスナーでフェールオーバー リダイレクトと読み取り専用ルーティングが有効にされている場合、クライアント接続でこれらを使用する必要はありません。 また、クライアント接続は、可用性グループ リスナーに接続する代わりに、SQLServer のインスタンスを直接参照できます。  
  
SQL Server のインスタンスにとって、接続のログインで、可用性グループ リスナーまたは他のインスタンス エンドポイントのどちらを使用するかは関係ありません。  SQL Server のインスタンスは、接続先データベースの状態を確認し、可用性グループの構成およびインスタンス上のデータベースの現在の状態に基づいて、接続を許可または禁止します。  たとえば、クライアント アプリケーションが SQL Server ポートのインスタンスに直接接続し、可用性グループでホストされているターゲット データベースに接続する場合、ターゲット データベースがプライマリ状態でオンラインであれば接続は成功します。  ターゲット データベースがオフラインまたは移行状態の場合は、データベースへの接続が失敗します。  
  
データベース ミラーリングを [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]に移行している間、セカンダリ レプリカが 1 つしか存在せず、これにユーザーが接続できない場合は、アプリケーションでデータベース ミラーリング接続文字列を指定できます。 

##  <a name="database-mirroring-connection-strings"></a><a name="DbmConnectionString"></a> データベース ミラーリングの接続文字列 
 可用性グループに 1 つしかセカンダリ レプリカが存在せず、さらに、その可用性グループが、セカンダリ レプリカに ALLOW_CONNECTIONS = READ_ONLY または ALLOW_CONNECTIONS = NONE が構成されている場合、クライアントは、データベース ミラーリングの接続文字列を使用してプライマリ レプリカに接続できます。 可用性グループに存在する可用性レプリカが 2 つだけ (プライマリ レプリカおよび 1 つのセカンダリ レプリカ) であれば、既存のアプリケーションをデータベース ミラーリングから可用性グループに移行する際にこの方法を用いることができます。 セカンダリ レプリカをさらに追加する場合は、可用性グループの可用性グループ リスナーを作成し、その可用性グループ リスナー DNS 名を使用するようにアプリケーションを更新する必要があります。  
  
 データベース ミラーリングの接続文字列を使用する際、クライアントは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client または .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]を使用できます。 クライアントが指定する接続文字列には、最低限、1 つのサーバー インスタンスの名前 ( *イニシャル パートナー名*) が指定されている必要があります。接続先の可用性レプリカを初期状態でホストするサーバー インスタンスは、この名前によって識別されます。 接続文字列には、必要に応じて、別のサーバー インスタンスの名前を指定することもできます。これを *フェールオーバー パートナー名* といい、初期状態でセカンダリ レプリカをホストするサーバー インスタンスは、フェールオーバー パートナー名として識別されます。  
  
 データベース ミラーリングの接続文字列の詳細については、「 [データベース ミラーリング セッションへのクライアントの接続 &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)」を参照してください。  
  
  
##  <a name="multi-subnet-failovers"></a><a name="SupportAgMultiSubnetFailover"></a> マルチサブネット フェールオーバー  
 
 接続文字列で MultiSubnetFailover 接続オプションをサポートするクライアント ライブラリを使用している場合、MultiSubnetFailover を "True" または "Yes" に設定して (使用しているプロバイダーの構文によって異なります)、別のサブネットへの可用性グループのフェールオーバーを最適化できます。  
  
> [!NOTE]  
>  可用性グループ リスナーおよび SQL Server フェールオーバー クラスター インスタンス名への単一サブネット接続およびマルチサブネット接続の両方に対して、この設定を推奨します。  このオプションを有効にすると、単一サブネットのシナリオでも、さらに最適化されます。  
  
 **MultiSubnetFailover** 接続オプションは TCP ネットワーク プロトコルのみで機能します。また、可用性グループ リスナーに接続する場合、および [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]に接続している仮想ネットワーク名を使用する場合にのみサポートされます。  
  
 マルチサブネット フェールオーバーを有効にする ADO.NET プロバイダー (System.Data.SqlClient) の接続文字列の例を次に示します。  
  
```  
Server=tcp:AGListener,1433;Database=AdventureWorks;Integrated Security=SSPI; MultiSubnetFailover=True  
```  
  
 **MultiSubnetFailover** 接続オプションは、可用性グループが単一のサブネットのみにある場合でも、 **True** に設定することをお勧めします。  これにより、今後、クライアント接続文字列を変更することなく、複数のサブネットをサポートするように新しいクライアントをあらかじめ構成することができ、単一サブネットのフェールオーバーのパフォーマンスも最適化できます。  **MultiSubnetFailover** 接続オプションは必須ではありませんが、サブネットのフェールオーバーが速くなるという利点があります。  これは、クライアント ドライバーが、可用性グループに関連付けられている各 IP アドレスの TCP ソケットを同時に開こうとするためです。  クライアント ドライバーは、最初の IP が正常に応答するのを待ち、応答した場合は、その IP を接続に使用します。  
  
##  <a name="listeners--tlsssl-certificates"></a><a name="SSLcertificates"></a> リスナーと TLS/SSL 証明書  

可用性グループ リスナーへの接続時に、参加している SQL Server のインスタンスがセッションの暗号化と共に TLS/SSL 証明書を使用していることがあります。この場合、強制的に暗号化するために、接続クライアント ドライバーが TLS/SSL 証明書のサブジェクト代替名をサポートする必要があります。  SQL Server ドライバーでの証明書のサブジェクト代替名のサポートは、ADO.NET (SqlClient)、Microsoft JDBC、および SQL Native Client (SNAC) に対して計画されています。  
  
X.509 証明書は、すべての可用性グループ リスナー セットのリストを証明書のサブジェクト代替名に設定して、フェールオーバー クラスターに参加している各サーバー ノードに対して構成する必要があります。 

証明書の値の形式は次のとおりです。 

```  
CN = Server.FQDN  
SAN = Server.FQDN,Listener1.FQDN,Listener2.FQDN
```

たとえば、次のような値があるとします。 

```
Servername: Win2019   
Instance: SQL2019   
AG: AG2019   
Listener: Listener2019   
Domain: contoso.com  (which is also the FQDN)
```

可用性グループが 1 つだけの WSFC の場合、証明書には、サーバーの完全修飾ドメイン名 (FQDN) とリスナーの FQDN が含まれている必要があります。 

```
CN: Win2019.contoso.com
SAN: Win2019.contoso.com, Listener2019.contoso.com 
```

この構成では、インスタンス (`WIN2019\SQL2019`) またはリスナー (`Listener2019`) に接続するときに、接続が暗号化されます。 

ネットワークの構成方法によっては、SAN にも NetBIOS を追加することが必要な場合がある、顧客の小さいサブセットが存在します。 この場合、証明書の値は次のようになります。 

```
CN: Win2019.contoso.com
SAN: Win2019,Win2019.contoso.com,Listener2019,Listener2019.contoso.com
```

WSFC に次のような 3 つの可用性グループ リスナーがあるとします: Listener1、Listener2、Listener3

この場合は、証明書の値は次のようになります。 

```
CN: Win2019.contoso.com
SAN: Win2019.contoso.com,Listener1.contoso.com,Listener2.contoso.com,Listener3.contoso.com
```
  
  
##  <a name="listeners-and-kerberos-spns"></a><a name="SPNs"></a> リスナーと Kerberos (SPN) 

ドメイン管理者は、リスナーへのクライアント接続のために Kerberos を有効にするように、可用性グループリスナーごとに Active Directory のサービス プリンシパル名 (SPN) を構成する必要があります。 SPN が登録されている場合は、可用性レプリカをホストするサーバー インスタンスのサービス アカウントを使用する必要があります。 SPN がすべてのレプリカで機能するためには、可用性グループをホストする WSFC クラスター内のすべてのインスタンスで同じサービス アカウントを使用する必要があります。  
  
 SPN は、Windows コマンド ライン ツールの **setspn** を使用して構成します。  たとえば、 `AG1listener.Adventure-Works.com` というドメイン アカウントで実行されるように構成された、一連の SQL Server インスタンスでホストされている `corp\svclogin2`という名前の可用性グループの SPN を構成する場合は、次のようになります。  
  
```  
setspn -A MSSQLSvc/AG1listener.Adventure-Works.com:1433 corp\svclogin2  
```  
  
 SQL Server の SPN の手動登録の詳細については、「 [Kerberos 接続用のサービス プリンシパル名の登録](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)」を参照してください。  
  


## <a name="next-steps"></a>次のステップ

リスナーに正常に接続したら、パフォーマンスを向上させるために、[読み取り専用ワークロード](overview-of-always-on-availability-groups-sql-server.md)と[バックアップ](configure-backup-on-availability-replicas-sql-server.md)をセカンダリ レプリカにオフロードすることを検討してください。 また、可用性グループの正常性を確保するために、さまざまな[可用性グループの監視戦略](monitoring-of-availability-groups-sql-server.md)を確認することもできます。 

可用性グループの詳細については、「[Always On 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)」を参照してください。