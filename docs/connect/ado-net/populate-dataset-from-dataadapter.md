---
title: DataAdapter から DataSet を設定する
description: データ ソースに依存しない一貫したリレーショナル プログラミング モデルを提供する ADO.NET の DataAdapter から、DataSet を設定する方法について説明します。
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: 3fa0ac7d-e266-4954-bfac-3fbe2f913153
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: e6c50bf7255dc77edfd0b93e03dedeec83ed4c4d
ms.sourcegitcommit: c938c12cf157962a5541347fcfae57588b90d929
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2020
ms.locfileid: "97771504"
---
# <a name="populate-a-dataset-from-a-dataadapter"></a>DataAdapter から DataSet を設定する

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

ADO.NET の <xref:System.Data.DataSet> は、データ ソースに依存しない一貫したリレーショナル プログラミング モデルを提供するメモリ常駐型のデータ表現です。 `DataSet` はテーブル、制約、およびテーブル間のリレーションシップを含む完全なデータのセットを表します。 `DataSet` はデータ ソースとは独立しているため、 `DataSet` にはそのアプリケーションに固有のデータと複数のデータ ソースからのデータを含めることができます。 既存のデータ ソースとの対話は `DataAdapter`によって制御されます。

`SelectCommand` の `DataAdapter` プロパティは、データ ソースからデータを取得する `Command` オブジェクトです。 `InsertCommand`の `UpdateCommand`、 `DeleteCommand` 、 `DataAdapter` の各プロパティは、 `Command` のデータに対して行われた変更に基づいてデータ ソースのデータ更新を管理する `DataSet`オブジェクトです。 これらのプロパティは、「[DataAdapter を使用してデータ ソースを更新する](update-data-sources-with-dataadapters.md)」で詳しく説明されています。

`Fill` の `DataAdapter` メソッドは、 `DataSet` の `SelectCommand` の結果を `DataAdapter`に設定するために使用します。 `Fill` は、その引数として、設定対象である `DataSet` と、 `DataTable` オブジェクト (つまり、 `DataTable` から返された行を格納する `SelectCommand`の名前) を受け取ります。

> [!NOTE]
> `DataAdapter` を使用してテーブル全体を取得すると、特にテーブルの行数が多い場合は処理に時間がかかります。 データベースにアクセスし、データを検索して処理した後、そのデータをクライアントに転送するという時間のかかる処理が伴うためです。 また、テーブル全体をクライアントに取得しようとすると、サーバー上ですべての行がロックされます。 `WHERE` 句を使用して、クライアントから返される行数をできるだけ減らすことでパフォーマンスを向上させることができます。 また、 `SELECT` ステートメントで必要な列を明示的に指定するだけでもクライアントに返されるデータ量を減らすことができます。 それ以外の対策としては、一度に数百行など、行をバッチで取得し、クライアントが現在のバッチの処理を完了した時点で次のバッチを取得する方法も効果的です。

`Fill` メソッドは、 `DataReader` オブジェクトを暗黙的に使用して `DataSet`内でテーブルを作成するための列の名前と型、および `DataSet`内のテーブルの行を設定するためのデータを返します。 テーブルおよび列は、存在しない場合にのみ作成されます。それ以外の場合、 `Fill` には、既存の `DataSet` スキーマが使用されます。 列の型は、「[ADO.NET でのデータ型のマッピング](data-type-mappings-ado-net.md)」のテーブルに従って、.NET Framework 型として作成されます。 データ ソースに主キーが存在し、 `DataAdapter`**によって制御されます。** `MissingSchemaAction` が `MissingSchemaAction`**によって制御されます。** `AddWithKey`によって制御されます。 `Fill` はテーブルに主キーがあることがわかると、主キー列の値がデータ ソースから返された主キー列の値と一致する行について、データ ソースから返されたデータで `DataSet` 内のデータを上書きします。 主キーが見つからない場合は、 `DataSet`のテーブルの末尾にデータを追加します。 `Fill` は `DataSet` の読み込み時に存在する可能性があるすべてのマッピングを使用します (「[DataAdapter、DataTable、DataColumn のマッピング](dataadapter-datatable-datacolumn-mappings.md)」を参照)。

> [!NOTE]
> `SelectCommand` が OUTER JOIN の結果を返す場合、 `DataAdapter` は、生成される `PrimaryKey` に `DataTable`値を設定しません。 自分で `PrimaryKey` を定義して、重複行が正しく解決されるようにする必要があります。

次のコード サンプルでは、Microsoft SQL Server の <xref:Microsoft.Data.SqlClient.SqlDataAdapter> データベースへの <xref:Microsoft.Data.SqlClient.SqlConnection> を使用する `Northwind` のインスタンスを作成し、 <xref:System.Data.DataTable> 内の `DataSet` に顧客リストを読み込みます。 <xref:Microsoft.Data.SqlClient.SqlConnection> コンストラクターに渡される SQL ステートメントおよび <xref:Microsoft.Data.SqlClient.SqlDataAdapter> 引数は、 <xref:Microsoft.Data.SqlClient.SqlDataAdapter.SelectCommand%2A> の <xref:Microsoft.Data.SqlClient.SqlDataAdapter>プロパティを作成するために使用されます。

## <a name="example"></a>例

[!code-csharp[SqlDataAdapter_FillDataSet#1](~/../sqlclient/doc/samples/SqlDataAdapter_FillDataSet.cs#1)]

> [!NOTE]
> このサンプル コードでは、 `Connection`の開始と終了を明示的に行っていません。 `Fill` メソッドは、接続がまだ開いていないことを認識すると `Connection` が使用している `DataAdapter` を暗黙的に開きます。 `Fill` が接続を開いた場合は、 `Fill` の終了時に Fill が接続を終了します。 これにより、 `Fill` や `Update`などの単一の操作を扱う場合にコードを簡略化できます。 これに対し、開いている接続を必要とする複数の操作を実行する場合は、 `Open` の `Connection`メソッドを明示的に呼び出し、データ ソースに対する操作の実行後に `Close` の `Connection`メソッドを呼び出すことでアプリケーションのパフォーマンスを改善できます。 リソースを解放して他のクライアント アプリケーションが使用できるようにするために、データ ソースへの接続を開いたままにする時間は最小限にすることをお勧めします。

## <a name="multiple-result-sets"></a>複数結果セット

`DataAdapter` は複数の結果セットを検出すると、 `DataSet`に複数のテーブルを作成します。 これらのテーブルには、Table0 のように、"Table" で始まるインクリメンタル既定名 Table *N* が割り当てられます。 テーブル名を引数として `Fill` メソッドに渡すと、TableName0 を表す "TableName" で始まるインクリメンタル既定名 TableName *N* が割り当てられます。  
  
## <a name="populate-a-dataset-from-multiple-dataadapters"></a>複数の DataAdapter から DataSet を読み込む  

1 つの `DataSet` で、任意の数の `DataAdapter` オブジェクトを使用できます。 それぞれの `DataAdapter` で 1 つ以上の `DataTable` オブジェクトにデータを格納し、関連するデータ ソースに更新を反映させることができます。 `DataRelation` に対して `Constraint` オブジェクトおよび `DataSet` オブジェクトを部分的に追加できるため、複数の異なるデータ ソースから取得したデータを関連付けることができます。 たとえば、Microsoft SQL Server データベース、OLE DB を通じて公開される IBM DB2 データベース、および XML をストリーム転送するデータ ソースからのデータを `DataSet` に含めることができます。 1 つ以上の `DataAdapter` オブジェクトを使用して、各データ ソースとの通信を行うことができます。  
  
### <a name="example"></a>例  

次のコード サンプルでは、Microsoft SQL Server の `Northwind` データベースおよび Microsoft Access に格納された `Northwind` データベースから、それぞれ顧客リストと注文リストを取得します。 取得したテーブルを `DataRelation`で関連付けて、顧客および対応する注文の一覧を表示します。

[!code-csharp[SqlDataAdapter_FillDataSet#2](~/../sqlclient/doc/samples/SqlDataAdapter_FillDataSet.cs#2)]

## <a name="sql-server-decimal-type"></a>SQL Server Decimal 型

既定では、`DataSet` は .NET データ型を使用してデータを格納します。 ほとんどのアプリケーションで、これらのデータ型を使用してデータ ソース情報を簡単に表示できます。 しかし、データ ソースのデータ型が SQL Server の 10 進数データ型または数値データ型の場合は、この表現によって問題が生じる場合があります。 .NET `decimal` のデータ型の最大有効桁数は 28 桁であるのに対し、SQL Server `decimal` のデータ型の有効桁数は 38 桁です。 `SqlDataAdapter` が動作している間に、 `Fill` が、SQL Server の `decimal` フィールドの有効桁数が 28 文字を超えていると判断した場合、現在の行は `DataTable`に追加されません。 その場合は `FillError` イベントが発生するため、開発者は有効桁数の消失が発生していないかどうかを確認し、適切に対応できます。 `FillError` イベントの詳細については、「[DataAdapter イベントの処理](handle-dataadapter-events.md)」を参照してください。 SQL Server の `decimal` 値を取得するために、 <xref:Microsoft.Data.SqlClient.SqlDataReader> オブジェクトを使用し、 <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlDecimal%2A> メソッドを呼び出すこともできます。

ADO.NET でも `DataSet` の <xref:System.Data.SqlTypes> に対するサポート機能が強化されています。 詳細については、「 [SqlTypes and the DataSet](./sql/sqltypes-dataset.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [DataAdapter と DataReader](dataadapters-datareaders.md)
- [ADO.NET のデータ型のマッピング](data-type-mappings-ado-net.md)
- [複数のアクティブな結果セット (MARS)](./sql/multiple-active-result-sets-mars.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
