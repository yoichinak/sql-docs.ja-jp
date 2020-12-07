---
title: WMI Provider for Server Events の操作
description: WMI Provider for Server Events を使用してプログラミングする場合は、次のガイドラインを考慮してください。 Service Broker、接続文字列、アクセス許可を有効にする方法について説明します。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- event notifications [WMI]
- permissions [WMI]
- connection strings [WMI]
- security [WMI]
- Service Broker [WMI]
- WMI Provider for Server Events, connection strings
- WMI Provider for Server Events, Service Broker
- notifications [WMI]
- WMI Provider for Server Events, security
ms.assetid: cd974b3b-2309-4a20-b9be-7cfc93fc4389
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4c28188a6abada5ff699b8ee759a84c237b8d8e8
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891622"
---
# <a name="working-with-the-wmi-provider-for-server-events"></a>WMI Provider for Server Events の操作
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、WMI Provider for Server Events を使用したプログラミングを行う前に、検討する必要があるガイドラインを示します。  
  
## <a name="enabling-service-broker"></a>Service Broker の有効化  
 WMI Provider for Server Events は、イベントに対する WQL クエリを変換して、対象とするデータベースにイベント通知を作成します。 イベント通知のしくみを理解しておくと、プロバイダーに対してプログラミングを行う際に役立つ場合があります。 詳細については、「 [WMI Provider for Server Events の概念](./wmi-provider-for-server-events-concepts.md)」を参照してください。  
  
 特に、WMI プロバイダーによって作成されたイベント通知は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用してサーバー イベントに関するメッセージを送信するため、イベントが生成される場合は必ずこのサービスが有効化されている必要があります。 サーバー インスタンス上のイベントに対してクエリを実行するプログラムであれば、そのインスタンスの msdb 内の [!INCLUDE[ssSB](../../includes/sssb-md.md)] が有効化されている必要があります。これが、プロバイダーによって作成される対象 [!INCLUDE[ssSB](../../includes/sssb-md.md)] サービス (SQL/Notifications/ProcessWMIEventProviderNotification/v1.0) の拠点になります。 プログラムがデータベース内のイベントまたは特定のデータベース オブジェクト上のイベントに対してクエリを実行する場合、その対象データベース内の [!INCLUDE[ssSB](../../includes/sssb-md.md)] が有効化されている必要があります。 アプリケーションの展開後に対応する [!INCLUDE[ssSB](../../includes/sssb-md.md)] が有効化されていない場合、基になるイベント通知によって生成されたイベントはすべて、イベント通知が使用するサービスのキューに送信されますが、[!INCLUDE[ssSB](../../includes/sssb-md.md)] が有効化されるまで WMI 管理アプリケーションには返されません。  
  
 次のクエリは、サービス インスタンス上で有効化されている Service Broker を調べ、そのブローカー インスタンスの GUID を取得します。  
  
```  
SELECT name, is_broker_enabled, service_broker_guid FROM sys.databases;  
```  
  
 msdb の Service Broker GUID はプロバイダーの対象サービスの拠点であり、特別な意味を持っています。  
  
 データベースでを有効にするには [!INCLUDE[ssSB](../../includes/sssb-md.md)] 、 [ALTER database](../../t-sql/statements/alter-database-transact-sql.md) ステートメントの ENABLE_BROKER SET オプションを使用します。  
  
## <a name="specifying-a-connection-string"></a>接続文字列の指定  
 アプリケーションは、プロバイダーによって定義された WMI 名前空間に接続することによって、WMI Provider for Server Events を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにダイレクトします。 Windows WMI サービスは、この名前空間をプロバイダー DLL である Sqlwep.dll にマップし、これをメモリに読み込みます。 の各インスタンス [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には独自の WMI 名前空間があり、既定ではに設定さ \\ \\ れています。 \\*ルート*\Microsoft\SqlServer\ServerEvents \\ *instance_name*。 の既定のインストールでは、 *instance_name*既定値は MSSQLSERVER [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] です。  
  
## <a name="permissions-and-server-authentication"></a>権限とサーバー認証  
 WMI Provider for Server Events にアクセスするには、WMI 管理アプリケーションの起動元クライアントが、アプリケーションのアプリケーション接続文字列で指定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内の Windows 認証ログインまたはグループに対応している必要があります。  
  
## <a name="permissions-and-event-notification-scope"></a>権限およびイベント通知のスコープ  
 WMI Provider for Server Events は、WQL クエリを対象データベース内のイベント通知に変換します。 このため、呼び出し側アプリケーションは、プロバイダーへのアクセスに必要な最低限の権限に加えて、必要なイベント通知を作成するための正しい権限をデータベース内に持っている必要があります。 必要な権限は次のとおりです。  
  
-   データベース スコープのイベント通知を作成するには、少なくとも、現在のデータベースの CREATE DATABASE DDL EVENT NOTIFICATION 権限が必要です。  
  
-   サーバー スコープの DDL ステートメントに対するイベント通知を作成するには、少なくとも、サーバーの CREATE DDL EVENT NOTIFICATION 権限が必要です。  
  
-   トレース イベントに対するイベント通知を作成するには、少なくとも、サーバーの CREATE TRACE EVENT NOTIFICATION 権限が必要です。  
  
-   キュー スコープされるイベント通知を作成するには、少なくとも、キューの ALTER 権限が必要です。  
  
 WQL クエリのスコープの詳細については、「 [WMI Provider For Server Events での wql の使用](https://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx)」を参照してください。  
  
 スコープの例として、次の WQL クエリを含む WMI プロバイダー アプリケーションを考えます。  
  
```  
SELECT * FROM ALTER_TABLE  
WHERE DatabaseName = "AdventureWorks2012"   
    AND SchemaName = "Person"  
    AND ObjectName = "Person"  
    AND ObjectType = "TABLE";  
```  
  
 WMI プロバイダーはこのクエリを変換し、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベース内にイベント通知を作成します。 つまり、呼び出し側は、このようなイベント通知を作成するのに必要な権限 (具体的には CREATE DATABASE DDL EVENT NOTIFICATION 権限) を [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベース内に持っている必要があります。  
  
 サーバー レベルをスコープとしたイベント通知を指定する WQL クエリ (SELECT * FROM ALTER_TABLE など) の場合、呼び出し側アプリケーションはサーバー レベルの CREATE DDL EVENT NOTIFICATION 権限を持っている必要があります。 サーバースコープのイベント通知は、master データベースに格納されることに注意してください。 [Sys.server_event_notifications](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md)カタログビューを使用すると、メタデータを表示できます。  
  
> [!NOTE]  
>  WMI プロバイダーによって作成されるイベント通知のスコープ (サーバー、データベース、またはオブジェクト) は、最終的には、WMI プロバイダーによって使用される権限検証プロセスの結果によって異なります。 これは、プロバイダーを呼び出しているユーザーの権限セットとクエリ対象のデータベースの検証の影響を受けます。  
>   
>  前の例では、プロバイダーはまず、データベース スコープ (`ON DATABASE`) のイベント通知を作成しようとします。 プロバイダーがデータベースの存在を検出し、このデータベース上でイベント通知を作成するために必要な権限を呼び出し側が持っていると確認すると、登録が正常に行われます。 登録に失敗するとプロバイダーは、サーバー上 (`ON SERVER`) にイベント通知を作成しようとします。 この試行が成功したと見なして、サーバー上で発生した `ALTER_TABLE` イベントはすべて、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスから WMI サービス プロセスに送信されます。 ただし、`AdventureWorks` データベースに該当しないイベントは、フィルターによって除外されます。 このプロセスは、イベントのスコープに対して必要なネットワーク トラフィック量を増加させる場合がありますが、このプロセスによって、データベースを作成する前にそのデータベースに関する WQL クエリを登録しておき、データベースが作成されそのデータベースでの DDL 動作が開始した後にイベント データを受け取れるという柔軟性を実現することができます。  
  
## <a name="permissions-and-message-verification"></a>権限とメッセージの検証  
 WMI プロバイダーは、次の両方の条件が満たされる場合は、イベント通知に対してメッセージを送信しません。  
  
-   WMI プロバイダーを通してイベント通知を作成したユーザーがデータベース内に存在しない場合、または類似のイベント通知を作成するために必要な権限を持っていない場合。  
  
-   イベント通知は、次のイベントで作成されます。  
  
    -   DROP_LOGIN  
  
    -   ALTER_LOGIN  
  
    -   DROP_USER  
  
    -   ALTER_USER  
  
    -   ADD_ROLE_MEMBER  
  
    -   DROP_ROLE_MEMBER  
  
    -   ADD_SERVER_ROLE_MEMBER  
  
    -   DROP_SERVER_ROLE_MEMBER  
  
    -   DENY または REVOKE (ALTER DATABASE、ALTER ANY DATABASE EVENT NOTIFICATION、CREATE DATABASE DDL EVENT NOTIFICATION、CONTROL SERVER、ALTER ANY EVENT NOTIFICATION、CREATE DDL EVENT NOTIFICATION、または CREATE TRACE EVENT NOTIFICATION 権限のみに適用されます)  
  
## <a name="working-with-event-data-on-the-client-side"></a>クライアント側のイベント データの使用  
 WMI Provider for Server Events によって、ターゲットデータベースに必要なイベント通知が作成された後、イベント通知は、 **SQL/notification/Processを Eventprovidernotification/** v1.0 という名前の msdb 内の対象サービスにイベントデータを送信します。 発信先サービスは、" **wmi**" という名前の**msdb**内のキューにイベントを格納します。 (サービスとキューの両方が、に最初に接続するときにプロバイダーによって動的に作成され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます)。プロバイダーは、このキューから XML イベントデータを読み取り、それを管理オブジェクト形式 (MOF) に変換してから、クライアントアプリケーションに返します。 MOF データは、CIM (Common Information Model) クラス定義として WQL クエリから要求されるイベントのプロパティで構成されています。 各プロパティには、対応する CIM 型があります。 たとえば、プロパティは `SPID` CIM 型 **Sint32**として返されます。 各プロパティの CIM 型については、「 [WMI Provider For Server Events のクラスとプロパティ](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md)」の各イベントクラスに記載されています。  
  
## <a name="see-also"></a>参照  
 [WMI Provider for Server Events の概念](./wmi-provider-for-server-events-concepts.md)  
  
