---
title: SQL Server 接続プール
description: Microsoft SqlClient Data Provider for SQL Server により、SQL Server 接続プールを使用して接続を開くコストが最小限に抑えられる方法を説明します。これにより、新しい接続のオーバーヘッドが軽減されます。
ms.date: 11/13/2020
dev_langs:
- csharp
ms.assetid: 7e51d44e-7c4e-4040-9332-f0190fe36f07
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 2a04c986f9d9b5189a5ed0c2751c0df3cdd876e0
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126470"
---
# <a name="sql-server-connection-pooling-adonet"></a>SQL Server の接続プール (ADO.NET)

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

通常、データベース サーバーへの接続は、時間のかかるいくつかの手順で構成されています。 ソケットまたは名前付きパイプなどの物理チャネルの確立、サーバーとの最初のハンドシェイクの実行、接続文字列の情報の解析、サーバーによる接続の認証、現在のトランザクションへ参加するための検証などの手順を行う必要があります。

実際には、ほとんどのアプリケーションで、1 つまたはいくつかの違いがあるだけの構成を接続に使用しています。 つまり、アプリケーションの実行時に、多数の同一の接続が繰り返し開かれ、閉じられているのです。 接続を開くコストを最小化するため、Microsoft SqlClient Data Provider for SQL Server により "*接続プール*" と呼ばれる最適化の手法が使用されます。

接続プールは、新しく開く必要のある接続の数を減らします。 "*プーラー*" には、物理的な接続の所有権が保持されます。 プーラーは、任意の接続構成それぞれのアクティブな接続のセットをそのまま保持して、接続を管理します。 この接続の `Open` を呼び出すと、プーラーは、プールに使用可能な接続があるかどうかを確認します。 プールされた接続が使用できる場合は、新しい接続を開く代わりに、プールされた接続を呼び出し元に返します。 アプリケーションが接続で `Close` を呼び出すと、プーラーは接続を閉じる代わりに、プールされたアクティブな接続のセットに接続を返します。 接続がプールに返されると、その接続は、次の `Open` 呼び出しで再度使用できる状態になります。

同じ構成を持つ接続のみをプールすることができます。 Microsoft SqlClient Data Provider for SQL Server により、構成ごとに 1 つずつ、複数のプールが同時に保持されます。 接続は接続文字列によってプール内で区別されます。また、統合セキュリティを使用している場合は、Windows ID によっても区別されます。 接続がプールされるかどうかは、その接続がトランザクションに参加しているかどうかにも依存します。 <xref:Microsoft.Data.SqlClient.SqlConnection.ChangePassword%2A> を使用すると、<xref:Microsoft.Data.SqlClient.SqlCredential> インスタンスは接続プールに影響します。 ユーザー ID とパスワードが同じでも、<xref:Microsoft.Data.SqlClient.SqlCredential> のインスタンスごとに異なる接続プールが使用されます。

接続をプールすると、アプリケーションのパフォーマンスとスケーラビリティを大幅に改善できます。 Microsoft SqlClient Data Provider for SQL Server の接続プールは既定で有効になります。 明示的に無効にしない限り、プーラーは、アプリケーションで接続が開かれたり、閉じられたりする際に接続を最適化します。 また、接続プール機能の動作を制御する接続文字列修飾子を指定することもできます。 詳細については、このトピックで後述する「**接続文字列キーワードによる接続プールの制御**」を参照してください。

> [!IMPORTANT]
> 接続プールが有効になっているときに、タイムアウト エラーまたはその他のログイン エラーが発生した場合は、例外がスローされ、それから **5** 秒間 ("`blocking period`")、後続の接続試行は失敗します。 ブロック期間内にアプリケーションが接続を試みると、最初の例外が再度スローされます。 ブロック期間が終了した後でエラーが発生した場合、新しいブロック期間は前のブロック期間の 2 倍の長さになります。"*最大の長さは **1** 分です*"。

> [!NOTE]
> "`blocking period`" メカニズムは、既定では Azure SQL Server には適用されません。 *.NET Standard* を除き、この動作は <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString> の <xref:Microsoft.Data.SqlClient.PoolBlockingPeriod> プロパティを変更することによって変更できます。

## <a name="pool-creation-and-assignment"></a>プールの作成と割り当て

接続が最初に開かれると、完全一致のアルゴリズムに基づいて接続プールが作成され、接続内の接続文字列に関連付けられます。 各接続プールが別の接続文字列に関連付けられます。 新しい接続が開かれたとき、接続文字列が既存のプールと完全に一致しない場合は、新しいプールが作成されます。

> [!NOTE]
> 接続は、"_プロセス_" ごと、"_アプリケーション ドメイン_" ごと、"_接続文字列_" ごと、そして統合セキュリティが使用されている場合は "_Windows ID_" ごとにプールされます。 また、接続文字列は完全に一致していることが必要です。同じ接続に対してキーワードを異なる順序で指定すると別々にプールされます。

> [!NOTE]
> 接続文字列で `MinPoolSize` が指定されていない、またはゼロに指定されている場合、プール内の接続は、アクティブではない一定の期間後に閉じられます。 ただし、`MinPoolSize` がゼロより大きい値に設定されている場合、接続プールは、`AppDomain` がアンロードされ、プロセスが終了するまで破棄されません。 アクティブでないプールまたは空のプールを維持するためには、最小限のシステム オーバーヘッドが発生します。

> [!NOTE]
> フェールオーバーなど、致命的なエラーが発生すると、プールは自動的にクリアされます。

3 つの新しい <xref:Microsoft.Data.SqlClient.SqlConnection> オブジェクトを作成し、2 つの接続プールだけでこの 3 つのオブジェクトを管理する C# の例を次に示します。 1 番目の接続文字列と 2 番目の接続文字列では、`Initial Catalog` に割り当てる値が異なります。  


[!code-csharp[SqlConnection_Pooling#1](~/../sqlclient/doc/samples/SqlConnection_Pooling.cs#1)]

## <a name="adding-connections"></a>接続の追加

一意の接続文字列ごとに 1 つの接続プールが作成されます。 プールが作成された段階で、複数の接続オブジェクトが作成されてそのプールへ追加され、最小プール サイズ要件を満たします。 必要に応じて、指定されている最大プール サイズ (**既定値は 100**) になるまで、接続がプールに追加されます。 接続が終了または破棄されると、その接続は解放され、プールに戻されます。

<xref:Microsoft.Data.SqlClient.SqlConnection> オブジェクトが要求されると、プールに使用可能な接続がある場合はプールから取得されます。 使用可能な接続とは、サーバーへの有効なリンクを持つ接続のうち、使用中でないか、一致するトランザクション コンテキストを持っているか、またはどのトランザクション コンテキストにも関連付けられていない接続のことです。

接続プーラーは、接続がプールに解放されたときに接続の再割り当てを行って、接続に対する要求に応えます。 最大プール サイズに達すると、使用可能な接続を取得できなくなり、要求はキューに置かれます。 その後、プーラーによって、タイムアウトに達するまで (**既定値は 15 秒**) 接続の再利用が試みられます。 接続がタイムアウトになる前に、プーラーが要求を満たすことができない場合は、例外がスローされます。

> [!CAUTION]
> 接続がプールに返されるようにするために、接続を使い終えたら必ず接続を終了することを強くお勧めします。 この操作は、`Connection` オブジェクトの `Close` または `Dispose` メソッドを使用して、あるいは C# の `using` ステートメントまたは Visual Basic の `Using` ステートメントの内部ですべての接続を開くことによって、行うことができます。 明示的に終了されていない接続は、プールに追加したり返したりすることができないことがあります。 詳しくは、「[using ステートメント](/dotnet/docs/csharp/language-reference/keywords/using-statement.md)」または「[方法: システム リソースを破棄する](/dotnet/docs/visual-basic/programming-guide/language-features/control-flow/how-to-dispose-of-a-system-resource.md)」 (Visual Basic の場合) をご覧ください。

> [!NOTE]
> クラスの `Close` メソッド内で `Dispose`、`Connection`、またはその他のマネージド オブジェクトの `DataReader` または `Finalize` を呼び出さないでください。 終了処理では、クラスに直接所有されているアンマネージ リソースだけを解放してください。 クラスがアンマネージ リソースを所有していない場合は、クラス定義に `Finalize` メソッドを含めないでください。 詳しくは、「[ガベージ コレクション](/dotnet/docs/standard/garbage-collection/index.md)」をご覧ください。

接続の開始と終了に関連するイベントについて詳しくは、SQL Server のドキュメントの「[Audit Login イベント クラス](/sql/relational-databases/event-classes/audit-login-event-class)」および「[Audit Logout イベント クラス](/sql/relational-databases/event-classes/audit-logout-event-class)」をご覧ください。

## <a name="removing-connections"></a>接続の削除

接続が約 **4 から 8** 分間アイドル状態になった後、またはサーバーとの接続が切断されたことがプーラーで検出された場合は、接続プーラーによってプールから接続が削除されます。

> [!NOTE]
> 切断された接続は、サーバーとの通信が試みられた後でのみ検出できます。 接続がサーバーに接続していないことがわかると、その接続は無効としてマークされます。 無効な接続は、閉じられるか、または再利用された場合のみ、接続プールから削除されます。

既に存在しないサーバーへの接続が存在する場合は、接続プーラーが、その接続が切断されていることをまだ検出せず、無効というマークを付けていない状況のときでも、プールからその接続を削除できます。 この機能は、接続がまだ有効であることを確認するオーバーヘッドによってサーバーへのラウンド トリップが実行されることにより、プーラーの利点が失われてしまうことを防ぐためにあります。 この状況が発生した場合は、接続の使用を最初に試みたときに接続が切断されていることが検出され、例外がスローされます。

## <a name="clearing-the-pool"></a>プールのクリア

Microsoft SqlClient Data Provider for SQL Server において、プールをクリアするための 2 つの新しいメソッド <xref:Microsoft.Data.SqlClient.SqlConnection.ClearAllPools%2A> と <xref:Microsoft.Data.SqlClient.SqlConnection.ClearPool%2A> が導入されています。 `ClearAllPools` は、指定されたプロバイダーの接続プールをクリアし、`ClearPool` は、特定の接続に関連付けられた接続プールをクリアします。

> [!NOTE]
> これらのメソッドが呼び出されたときに使用中の接続がある場合は、適切にマーク付けされ、 接続が閉じられるとプールに返されずに破棄されます。

## <a name="transaction-support"></a>トランザクションのサポート

接続はプールから取り出され、トランザクション コンテキストに基づいて割り当てられます。 接続文字列で `Enlist=false` が指定されていない限り、接続プールは、接続を <xref:System.Transactions.Transaction.Current%2A> コンテキストの中に参加させます。 接続が閉じられ、参加した `System.Transactions` トランザクションと共にプールに返されると、同じ `System.Transactions` トランザクションを持つ接続プールに対する次の要求でも、使用可能であれば同じ接続を返すように接続が保持されます。 このような要求が発行された場合で、なおかつ、プールされた接続が使用できない場合は、プールの非トランザクション部分から接続を取り出して参加させます。 プールのどちらの領域にも使用できる接続がない場合は、新しい接続を作成して参加させます。

接続が終了すると、その接続は解放されてプールへ返り、さらに、そのトランザクション コンテキストに基づいて特定のサブプールへ返ります。 そのため、分散トランザクションが保留状態である場合を含め、エラーを発生させることなく、開発者が接続を終了させることは可能です。 これにより、分散トランザクションを後でコミットまたは中止できます。

## <a name="controlling-connection-pooling-with-connection-string-keywords"></a>接続文字列キーワードによる接続プールの制御

`ConnectionString` オブジェクトの <xref:Microsoft.Data.SqlClient.SqlConnection> プロパティは、接続プール ロジックの動作を調整するために使用できる接続文字列キーおよび値のペアをサポートします。 詳細については、「<xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>」を参照してください。

## <a name="pool-fragmentation"></a>プールの断片化

プールの断片化は、プロセスが終了するまで解放されないプールを多数作成できる Web アプリケーションの多くで一般的な問題です。 これにより、多数の接続が開いたままになってメモリを消費し、パフォーマンスが低下します。

### <a name="pool-fragmentation-due-to-integrated-security"></a>統合セキュリティによるプールの断片化

接続は、接続文字列とユーザー ID に基づいてプールされます。 したがって、Web サイトで基本認証または Windows 認証を使用していて、統合セキュリティ ログインを使用している場合は、1 ユーザーにつき 1 つのプールが作成されます。 これによって、単一のユーザーによる後続のデータベース要求のパフォーマンスが向上しますが、他のユーザーによって作成された接続は使用できません。 また、1 ユーザーにつき少なくとも 1 つの接続がデータベース サーバーに存在することになります。 これは、開発者がセキュリティおよび監査要件に対して、特定の Web アプリケーションのアーキテクチャに重点を置く必要があるために起こる副作用です。

### <a name="pool-fragmentation-due-to-many-databases"></a>多数のデータベースによるプールの断片化

インターネット サービス プロバイダーの多くは、1 つのサーバー上で複数の Web サイトをホストしています。 インターネット サービス プロバイダーは、1 つのデータベースを使用してフォーム認証ログインを確認し、そのユーザーまたはユーザー グループの特定のデータベースへの接続を開きます。 認証データベースへの接続はプールされ、すべてのユーザーが使用できるようになります。 ただし、各データベースに対して個別の接続のプールが存在するため、サーバーへの接続数が増加します。

これもまた、アプリケーションのデザインの副作用です。 SQL Server に接続するときにセキュリティを損なうことなく、この副作用を回避する比較的簡単な方法があります。 各ユーザーまたはグループの個別のデータベースに接続する代わりに、サーバー上の同じデータベースに接続してから、Transact-SQL USE ステートメントを実行して目的のデータベースに変更します。
 
`master` データベースへの最初の接続を作成し、`databaseName` 文字列変数で指定した目的のデータベースに切り替えるコードを次に示します。

[!code-csharp[SqlConnection_Pooling_Use_Statement#1](~/../sqlclient/doc/samples/SqlConnection_Pooling_Use_Statement.cs#1)]

## <a name="application-roles-and-connection-pooling"></a>アプリケーション ロールおよび接続プール

`sp_setapprole` システム ストアド プロシージャの呼び出しにより SQL Server のアプリケーション ロールが起動された後は、その接続のセキュリティ コンテキストをリセットすることはできません。 ただし、プールを有効した場合は、プールに接続が返され、プール接続が再利用されると、エラーが発生します。

### <a name="application-role-alternatives"></a>アプリケーション ロールに代わる方法

アプリケーション ロールに代わるセキュリティ メカニズムの使用をお勧めします。

## <a name="see-also"></a>関連項目

- [接続プール](connection-pooling.md)
- [SQL Server と ADO.NET](./sql/index.md)
