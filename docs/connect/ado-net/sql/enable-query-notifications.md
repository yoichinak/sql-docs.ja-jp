---
title: クエリ通知の有効化
description: クエリ通知を使用する方法、およびそれを有効にし、使用するための要件について説明します。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: a5333e19-8e55-4aa9-82dc-ca8745e516ed
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 1fae73102dbbb29b6772213c4d021c273271458a
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725640"
---
# <a name="enabling-query-notifications"></a>クエリ通知の有効化

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

クエリ通知を使用するアプリケーションには、一般的な一連の要件があります。 SQL クエリ通知をサポートするには、データ ソースが正しく設定され、ユーザーがクライアント側およびサーバー側の正しい権限を所有している必要があります。  
  
クエリ通知を使用するには、次のことが必要です。  
  
- データベースのクエリ通知を有効にします。  
  
- データベースへの接続に使用するユーザー ID に必要なアクセス許可があることを確認します。  
  
- <xref:Microsoft.Data.SqlClient.SqlCommand> オブジェクトを使用して、通知オブジェクト (<xref:Microsoft.Data.SqlClient.SqlDependency> または <xref:Microsoft.Data.Sql.SqlNotificationRequest> のいずれか) が関連付けられている有効な SELECT ステートメントを実行します。  
  
- 監視対象のデータが変更された場合に通知を処理するコードを指定します。  
  
## <a name="query-notifications-requirements"></a>クエリ通知の要件  
クエリ通知は、特定の要件の一覧を満たす SELECT ステートメントでのみサポートされます。 次の表に、SQL Server オンライン ブックの Service Broker とクエリ通知のドキュメントへのリンクを示します。  
  
**SQL Server のドキュメント**  
  
- [通知のためのクエリの作成](/previous-versions/sql/sql-server-2008-r2/ms181122(v=sql.105))  
  
- [Service Broker のセキュリティに関する注意点](/previous-versions/sql/sql-server-2005/ms166059(v=sql.90))  
  
- [セキュリティと保護 (Service Broker)](/previous-versions/sql/sql-server-2008-r2/bb522911(v=sql.105))  
  
- [Notification Services のセキュリティに関する注意点](/previous-versions/sql/sql-server-2005/ms172604(v=sql.90))  
  
- [クエリ通知の権限](/previous-versions/sql/sql-server-2008-r2/ms188311(v=sql.105))  
  
- [Service Broker の国際化に関する注意点](/previous-versions/sql/sql-server-2005/ms166028(v=sql.90))  
  
- [ソリューション設計に関する考慮事項 (Service Broker)](/previous-versions/sql/sql-server-2008-r2/bb522899(v=sql.105))  
  
- [Service Broker 開発者向けの情報](/previous-versions/sql/sql-server-2008-r2/ms166100(v=sql.105))  
  
- [開発者ガイド (Service Broker)](/previous-versions/sql/sql-server-2008-r2/bb522908(v=sql.105))  
  
## <a name="enabling-query-notifications-to-run-sample-code"></a>サンプル コードを実行するためのクエリ通知の有効化  
**AdventureWorks** データベースで Service Broker を有効にするには、SQL Server Management Studio を通じて、次の Transact-SQL ステートメントを実行します。  
  
`ALTER DATABASE AdventureWorks SET ENABLE_BROKER;`  
  
クエリ通知のサンプルを正しく実行するには、次の Transact-SQL ステートメントをデータベース サーバー上で実行する必要があります。  
  
```sql
CREATE QUEUE ContactChangeMessages;  
  
CREATE SERVICE ContactChangeNotifications  
  ON QUEUE ContactChangeMessages  
([http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification]);  
```  
  
## <a name="query-notifications-permissions"></a>クエリ通知のアクセス許可  
通知を要求するコマンドを実行するユーザーには、サーバー上で SUBSCRIBE QUERY NOTIFICATIONS データベース権限が必要です。  
  
部分的に信頼される状況で実行されるクライアント側のコードには <xref:Microsoft.Data.SqlClient.SqlClientPermission> が必要です。  
  
次のコードは <xref:Microsoft.Data.SqlClient.SqlClientPermission> オブジェクトを作成し、<xref:System.Security.Permissions.PermissionState> を <xref:System.Security.Permissions.PermissionState.Unrestricted> に設定します。 <xref:System.Security.CodeAccessPermission.Demand%2A> は、呼び出し履歴の上位にある呼び出し元にアクセス許可が付与されていないものがある場合、実行時に <xref:System.Security.SecurityException> を強制します。  
  
[!code-csharp[DataWorks SqlClientPermission_Demand#1](~/../sqlclient/doc/samples/SqlClientPermission_Demand.cs#1)]
  
## <a name="choosing-a-notification-object"></a>通知オブジェクトの選択  
クエリ通知 API には、通知を処理するための 2 つのオブジェクト <xref:Microsoft.Data.SqlClient.SqlDependency> と <xref:Microsoft.Data.Sql.SqlNotificationRequest> があります。
  
### <a name="using-sqldependency"></a>SqlDependency の使用  
<xref:Microsoft.Data.SqlClient.SqlDependency> を使用するには、使用している SQL Server データベースに対して Service Broker を有効にし、通知を受け取るためのアクセス許可をユーザーに与える必要があります。 通知キューなどの Service Broker オブジェクトは事前に定義されています。  
  
さらに、<xref:Microsoft.Data.SqlClient.SqlDependency> によってワーカー スレッドが自動的に起動し、キューにポストされた通知が処理されます。また、Service Broker メッセージも解析され、情報がイベント引数データとして公開されます。 <xref:Microsoft.Data.SqlClient.SqlDependency> は、`Start` メソッドを呼び出し、データベースに対する依存関係を確立して初期化する必要があります。 これは、必要となる各データベース接続に対するアプリケーションの初期化中に、1 回だけ呼び出す必要のある静的メソッドです。 `Stop` メソッドは、作成された依存関係の接続ごとにアプリケーションの終了時に呼び出す必要があります。  
  
### <a name="using-sqlnotificationrequest"></a>SqlNotificationRequest の使用  
これに対して、<xref:Microsoft.Data.Sql.SqlNotificationRequest> では、リッスンしているインフラストラクチャ全体を自分で実装する必要があります。 さらに、キュー、サービス、およびキューでサポートされているメッセージの種類など、サポート対象となるすべての Service Broker オブジェクトを定義する必要があります。 この手動のアプローチは、使用しているアプリケーションに特殊な通知メッセージまたは通知動作が必要な場合や、アプリケーションがより大きな Service Broker アプリケーションの一部である場合に役立ちます。  
  
## <a name="next-steps"></a>次のステップ
- [SQL Server でのクエリ通知](query-notifications-sql-server.md)