---
title: 可用性グループ リスナーとは
description: 'Always On 可用性グループ リスナーの概要と、目的のサーバーにトラフィックを自動的に転送するためにそれがどのように機能するかについて説明します。 '
ms.custom: seodec18
ms.date: 02/27/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
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
ms.openlocfilehash: aa84b43cbcf636facdade77040eeadf7e8449c54
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584694"
---
# <a name="what-is-an-availability-group-listener"></a>可用性グループ リスナーとは  
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

可用性グループ リスナーは、Always On 可用性グループのプライマリ レプリカまたはセカンダリ レプリカ内のデータベースにアクセスするために、クライアントが接続できる仮想ネットワーク名 (VNN) です。 リスナーを使用すると、クライアントは、SQL Server の物理インスタンス名を知らなくても、レプリカに接続できます。 リスナーはトラフィックをルーティングするため、フェールオーバーの発生後にクライアント接続文字列を変更する必要はありません。 

可用性グループ リスナーには、ドメイン ネーム システム (DNS) のリスナー名、リスナー ポート指定、および 1 つ以上の IP アドレスが含まれます。 可用性グループ リスナーでは、TCP プロトコルのみがサポートされています。  リスナーの DNS 名が、ドメインおよび NetBIOS 内で一意である必要があります。  リスナーを作成すると、それは関連付けられた仮想ネットワーク名 (VNN)、仮想 IP (VIP)、可用性グループの依存関係と共に、クラスター内のリソースになります。 クライアントは、DNS を使用して VNN を複数の IP アドレスに解決した後、接続要求が成功するかタイムアウトするまで、それぞれのアドレスに接続を試みます。  
  
1 つ以上の[読み取り可能なセカンダリ レプリカ](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)に対して読み取り専用のルーティングが構成されている場合、リスナーに対する読み取りを目的としたクライアント接続は読み取り可能なセカンダリ レプリカに自動的にリダイレクトされます。 
  
この記事では、可用性グループ リスナーの概要を示します。 [リスナーを構成](create-or-configure-an-availability-group-listener-sql-server.md)し、[リスナーに接続する](listeners-client-connectivity-application-failover.md)方法を学習することもできます。
  
  
##  <a name="listener-parameters"></a><a name="AGlConfig"></a> リスナーのパラメーター  

 可用性グループ リスナーでは、以下のものが使用されます。
  
 **一意の DNS 名**  
 これは仮想ネットワーク名 (VNN) とも呼ばれています。 DNS ホスト名に対する Active Directory の名前付け規則が適用されます。 詳細については、サポート技術情報の「 [Active Directory でのコンピューター、ドメイン、サイト、および OU の名前付け規則](https://support.microsoft.com/kb/909264) 」を参照してください。  
  
**1 つまたは複数の仮想 IP アドレス (VIP)**  
 VIP は、可用性グループがフェールオーバーする 1 つ以上のサブネットに対して構成されます。  
  
**IP アドレスの構成**  
 特定の可用性グループ リスナーの IP アドレスには、動的ホスト構成プロトコル (DHCP) または 1 つまたは複数の静的 IP アドレスを使用できます。 DHCP を使用すると、フェールオーバー中に接続の遅延が発生する可能性があるため、運用環境での使用はお勧めできません。 複数のサブネットにまたがって拡張される可用性グループ、またはハイブリッド ネットワーク構成を使用する可用性グループは、静的 IP アドレスを使用する必要があります。 
 
  
##  <a name="listener-port"></a><a name="SelectListenerPort"></a> リスナー ポート 
 可用性グループ リスナーを構成する場合は、ポートを指定する必要があります。  既定のポートを 1433 に構成すると、クライアント接続文字列をシンプルにできます。 1433 を使用する場合は、接続文字列でポート番号を指定する必要がありません。 また、各可用性グループ リスナーに個別の仮想ネットワーク名があるため、1 つの WSFC で構成された各可用性グループ リスナーが同じ既定のポート 1433 を参照するように構成できます。  
  
 標準ではないリスナー ポートを指定することもできます。ただし、その場合、可用性グループ リスナーに接続するたびに、接続文字列で接続先ポートを明示的に指定する必要があります。  また、標準以外のポートに対して、ファイアウォールのアクセス許可を有効にする必要があります。  
  
 可用性グループ リスナー VNN で既定のポート 1433 を使用する場合、クラスター ノード上の他のサービスがそのポートを使用していないことを確認する必要があります。確認しない場合、ポートの競合が発生する可能性があります。  
  
 SQL Server のインスタンスの 1 つが、インスタンス リスナーを通じて TCP ポート 1433 を既にリッスンしていて、コンピューター上の他のサービス (SQL Server の別のインスタンスを含む) がポート 1433 をリッスンしていない場合は、可用性グループ リスナーでポートの競合は発生しません。  これは、可用性グループ リスナーが同じサービス プロセス内で同じ TCP ポートを共有できるためです。  ただし、同じポートをリッスンするように、SQL Server の複数のインスタンス (サイド バイ サイド) を構成しないでください。  
  
  
##  <a name="behavior-of-client-connections-on-failover"></a><a name="CCBehaviorOnFailover"></a> フェールオーバー時のクライアント接続動作  

 可用性グループのフェールオーバーが発生すると、可用性グループへの既存の永続的な接続は終了します。このため、クライアントが、同じプライマリ データベースまたは読み取り専用セカンダリ データベースとの連携を保つには、新しい接続を確立する必要があります。  フェールオーバーがサーバー側で発生している間は、可用性グループへの接続が失敗することがあります。この場合、プライマリが完全にオンラインになるまで、クライアント アプリケーションは接続を再試行します。  
  
 クライアント アプリケーションの接続の試行中、接続のタイムアウト期間が経過する前に可用性グループがオンラインに戻ると、クライアント ドライバーによる内部での再試行のいずれかが正常に接続できる場合があります。このとき、アプリケーションでエラーは発生しません。  


## <a name="next-steps"></a>次のステップ

これで、可用性グループ リスナーがどのように機能するか、[リスナーの作成](create-or-configure-an-availability-group-listener-sql-server.md)方法、[リスナーに接続](listeners-client-connectivity-application-failover.md)するようにアプリケーションを構成する方法について理解しました。 また、可用性グループの正常性を確保するために、さまざまな[可用性グループの監視戦略](monitoring-of-availability-groups-sql-server.md)を確認することもできます。 

可用性グループの詳細については、「[Always On 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)」を参照してください。 
  

  
  
