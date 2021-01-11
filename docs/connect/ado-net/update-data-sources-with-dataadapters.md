---
title: DataAdapter を使用してデータ ソースを更新する
description: DataAdapter の Update メソッドが、DataSet からの変更を ADO.NET アプリケーションのデータ ソースに反映させて解決する方法について説明します。
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: d1bd9a8c-0e29-40e3-bda8-d89176b72fb1
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 6f2feb876d0f232f4d7951de8ee1cc84587e6486
ms.sourcegitcommit: c938c12cf157962a5541347fcfae57588b90d929
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2020
ms.locfileid: "97771375"
---
# <a name="update-data-sources-with-dataadapters"></a>DataAdapter を使用してデータ ソースを更新する

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

`Update` の <xref:System.Data.Common.DataAdapter> メソッドを呼び出して、変更を <xref:System.Data.DataSet> からデータ ソースに反映します。 `Update` メソッドは、`Fill` メソッドと同様に、引数として `DataSet` のインスタンスおよびオプションの <xref:System.Data.DataTable> オブジェクトまたは `DataTable` 名を受け取ります。 `DataSet` のインスタンスは、行われた変更点を格納する `DataSet` です。`DataTable` は、変更点の取得元のテーブルです。 `DataTable` を指定しなかった場合、`DataTable` 内の最初の `DataSet` が使用されます。

`Update` メソッドを呼び出すと、`DataAdapter` は、既に加えられた変更を解析し、適切なコマンド (INSERT、UPDATE、または DELETE) を実行します。 `DataAdapter` は <xref:System.Data.DataRow> へ加えられた変更を検出すると、<xref:Microsoft.Data.SqlClient.SqlDataAdapter.InsertCommand%2A>、<xref:Microsoft.Data.SqlClient.SqlDataAdapter.UpdateCommand%2A>、または <xref:Microsoft.Data.SqlClient.SqlDataAdapter.DeleteCommand%2A> を使用してその変更を処理します。

これらのプロパティを使用すると、設計時にコマンド構文を指定し、可能であれば、ストアド プロシージャを介して、ADO.NET アプリケーションのパフォーマンスを最大限に高めることができます。 コマンドは `Update` を呼び出す前に明示的に設定する必要があります。 `Update` を呼び出し、その更新に関連する適切なコマンドが存在しない場合 (たとえば、削除済みの行に関連する `DeleteCommand` が存在しない場合) は、例外がスローされます。

> [!IMPORTANT]
> `DataAdapter` を使用してデータの編集または削除を行うために SQL Server ストアド プロシージャを使用している場合は、ストアド プロシージャの定義内で `SET NOCOUNT ON` を使用しないようにしてください。 処理された行数がゼロとして返され、`DataAdapter` によってコンカレンシーの競合として解釈されてしまいます。 この場合、<xref:System.Data.DBConcurrencyException> がスローされます。

Command パラメーターを使用して、`DataSet` 内の各変更行に対する SQL ステートメントまたはストアド プロシージャに入力値と出力値を指定できます。 詳細については、「[DataAdapter パラメーター](dataadapter-parameters.md)」を参照してください。

> [!NOTE]
> <xref:System.Data.DataTable> の行を Delete することと、行を Remove することの違いを理解することが大切です。 `Remove` メソッドまたは `RemoveAt` メソッドを呼び出した場合、行は直ちに削除されます。 `DataTable` または `DataSet` を `DataAdapter` に渡し、`Update` を呼び出した場合、バック エンド データ ソース内の対応する行が **影響を受けることはありません**。 `Delete` メソッドを使用した場合、行はそのまま `DataTable` 内に維持され、削除対象としてマークされます。 次に、`DataTable` または `DataSet` を `DataAdapter` に渡して `Update`を呼び出すと、バック エンド データ ソース内の対応する行が **削除されます**。

`DataTable` を単一データベース テーブルに割り当てたり、単一データベースから生成する場合は、<xref:System.Data.Common.DbCommandBuilder> オブジェクトを利用して自動的に `DeleteCommand` の `InsertCommand` オブジェクト、`UpdateCommand` オブジェクト、および `DataAdapter` オブジェクトを生成できます。 詳細については、「[CommandBuilder を使用したコマンドの生成](generate-commands-with-commandbuilders.md)」を参照してください。

## <a name="use-updatedrowsource-to-map-values-to-a-dataset"></a>UpdatedRowSource を使用して DataSet に値をマップする

<xref:Microsoft.Data.SqlClient.SqlCommand> オブジェクトの <xref:Microsoft.Data.SqlClient.SqlCommand.UpdatedRowSource%2A> プロパティを使用すると、`DataAdapter` の <xref:System.Data.Common.DbDataAdapter.Update%2A> メソッドの呼び出し後にデータ ソースから返される値を `DataTable` にマップする方法を制御できます。 `UpdatedRowSource` プロパティを <xref:System.Data.UpdateRowSource> 列挙型の値の 1 つに設定することで、`DataAdapter` コマンドが返した出力パラメーターを無視するか、`DataSet` 内の変更行に適用するかを制御できます。 最初に返された行 (存在する場合) を、`DataTable` 内の変更行に適用するかどうかを指定することもできます。

`UpdateRowSource` 列挙型のさまざまの値と、それらの値が `DataAdapter` で使用されるコマンドの動作にどのように影響するかを次の表で説明します。

|UpdatedRowSource 列挙型|説明|
|----------------------------------|-----------------|
|<xref:System.Data.UpdateRowSource.Both>|出力パラメーターと返された結果セットの最初の行を `DataSet` 内の変更行に割り当てます。|
|<xref:System.Data.UpdateRowSource.FirstReturnedRecord>|返された結果セットの最初の行のデータだけを `DataSet` 内の変更行に割り当てます。|
|<xref:System.Data.UpdateRowSource.None>|出力パラメーターまたは返された結果セットの行が無視されます。|
|<xref:System.Data.UpdateRowSource.OutputParameters>|出力パラメーターだけを `DataSet` 内の変更行に割り当てます。|

`Update` メソッドは変更点を元のデータ ソースに反映させますが、`DataSet` に最後にデータを格納した後、他のクライアントがデータ ソースのデータを変更した可能性もあります。 `DataSet` を現在のデータで更新するには、`DataAdapter` および `Fill` メソッドを使用します。 新しい行がテーブルに追加され、更新された情報が既存の行に取り込まれます。

`Fill` メソッドは、`DataSet` の行と `SelectCommand` によって返された行の主キーの値を調べて、新しい行が追加されたか、または既存の行が更新されたかを判断します。 `Fill` メソッドは、`DataSet` によって返された結果の行に一致する主キーの値を持つ `SelectCommand` の行を見つけた場合、`SelectCommand` によって返された行の情報で既存の行を更新して、既存の行の <xref:System.Data.DataRow.RowState%2A> を `Unchanged` に設定します。 `SelectCommand` によって返された行の主キーの値が、`DataSet` のどの行の主キーの値にも一致しない場合、`Fill` メソッドは、`RowState` が `Unchanged` の新しい行を追加します。

> [!NOTE]
> `SelectCommand` から **OUTER JOIN** の結果が返される場合、結果として得られる `DataTable` の `PrimaryKey` 値は `DataAdapter` によって設定されません。 自分で `PrimaryKey` を定義して、重複行が正しく反映されるようにする必要があります。

`Update` メソッドの呼び出し時に発生する可能性がある例外を処理するには、行更新エラーが発生したときに `RowUpdated` イベントを使用してそれらに応答することも ([DataAdapter のイベントの処理](handle-dataadapter-events.md)に関するページを参照)、`Update` の呼び出しの前に <xref:System.Data.Common.DataAdapter.ContinueUpdateOnError%2A> を `true` に設定し、更新が完了した時点で特定の行の `RowError` プロパティに格納されているエラー情報に応答することもできます。

> [!NOTE]
> `DataSet`、`DataTable`、または `DataRow` に対して `AcceptChanges` を呼び出すと、`DataRow` に対するすべての `Original` の値が、`DataRow` に対する `Current` の値で上書きされます。 行を一意に識別するフィールド値が変更された場合は、`AcceptChanges` 呼び出しの後に `Original` 値がデータ ソースの値と一致しなくなります。 `AcceptChanges` は、`DataAdapter` の `Update` メソッドの呼び出し中に行ごとに自動的に呼び出されます。 Update メソッドの呼び出し中に元の値を維持するには、まず `AcceptChangesDuringUpdate` の `DataAdapter` プロパティを false に設定するか、`RowUpdated` イベントのイベント ハンドラーを作成し、その <xref:System.Data.Common.RowUpdatedEventArgs.Status%2A> を <xref:System.Data.UpdateStatus.SkipCurrentRow> に設定します。 詳細については、「[DataAdapter イベントの処理](handle-dataadapter-events.md)」を参照してください。

次の例では、`DataAdapter` の `UpdateCommand` を明示的に設定し、その `Update` メソッドを呼び出すことにより、変更済みの行に対して更新を実行する方法を示します。

> [!NOTE]
> `UPDATE statement` の `WHERE clause` で指定されるパラメーターは、`SourceColumn` の `Original` 値を使用するように設定されます。 `Current` 値が既に変更されている可能性、そしてデータ ソースの値と一致していない可能性があるため、この設定は重要です。 `Original` 値は、データ ソースから `DataTable` にデータを取得するために使用された値です。

[!code-csharp[SqlDataAdapter_Update#1](~/../sqlclient/doc/samples/SqlDataAdapter_Update.cs#1)]

## <a name="autoincrement-columns"></a>AutoIncrement 列

データ ソースから取得したテーブルに自動インクリメント列がある場合、自動インクリメント値をストアド プロシージャの出力パラメーターとして取得してそれをテーブルの列に割り当てるか、ストアド プロシージャまたは SQL ステートメントによって返された結果セットの最初の行の自動インクリメント値を取得するか、または `DataSet` の `RowUpdated` イベントを使用して追加の SELECT コマンドを実行することによって、`DataAdapter` の列に値を格納できます。 詳細と例については、「[ID 値または autonumber 値の取得](retrieve-identity-or-autonumber-values.md)」を参照してください。

## <a name="ordering-of-inserts-updates-and-deletes"></a>挿入、更新、削除の順序

通常の条件下では、`DataSet` を使用して行う変更の順序をデータ ソースに送信することが重要です。 たとえば、既存の行の主キーの値を更新し、その新しい主キーの値を外部キーとして新しい行を追加する場合、更新は挿入の前に処理する必要があります。

`Select` の `DataTable` メソッドを使用すると、特定の `DataRow` を持つ行だけを参照する `RowState` 配列を返すことができます。 その後で、返された `DataRow` 配列を `Update` の `DataAdapter` メソッドに渡して変更行を処理できます。 更新する行のサブセットを指定することで、挿入、更新、および削除の処理順序を制御できます。

## <a name="example"></a>例

たとえば次のコードでは、テーブルの削除行を最初に処理し、次に更新行、最後に挿入行を処理します。

[!code-csharp[SqlDataAdapter_Update#2](~/../sqlclient/doc/samples/SqlDataAdapter_Update.cs#2)]

## <a name="use-a-dataadapter-to-retrieve-and-update-data"></a>DataAdapter を使用してデータを取得および更新する

DataAdapter を使用すると、データを取得および更新できます。

- このサンプルでは、`DataAdapter.AcceptChangesDuringFill` を使用して、データベース内のデータを複製します。 このプロパティが **false** として設定されている場合、テーブルの入力時に **AcceptChanges** は呼び出されず、新しく追加された行は挿入された行として扱われます。 そのため、このサンプルでは、これらの行を使用して、データベースに新しい行を挿入します。

- このサンプルでは、`DataAdapter.TableMappings` を使用して、ソース テーブルと DataTable の間のマッピングを定義します。

- このサンプルでは、`DataAdapter.FillLoadOption` を使用して、アダプターで **DbDataReader** から **DataTable** にどのように入力するかを決定します。 DataTable を作成するときは、プロパティを **LoadOption.Upsert** または **LoadOption.PreserveChanges** として設定することによって、データベースからのデータを現在のバージョンまたは元のバージョンにのみ書き込むことができるだけです。

- このサンプルでは、`DbDataAdapter.UpdateBatchSize` を使用してバッチ操作を実行することで、テーブルを更新します。

サンプルをコンパイルして実行する前に、サンプル データベースを作成する必要があります。

```sql
USE [master]
GO

CREATE DATABASE [MySchool]

GO

USE [MySchool]
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Course]([CourseID] [nvarchar](10) NOT NULL,
[Year] [smallint] NOT NULL,
[Title] [nvarchar](100) NOT NULL,
[Credits] [int] NOT NULL,
[DepartmentID] [int] NOT NULL,
 CONSTRAINT [PK_Course] PRIMARY KEY CLUSTERED
(
[CourseID] ASC,
[Year] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY]

GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Department]([DepartmentID] [int] IDENTITY(1,1) NOT NULL,
[Name] [nvarchar](50) NOT NULL,
[Budget] [money] NOT NULL,
[StartDate] [datetime] NOT NULL,
[Administrator] [int] NULL,
 CONSTRAINT [PK_Department] PRIMARY KEY CLUSTERED
(
[DepartmentID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY]

GO

INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C1045', 2012, N'Calculus', 4, 7)
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C1061', 2012, N'Physics', 4, 1)
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C2021', 2012, N'Composition', 3, 2)
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C2042', 2012, N'Literature', 4, 2)

SET IDENTITY_INSERT [dbo].[Department] ON

INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (1, N'Engineering', 350000.0000, CAST(0x0000999C00000000 AS DateTime), 2)
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (2, N'English', 120000.0000, CAST(0x0000999C00000000 AS DateTime), 6)
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (4, N'Economics', 200000.0000, CAST(0x0000999C00000000 AS DateTime), 4)
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (7, N'Mathematics', 250024.0000, CAST(0x0000999C00000000 AS DateTime), 3)
SET IDENTITY_INSERT [dbo].[Department] OFF

ALTER TABLE [dbo].[Course]  WITH CHECK ADD  CONSTRAINT [FK_Course_Department] FOREIGN KEY([DepartmentID])
REFERENCES [dbo].[Department] ([DepartmentID])
GO
ALTER TABLE [dbo].[Course] CHECK CONSTRAINT [FK_Course_Department]
GO
```

[!code-csharp[SqlDataAdapter_Properties#1](~/../sqlclient/doc/samples/SqlDataAdapter_Properties.cs#1)]

## <a name="see-also"></a>関連項目

- [DataAdapter と DataReader](dataadapters-datareaders.md)
- [ID 値または autonumber 値の取得](retrieve-identity-or-autonumber-values.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
