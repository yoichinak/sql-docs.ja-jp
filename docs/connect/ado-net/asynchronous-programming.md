---
title: 非同期プログラミング
description: Microsoft SqlClient Data Provider for SQL Server での非同期プログラミングについて説明します。
ms.date: 12/04/2020
ms.assetid: 85da7447-7125-426e-aa5f-438a290d1f77
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 6eec681974499219a1ca649f9a47449a27ff4002
ms.sourcegitcommit: 5b2c47ce88f7e56552fd415c32b319009d043b56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/29/2020
ms.locfileid: "97804298"
---
# <a name="asynchronous-programming"></a>非同期プログラミング

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

このトピックでは、Microsoft SqlClient Data Provider for SQL Server (SqlClient) での非同期プログラミングのサポートについて説明します。

## <a name="legacy-asynchronous-programming"></a>レガシ非同期プログラミング

Microsoft SqlClient Data Provider for SQL Server には、<xref:Microsoft.Data.SqlClient> に移行するアプリケーションの下位互換性を維持するために、**System.Data.SqlClient** のメソッドが含まれています。 新しい開発に次のレガシ非同期プログラミング メソッドを使用することはお勧めしません。

- <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A?displayProperty=nameWithType>

- <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A?displayProperty=nameWithType>

- <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A?displayProperty=nameWithType>

> [!TIP]
> Microsoft SqlClient Data Provider for SQL Server では、これらのレガシ メソッドの接続文字列に `Asynchronous Processing=true` が不要になりました。

## <a name="asynchronous-programming-features"></a>非同期プログラミング機能

これらの非同期プログラミング機能には、コードを非同期にするための簡単な手法が用意されています。

.NET の非同期プログラミングの詳細については、以下を参照してください。

- [C# の非同期プログラミング](/dotnet/csharp/async)

- [Async および Await を使用した非同期プログラミング (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/async/index)

ユーザー インターフェイスが応答しない場合やサーバーのパフォーマンスが向上しない場合は、コードをさらに非同期にする必要がある可能性があります。 非同期コードの記述には、従来、非同期操作の完了後に発生するロジックを表すコールバック (または継続とも呼ばれます) のインストールが伴っていました。 これにより、同期コードと比較して、非同期コードの構造は複雑になります。

コールバックを使用することなく、またコードを複数のメソッドやラムダ式に分割することなく、非同期メソッドを呼び出すことができます。

`async` 修飾子はメソッドが非同期であることを示します。 `async` メソッドを呼び出すと、タスクが返されます。 `await` 演算子がタスクに適用されると、現在のメソッドはすぐに終了します。 タスクが終了すると、同じメソッド内で実行が再開されます。

> [!TIP]
> Microsoft SqlClient Data Provider for SQL Server では、`Context Connection` 接続文字列キーワードを設定するために非同期呼び出しは必要ありません。

`async` メソッドを呼び出すと、追加のスレッドは割り当てられません。 既存の I/O 完了スレッドが最後に簡単に使用される可能性があります。

Microsoft SqlClient Data Provider for SQL Server の次のメソッドは、非同期プログラミングをサポートしています。

- <xref:System.Data.Common.DbConnection.OpenAsync%2A?displayProperty=nameWithType>

- <xref:System.Data.Common.DbCommand.ExecuteDbDataReaderAsync%2A?displayProperty=nameWithType>

- <xref:System.Data.Common.DbCommand.ExecuteNonQueryAsync%2A?displayProperty=nameWithType>

- <xref:System.Data.Common.DbCommand.ExecuteReaderAsync%2A?displayProperty=nameWithType>

- <xref:System.Data.Common.DbCommand.ExecuteScalarAsync%2A?displayProperty=nameWithType>

- <xref:System.Data.Common.DbDataReader.GetFieldValueAsync%2A>

- <xref:System.Data.Common.DbDataReader.IsDBNullAsync%2A>

- <xref:System.Data.Common.DbDataReader.NextResultAsync%2A?displayProperty=nameWithType>

- <xref:System.Data.Common.DbDataReader.ReadAsync%2A?displayProperty=nameWithType>

- <xref:Microsoft.Data.SqlClient.SqlConnection.OpenAsync%2A?displayProperty=nameWithType>

- <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteNonQueryAsync%2A?displayProperty=nameWithType>

- <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteReaderAsync%2A?displayProperty=nameWithType>

- <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteScalarAsync%2A?displayProperty=nameWithType>

- <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteXmlReaderAsync%2A?displayProperty=nameWithType>

- <xref:Microsoft.Data.SqlClient.SqlDataReader.NextResultAsync%2A?displayProperty=nameWithType>

- <xref:Microsoft.Data.SqlClient.SqlDataReader.ReadAsync%2A?displayProperty=nameWithType>

- <xref:Microsoft.Data.SqlClient.SqlBulkCopy.WriteToServerAsync%2A?displayProperty=nameWithType>

他の非同期メンバーは、[SqlClient ストリーミング サポート](sqlclient-streaming-support.md)をサポートしています。

> [!TIP]
> 非同期メソッドでは、接続文字列に `Asynchronous Processing=true` は必要ありません。 また、このプロパティは、Microsoft SqlClient Data Provider for SQL Server で廃止されています。

### <a name="synchronous-to-asynchronous-connection-open"></a>同期から非同期の接続のオープン

非同期機能を使用するように既存のアプリケーションをアップグレードすることができます。 たとえば、同期接続アルゴリズムを使用したアプリケーションで、データベースに接続するたびに UI スレッドをブロックし、接続すると、ユーザーがサインインしたことを他のユーザーに通知するストアド プロシージャが呼び出されるとします。

[!code-csharp[SqlCommand_ExecuteNonQuery#1](~/../sqlclient/doc/samples/SqlCommand_ExecuteNonQuery.cs#1)]

非同期機能を使用するように変換すると、プログラムは次のようになります。

[!code-csharp[SqlCommand_ExecuteNonQueryAsync#1](~/../sqlclient/doc/samples/SqlCommand_ExecuteNonQueryAsync.cs#1)]

### <a name="add-the-asynchronous-feature-in-an-existing-application-mixing-old-and-new-patterns"></a>既存のアプリケーションに非同期機能を追加する (古いパターンと新しいパターンを混在させる)

既存の非同期ロジックを変更せずに、非同期機能 (SqlConnection:: OpenAsync) を追加することもできます。 たとえば、現在、次のアルゴリズムを使用するアプリケーションがあるとします。

[!code-csharp[SqlConnection_OpenAsync_ContinueWith#1](~/../sqlclient/doc/samples/SqlConnection_OpenAsync_ContinueWith.cs#1)]

既存のアルゴリズムを大幅に変更することなく、非同期パターンの使用を開始できます。

[!code-csharp[SqlConnection_OpenAsync_ContinueWith#2](~/../sqlclient/doc/samples/SqlConnection_OpenAsync_ContinueWith.cs#2)]

### <a name="use-the-base-provider-model-and-the-asynchronous-feature"></a>基本プロバイダー モデルと非同期機能を使用する

異なるデータベースに接続してクエリを実行できるツールを作成することが必要になる場合があります。 基本プロバイダー モデルと非同期機能を使用することができます。

分散トランザクションを使用するには、サーバー上で Microsoft Distributed Transaction Controller (MSDTC) サービスを有効にする必要があります。 MSDTC を有効にする方法の詳細については、「[Web サーバーで MSDTC を有効にする方法](/previous-versions/commerce-server/dd327979(v=cs.90))」を参照してください。

[!code-csharp[SqlClient_AsyncProgramming_ProviderModel#1](~/../sqlclient/doc/samples/SqlClient_AsyncProgramming_ProviderModel.cs#1)]

### <a name="use-sql-transactions-and-the-new-asynchronous-feature"></a>SQL トランザクションと新しい非同期機能を使用する

[!code-csharp[SqlClient_AsyncProgramming_SqlTransaction#1](~/../sqlclient/doc/samples/SqlClient_AsyncProgramming_SqlTransaction.cs#1)]

### <a name="use-distributed-transactions-and-the-new-asynchronous-feature"></a>分散トランザクションと新しい非同期機能を使用する

エンタープライズ アプリケーションでは、複数のデータベース サーバー間のトランザクションを有効にするために、シナリオによっては **分散トランザクション** の追加が必要になる場合があります。 次のように、System.Transactions 名前空間を使用して分散トランザクションを登録できます。

[!code-csharp[SqlClient_AsyncProgramming_DistributedTransaction#1](~/../sqlclient/doc/samples/SqlClient_AsyncProgramming_DistributedTransaction.cs#1)]

### <a name="cancel-an-asynchronous-operation"></a>非同期操作を取り消す

<xref:System.Threading.CancellationToken> を使用して、非同期要求を取り消すことができます。

[!code-csharp[SqlClient_AsyncProgramming_Cancellation#1](~/../sqlclient/doc/samples/SqlClient_AsyncProgramming_Cancellation.cs#1)]

### <a name="asynchronous-operations-with-sqlbulkcopy"></a>SqlBulkCopy を使用した非同期操作

非同期機能は <xref:Microsoft.Data.SqlClient.SqlBulkCopy.WriteToServerAsync%2A?displayProperty=nameWithType> を使用した <xref:Microsoft.Data.SqlClient.SqlBulkCopy?displayProperty=nameWithType> にもあります。

[!code-csharp[SqlClient_AsyncProgramming_SqlBulkCopy#1](~/../sqlclient/doc/samples/SqlClient_AsyncProgramming_SqlBulkCopy.cs#1)]

## <a name="asynchronously-use-multiple-commands-with-mars"></a>MARS と共に複数のコマンドを非同期に使用する

この例では、**AdventureWorks** データベースへの 1 つの接続を開きます。 <xref:Microsoft.Data.SqlClient.SqlCommand> オブジェクトを使用することで、<xref:Microsoft.Data.SqlClient.SqlDataReader> が作成されます。 そのリーダーが使用されるとき、最初の <xref:Microsoft.Data.SqlClient.SqlDataReader> のデータが 2 番目のリーダーの WHERE 句への入力として使用され、2 番目の <xref:Microsoft.Data.SqlClient.SqlDataReader> が開きます。

> [!NOTE]
> 次の例では、サンプルの [**AdventureWorks** データベース](../../samples/adventureworks-install-configure.md)を使用しています。 サンプル コードに示されている接続文字列では、データベースがローカル コンピューターにインストールされ、使用可能であることを前提としています。 必要に応じて、お使いの環境に合わせて接続文字列を変更してください。

[!code-csharp[SqlClient_AsyncProgramming_MultipleCommands#1](~/../sqlclient/doc/samples/SqlClient_AsyncProgramming_MultipleCommands.cs#1)]

## <a name="asynchronously-read-and-update-data-with-mars"></a>MARS を使用してデータを非同期的に読み取り、更新する

MARS を使用すると、複数の保留中の操作について、読み取り操作と DML (データ操作言語) 操作の両方で 1 つの接続を使用することができます。 この機能により、アプリケーションで接続ビジー エラーを処理する必要がなくなります。 さらに、MARS ではサーバー側カーソルの使用を置き換えることができます。通常、この処理は多くのリソースを消費します。 最後に、複数の操作を単一の接続で実行できるので、同じトランザクション コンテキストを共有することにより、システムのストアド プロシージャである **sp_getbindtoken** と **sp_bindsession** を使用する必要がなくなります。

次のコンソール アプリケーションでは、2 つの <xref:Microsoft.Data.SqlClient.SqlDataReader> オブジェクトを 3 つの <xref:Microsoft.Data.SqlClient.SqlCommand> オブジェクトと使用する方法、および 1 つの <xref:Microsoft.Data.SqlClient.SqlConnection> オブジェクトを MARS を有効にして使用する方法について示します。 最初のコマンド オブジェクトは、信用格付けの評価が 5 であるベンダーの一覧を取得します。 2 番目のコマンド オブジェクトは、<xref:Microsoft.Data.SqlClient.SqlDataReader> から提供されているベンダー ID を使用して、特定のベンダーの全製品を含む 2 番目の <xref:Microsoft.Data.SqlClient.SqlDataReader> を読み込みます。 各製品レコードには、2 番目の <xref:Microsoft.Data.SqlClient.SqlDataReader> によってアクセスされます。 計算が実行され、新規 **OnOrderQty** を判定します。 3 番目のコマンド オブジェクトでは、**ProductVendor** テーブルを新しい値で更新します。 このプロセスはすべて 1 つのトランザクション内で実行され、最後にロールバックされます。

> [!NOTE]
> 次の例では、サンプルの [**AdventureWorks** データベース](../../samples/adventureworks-install-configure.md)を使用しています。 サンプル コードに示されている接続文字列では、データベースがローカル コンピューターにインストールされ、使用可能であることを前提としています。 必要に応じて、お使いの環境に合わせて接続文字列を変更してください。

[!code-csharp[SqlClient_AsyncProgramming_MultipleCommandsEx#1](~/../sqlclient/doc/samples/SqlClient_AsyncProgramming_MultipleCommandsEx.cs#1)]

## <a name="see-also"></a>関連項目

- [ADO.NET でのデータの取得と変更](retrieving-modifying-data.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
