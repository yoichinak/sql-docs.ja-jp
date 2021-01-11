---
title: SqlClient ストリーミング サポート
description: 完全にメモリに読み込むことなく SQL Server からデータをストリーミングするアプリケーションの作成方法について説明します。
ms.date: 12/04/2020
ms.assetid: c449365b-470b-4edb-9d61-8353149f5531
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: c5ae05856f3f1e01d5831a6e80338f19e3994966
ms.sourcegitcommit: 4419e99d77ee2c73f9da1559c7944f7702f2de30
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/23/2020
ms.locfileid: "97744397"
---
# <a name="sqlclient-streaming-support"></a>SqlClient ストリーミング サポート

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

SQL Server とアプリケーション間のストリーミング サポートでは、サーバー上の非構造化データ (ドキュメント、画像、およびメディア ファイル) をサポートします。 SQL Server データベースはバイナリ ラージ オブジェクト (BLOB) を格納できますが、BLOB の取得には大量のメモリが使用される可能性があります。

SQL Server との間のストリーミングのサポートにより、データをストリーミングするアプリケーションの作成が簡単になり、データをメモリに完全に読み込む必要がないため、メモリのオーバーフロー例外が減少します。

また、ストリーミング サポートにより、特に大規模な BLOB を送信、取得、操作するためにビジネス オブジェクトが Azure SQL に接続されるシナリオでは、中間層アプリケーションのスケールが向上します。

> [!WARNING]
> ストリーミングをサポートするメンバーは、クエリからデータを取得し、クエリやストアド プロシージャにパラメーターを渡すために使用されます。 ストリーミング機能は、基本的な OLTP およびデータ移行のシナリオに対処し、オンプレミスおよびオフプレミスのデータ移行環境に適用できます。

## <a name="streaming-support-from-sql-server"></a>SQL Server からのストリーミング サポート

SQL Server からのストリーミングのサポートでは、<xref:System.IO.Stream>、<xref:System.Xml.XmlReader>、<xref:System.IO.TextReader> の各オブジェクトを取得して対応するために、<xref:System.Data.Common.DbDataReader> クラスと <xref:Microsoft.Data.SqlClient.SqlDataReader> クラスに新機能が導入されています。 これらのクラスはクエリからデータを取得するために使用されます。 その結果、SQL Server からのストリーミングのサポートは OLTP シナリオに対応しており、オンプレミスおよびオフプレミス環境に適用されます。

SQL Server からのストリーミングのサポートを有効にするために、次のメンバーが <xref:Microsoft.Data.SqlClient.SqlDataReader> に追加されました。

- <xref:Microsoft.Data.SqlClient.SqlDataReader.IsDBNullAsync%2A>

- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetFieldValue%2A?displayProperty=nameWithType>

- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetFieldValueAsync%2A>

- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetStream%2A>

- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetTextReader%2A>

- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetXmlReader%2A>

SQL Server からのストリーミングのサポートを有効にするために、次のメンバーが <xref:System.Data.Common.DbDataReader> に追加されました。

- <xref:System.Data.Common.DbDataReader.GetFieldValue%2A>

- <xref:System.Data.Common.DbDataReader.GetStream%2A>

- <xref:System.Data.Common.DbDataReader.GetTextReader%2A>

## <a name="streaming-support-to-sql-server"></a>SQL Server へのストリーミング サポート

<xref:Microsoft.Data.SqlClient.SqlParameter> クラスには SQL Server へのストリーミング サポートがあるため、<xref:System.Xml.XmlReader>、<xref:System.IO.Stream>、および <xref:System.IO.TextReader> の各オブジェクトを受け取って対応できます。 <xref:Microsoft.Data.SqlClient.SqlParameter> はクエリおよびストアド プロシージャにパラメーターを渡すために使用されます。

> [!NOTE]
> <xref:Microsoft.Data.SqlClient.SqlCommand> オブジェクトの破棄または <xref:Microsoft.Data.SqlClient.SqlCommand.Cancel%2A> の呼び出しでは、ストリーミング操作を取り消す必要があります。 アプリケーションが <xref:System.Threading.CancellationToken> を送信すると、取り消しは保証されません。

次の <xref:Microsoft.Data.SqlClient.SqlParameter.SqlDbType%2A> 型は、<xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A> の <xref:System.IO.Stream> を受け取ります。

- **Binary**

- **VarBinary**

次の <xref:Microsoft.Data.SqlClient.SqlParameter.SqlDbType%2A> 型は、<xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A> の <xref:System.IO.TextReader> を受け取ります。

- **Char**

- **NChar**

- **NVarChar**

- **Xml**

**Xml**<xref:Microsoft.Data.SqlClient.SqlParameter.SqlDbType%2A> 型は、<xref:System.Xml.XmlReader> の <xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A> を受け取ります。

<xref:Microsoft.Data.SqlClient.SqlParameter.SqlValue%2A> は、<xref:System.Xml.XmlReader>、<xref:System.IO.TextReader>、および <xref:System.IO.Stream> 型の値を受け取ることができます。

<xref:System.Xml.XmlReader>、<xref:System.IO.TextReader>、および <xref:System.IO.Stream> の各オブジェクトは、<xref:Microsoft.Data.SqlClient.SqlParameter.Size%2A> によって定義された値まで転送されます。

## <a name="sample----streaming-from-sql-server"></a>サンプル -- SQL Server からのストリーミング

次の Transact-SQL を使用して、サンプル データベースを作成します。

```sql
CREATE DATABASE [Demo]
GO
USE [Demo]
GO
CREATE TABLE [Streams] (
[id] INT PRIMARY KEY IDENTITY(1, 1),
[textdata] NVARCHAR(MAX),
[bindata] VARBINARY(MAX),
[xmldata] XML)
GO
INSERT INTO [Streams] (textdata, bindata, xmldata) VALUES (N'This is a test', 0x48656C6C6F, N'<test>value</test>')
INSERT INTO [Streams] (textdata, bindata, xmldata) VALUES (N'Hello, World!', 0x54657374696E67, N'<test>value2</test>')
INSERT INTO [Streams] (textdata, bindata, xmldata) VALUES (N'Another row', 0x666F6F626172, N'<fff>bbb</fff><fff>bbc</fff>')
GO
```

このサンプルでは、次の処理の実行方法を示します。

- 大きなファイルを非同期に取得できるようにして、ユーザー インターフェイス スレッドのブロックを回避する。

- .NET で SQL Server から大きなテキスト ファイルを転送する。

- .NET で SQL Server から大きな XML ファイルを転送する。

- SQL Server からデータを取得する。

- メモリ不足になることなく、ある SQL Server データベースから別のデータベースに大きなファイル (BLOB) を転送する。

[!code-csharp[SqlClient_Streaming_FromServer#1](~/../sqlclient/doc/samples/SqlClient_Streaming_FromServer.cs#1)]

## <a name="sample----streaming-to-sql-server"></a>サンプル -- SQL Server へのストリーミング

次の Transact-SQL を使用して、サンプル データベースを作成します。

```sql
CREATE DATABASE [Demo2]
GO
USE [Demo2]
GO
CREATE TABLE [BinaryStreams] (
[id] INT PRIMARY KEY IDENTITY(1, 1),
[bindata] VARBINARY(MAX))
GO
CREATE TABLE [TextStreams] (
[id] INT PRIMARY KEY IDENTITY(1, 1),
[textdata] NVARCHAR(MAX))
GO
CREATE TABLE [BinaryStreamsCopy] (
[id] INT PRIMARY KEY IDENTITY(1, 1),
[bindata] VARBINARY(MAX))
GO
```

このサンプルでは、次の処理の実行方法を示します。

- .NET で SQL Server に大きな BLOB を転送する。

- .NET で SQL Server に大きなテキスト ファイルを転送する。

- 新しい非同期機能を使用して大きな BLOB を転送する。

- 新しい非同期機能と Await キーワードを使用して大きな BLOB を転送する。

- 大きな BLOB の転送を取り消す。

- 新しい非同期機能を使用して 1 つの SQL Server から別の SQL Server にストリーミングする。

[!code-csharp[SqlClient_Streaming_ToServer#1](~/../sqlclient/doc/samples/SqlClient_Streaming_ToServer.cs#1)]

## <a name="sample----streaming-from-one-sql-server-to-another-sql-server"></a>サンプル -- 1 つの SQL Server から別の SQL Server へのストリーミング

このサンプルでは、大きな BLOB を SQL Server 間で非同期にストリーミングする方法を示します。取り消し処理がサポートされています。

> [!NOTE]
> 次のサンプルを実行する前に、Demo および Demo2 データベースが作成されていることを確認してください。

[!code-csharp[SqlClient_Streaming_ServerToServer#1](~/../sqlclient/doc/samples/SqlClient_Streaming_ServerToServer.cs#1)]

## <a name="see-also"></a>関連項目

- [ADO.NET でのデータの取得と変更](retrieving-modifying-data.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
