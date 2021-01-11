---
title: パラメーターの構成
description: コマンド オブジェクトは、パラメーターを使用して SQL ステートメントまたはストアド プロシージャに値を渡すことによって、ADO.NET での型チェックと検証の機能を実現します。
ms.date: 11/25/2020
dev_langs:
- csharp
ms.assetid: 537d8a2c-d40b-4000-83eb-bc1fcc93f707
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 14442892bc59fc733c6a67153832b95c3f368b95
ms.sourcegitcommit: c938c12cf157962a5541347fcfae57588b90d929
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2020
ms.locfileid: "97771460"
---
# <a name="configuring-parameters"></a>パラメーターの構成

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

コマンド オブジェクトは、パラメーターを使用して SQL ステートメントまたはストアド プロシージャに値を渡すことによって、型チェックと検証の機能を実現します。 コマンド テキストとは異なり、パラメーターの入力は実行可能なコードとしてではなく、リテラル値として扱われます。 これにより、攻撃者がサーバーのセキュリティを侵害するコマンドを SQL ステートメントに "注入" する SQL インジェクション攻撃を防ぐことができます。

パラメーター化コマンドによりクエリ実行パフォーマンスも向上します。これは、データベース サーバーが入力コマンドを適切なキャッシュ済みクエリ プランに正確に一致させるのに役立つためです。 詳細については、「[実行プランのキャッシュと再利用](/sql/relational-databases/query-processing-architecture-guide#execution-plan-caching-and-reuse)」および「[パラメーターと実行プランの再利用](/sql/relational-databases/query-processing-architecture-guide#PlanReuse)」を参照してください。 セキュリティおよびパフォーマンス上の利点に加え、パラメーター化コマンドを使用すると、データ ソースに渡す値を簡単に扱うことができます。

<xref:System.Data.Common.DbParameter> オブジェクトは、コンストラクターを使って作成できるほか、 <xref:System.Data.Common.DbCommand.DbParameterCollection%2A> コレクションの `Add` メソッドを呼び出し、 <xref:System.Data.Common.DbParameterCollection> にオブジェクトを追加することによって作成することもできます。 `Add` メソッドは、コンストラクター引数または既存のパラメーター オブジェクトを入力として受け取ります。この点はデータ プロバイダーによっても異なります。

## <a name="supply-the-parameterdirection-property"></a>ParameterDirection プロパティを指定する

パラメーターを追加する際は、入力パラメーターとは別に、パラメーターの <xref:System.Data.ParameterDirection> プロパティを指定する必要があります。 `ParameterDirection` で使用できる <xref:System.Data.ParameterDirection> の値を次の表に示します。

|メンバー名|説明|
|-----------------|-----------------|
|<xref:System.Data.ParameterDirection.Input>|このパラメーターは入力パラメーターです。 既定値です。|
|<xref:System.Data.ParameterDirection.InputOutput>|このパラメーターは入力と出力の両方の機能を持っています。|
|<xref:System.Data.ParameterDirection.Output>|このパラメーターは出力パラメーターです。|
|<xref:System.Data.ParameterDirection.ReturnValue>|パラメーターは、ストアド プロシージャ、組み込み関数、ユーザー定義関数などの操作からの戻り値を表します。|

## <a name="work-with-parameter-placeholders"></a>パラメーターのプレースホルダーを操作する

パラメーターのプレースホルダーの構文はデータ ソースに依存します。 Microsoft SqlClient Data Provider for SQL Server では、パラメーターおよびパラメーターのプレースホルダーの名前付け方法と指定方法が異なります。 SqlClient Data Provider では、`@`*parametername* 形式の名前付きパラメーターが使用されます。

## <a name="specify-parameter-data-types"></a>パラメーターのデータ型を指定する

パラメーターのデータ型は、Microsoft SqlClient Data Provider for SQL Server に固有です。 型を指定すると、`Parameter` の値が Microsoft SqlClient Data Provider for SQL Server 型に変換されてから、データ ソースに値が渡されます。 `Parameter` オブジェクトの `DbType` プロパティを特定の `Parameter` に設定する一般的な方法で <xref:System.Data.DbType>の型を指定することもできます。

`Parameter` オブジェクトの Microsoft SqlClient Data Provider for SQL Server 型は、`Parameter` オブジェクトの `Value` の .NET Framework 型から、または `Parameter` オブジェクトの `DbType` から推論されます。 `Parameter` 値として渡されるオブジェクトまたは指定された `Parameter` に基づいて推論される `DbType`型を、次の表に示します。

|.NET の種類|DbType|SqlDbType|
|-------------------------|------------|---------------|
|<xref:System.Boolean>|ブール型|ビット|
|<xref:System.Byte>|Byte|TinyInt|
|byte[]|2 項|VarBinary。 バイト配列が VarBinary の最大サイズ (8000 バイト) より大きい場合、この暗黙の変換はエラーになります。 8000 バイトを超えるバイト配列の場合は、明示的に <xref:System.Data.SqlDbType> を設定してください。|
|<xref:System.Char>| |char から <xref:System.Data.SqlDbType> への推論はサポートされていません。|
|<xref:System.DateTime>|DateTime|DateTime|
|<xref:System.DateTimeOffset>|DateTimeOffset|SQL Server 2008 の DateTimeOffset。 SQL Server 2008 より前のバージョンの SQL Server では、DateTimeOffset から <xref:System.Data.SqlDbType> への推論はサポートされていません。|
|<xref:System.Decimal>|Decimal|Decimal|
|<xref:System.Double>|Double|Float|
|<xref:System.Single>|Single|Real|
|<xref:System.Guid>|GUID|UniqueIdentifier|
|<xref:System.Int16>|Int16|SmallInt|
|<xref:System.Int32>|Int32|int|
|<xref:System.Int64>|Int64|BigInt|
|<xref:System.Object>|Object|バリアント|
|<xref:System.String>|String|NVarChar。 文字列が NVarChar の最大サイズ (4000 文字) より大きい場合、この暗黙の変換はエラーになります。 4000 文字を超える文字列の場合は、明示的に <xref:System.Data.SqlDbType>を設定してください。|
|<xref:System.TimeSpan>|時刻|SQL Server 2008 の Time。 SQL Server 2008 より前のバージョンの SQL Server では、TimeSpan から <xref:System.Data.SqlDbType> への推論はサポートされていません。|
|<xref:System.UInt16>|UInt16|UInt16 から <xref:System.Data.SqlDbType> への推論はサポートされていません。|
|<xref:System.UInt32>|UInt32|UInt32 から <xref:System.Data.SqlDbType> への推論はサポートされていません。|
|<xref:System.UInt64>|UInt64|UInt64 から <xref:System.Data.SqlDbType> への推論はサポートされていません。|
||AnsiString|VarChar|
||AnsiStringFixedLength|Char|
||通貨|通貨|
||Date|SQL Server 2008 の Date。 SQL Server 2008 より前のバージョンの SQL Server では、Date から <xref:System.Data.SqlDbType> への推論はサポートされていません。|
||SByte|SByte から <xref:System.Data.SqlDbType> への推論はサポートされていません。|
||StringFixedLength|NChar|
||時刻|SQL Server 2008 の Time。 SQL Server 2008 より前のバージョンの SQL Server では、Time から <xref:System.Data.SqlDbType> への推論はサポートされていません。|
||VarNumeric|VarNumeric から <xref:System.Data.SqlDbType> への推論はサポートされていません。|
|ユーザー定義型 ( <xref:Microsoft.SqlServer.Server.SqlUserDefinedAggregateAttribute>を持つオブジェクト)|SqlClient は常に Object を返します|<xref:Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute> が存在する場合は `SqlDbType.Udt`。それ以外の場合は `Variant`|

> [!NOTE]
> decimal から他の型への変換は縮小変換になるため、decimal 値は最も近い整数値に切り捨てられます。 変換結果が対象の型にならなかった場合、 <xref:System.OverflowException> がスローされます。

> [!NOTE]
> サーバーに NULL パラメーター値を送信する場合は、`null` (Visual Basic の場合は `Nothing`) ではなく、<xref:System.DBNull> を指定する必要があります。 システムの null 値は、値のない空オブジェクトです。 <xref:System.DBNull> は、null 値を表すために使用します。

## <a name="derive-parameter-information"></a>パラメーター情報を派生させる

`DbCommandBuilder` クラスを使用してストアド プロシージャからパラメーターを派生させることができます。 `SqlCommandBuilder` クラスには静的メソッド `DeriveParameters` が用意されています。これにより、ストアド プロシージャからのパラメーター情報を使用するコマンド オブジェクトのパラメーターのコレクションが自動的に設定されます。 `DeriveParameters` はコマンドの既存のパラメーター情報を上書きします。

> [!NOTE]
> パラメーター情報を派生させた場合、情報を取得するためにデータ ソースへのラウンド トリップが 1 つ増えるため、パフォーマンスが低下します。 パラメーター情報がデザイン時にわかっている場合は、パラメーターを明示的に設定することでアプリケーションのパフォーマンスを改善できます。

詳細については、「[CommandBuilder でのコマンドの生成](generate-commands-with-commandbuilders.md)」を参照してください。

## <a name="using-parameters-with-a-sqlcommand-and-a-stored-procedure"></a>SqlCommand およびストアド プロシージャでのパラメーターの使用

ストアド プロシージャは、データドリブンのアプリケーションに多くの利点を提供します。 ストアド プロシージャを使用すると、データベースの操作を単一のコマンドにカプセル化し、最大のパフォーマンスが得られるように最適化し、さらに追加のセキュリティ機能を使用して、セキュリティを強化することができます。 ストアド プロシージャは、ストアド プロシージャ名の後にパラメーター引数を記述して SQL ステートメントとして渡すことで呼び出すことができますが、ADO.NET の <xref:System.Data.Common.DbCommand> オブジェクトの <xref:System.Data.Common.DbCommand.Parameters%2A> コレクションを使用すると、ストアド プロシージャ パラメーターをより明示的に定義でき、出力パラメーターや戻り値にもアクセスできます。

> [!NOTE]
> パラメーター化ステートメントは、 `sp_executesql,` を使ってサーバー上で実行されるため、クエリ プランの再利用が可能になります。 `sp_executesql` バッチ内のローカル カーソルまたはローカル変数は、 `sp_executesql`を呼び出すバッチでは認識されません。 データベース コンテキストの変更は、 `sp_executesql` ステートメント終了時まで有効です。 詳細については、「[sp_executesql (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-executesql-transact-sql)」を参照してください。

<xref:Microsoft.Data.SqlClient.SqlCommand> でパラメーターを使用して SQL Server のストアド プロシージャを実行する場合は、 <xref:Microsoft.Data.SqlClient.SqlCommand.Parameters%2A> コレクションに追加したパラメーターの名前が、ストアド プロシージャ内のパラメーター マーカーの名前と一致している必要があります。 Microsoft SqlClient Data Provider for SQL Server では、SQL ステートメントまたはストアド プロシージャにパラメーターを渡す際の疑問符 (?) のプレースホルダーはサポートされていません。 ストアド プロシージャ内のパラメーターは名前付きのパラメーターと見なされ、一致するパラメーター マーカーが検索されます。 たとえば、 `CustOrderHist` ストアド プロシージャが、 `@CustomerID`という名前のパラメーターで定義されているとします。 このストアド プロシージャを実行する場合、実行元のコードでも `@CustomerID`という名前のパラメーターを使用する必要があります。

```sql
CREATE PROCEDURE dbo.CustOrderHist @CustomerID varchar(5)
```

### <a name="example"></a>例

次の例では、 `Northwind` サンプル データベースにある SQL Server ストアド プロシージャを呼び出す方法を説明します。 ストアド プロシージャの名前は `dbo.SalesByCategory` で、 `@CategoryName` データ型の `nvarchar(15)`という名前の入力パラメーターを持ちます。 このコードでは、プロシージャの終了時に接続が破棄されるように、using ブロック内で新しい <xref:Microsoft.Data.SqlClient.SqlConnection> を作成しています。 <xref:Microsoft.Data.SqlClient.SqlCommand> オブジェクトおよび <xref:Microsoft.Data.SqlClient.SqlParameter> オブジェクトが作成され、それぞれのプロパティが設定されます。 <xref:Microsoft.Data.SqlClient.SqlDataReader> によって `SqlCommand` が実行された後、ストアド プロシージャから結果セットが返されて、出力がコンソール ウィンドウに表示されます。

> [!NOTE]
> `SqlCommand` オブジェクトと `SqlParameter` オブジェクトを作成してから別個のステートメントでプロパティを設定する代わりに、オーバーロード コンストラクターを使用して複数のプロパティを 1 つのステートメントで設定することもできます。

[!code-csharp[DataWorks SqlClient.StoredProcedure#1](~/../sqlclient/doc/samples/SqlCommand_StoredProcedure.cs#1)]

## <a name="see-also"></a>関連項目

- [コマンドとパラメーター](commands-parameters.md)
- [DataAdapter と DataReader](dataadapters-datareaders.md)
- [ADO.NET のデータ型のマッピング](data-type-mappings-ado-net.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
