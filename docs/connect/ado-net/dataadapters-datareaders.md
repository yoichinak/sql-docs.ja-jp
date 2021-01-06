---
title: DataAdapter と DataReader
description: データベースからデータを取得する Microsoft SqlClient Data Provider for SQL Server DataReader、およびデータ ソースからデータを取得して DataSet を作成する DataAdapter について説明します。
ms.date: 11/30/2020
ms.assetid: cc952ca2-ec19-46ab-9189-15174b52cb74
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 3a252ca44683c062e531081f0b625a5e2359d236
ms.sourcegitcommit: c938c12cf157962a5541347fcfae57588b90d929
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2020
ms.locfileid: "97771391"
---
# <a name="dataadapters-and-datareaders"></a>DataAdapter と DataReader

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Microsoft SqlClient Data Provider for SQL Server **DataReader** を使用すると、データベースから前方への読み取り専用のストリームを取得できます。 結果はクエリを実行すると返され、**DataReader** の **Read** メソッドを使用して要求するまで、クライアントのネットワーク バッファーに格納されます。 **DataReader** を使用すると、アプリケーションのパフォーマンスが向上します。これは、使用可能になったデータをすぐに取得するためと、一度に 1 つの行しかメモリに格納しない (既定の設定) ことによってシステムのオーバーヘッドが軽減されるためです。

<xref:System.Data.Common.DataAdapter> は、データ ソースからデータを取得し、1 つの <xref:System.Data.DataSet> 内でテーブルを設定するために使用されます。 また、`DataAdapter` は、`DataSet` に対して加えられた変更をデータ ソースに反映させます。 `DataAdapter` は、Microsoft SqlClient Data Provider for SQL Server の `Connection` オブジェクトを使用してデータ ソースに接続し、`Command` オブジェクトを使用して、データ ソースに対するデータの取得および変更の解決を行います。

.NET には <xref:System.Data.Common.DbDataReader> と <xref:System.Data.Common.DbDataAdapter> のオブジェクトがあります。Microsoft SqlClient Data Provider for SQL Server には、<xref:Microsoft.Data.SqlClient.SqlDataReader> と <xref:Microsoft.Data.SqlClient.SqlDataAdapter> のオブジェクトが含まれています。

## <a name="in-this-section"></a>このセクションの内容

[DataReader によってデータを取得する](retrieve-data-by-datareader.md)  
ADO.NET の **DataReader** オブジェクトと、それを使用してデータ ソースから結果ストリームを返す方法について説明します。

[DataAdapter から DataSet を設定する](populate-dataset-from-dataadapter.md)  
`DataSet` を使用して `DataAdapter` にテーブル、列、および行を設定する方法について説明します。

[DataAdapter パラメーター](dataadapter-parameters.md)  
`DataAdapter` のコマンド プロパティのパラメーターを使用する方法と、`DataSet` の列の内容をコマンド パラメーターに割り当てる方法について説明します。

[DataSet に既存の制約を追加する](add-existing-constraints-to-dataset.md)  
既存の制約を `DataSet` に追加する方法について説明します。

[DataAdapter、DataTable、DataColumn のマッピング](dataadapter-datatable-datacolumn-mappings.md)  
`DataTableMappings` の `ColumnMappings` および `DataAdapter` を設定する方法について説明します。

[クエリ結果のページング](paging-through-query-result.md)  
クエリの結果をデータ ページとして表示する例を示します。

[DataAdapter を使用してデータ ソースを更新する](update-data-sources-with-dataadapters.md)  
`DataAdapter` を使用して `DataSet` の変更内容を解決してデータベースに戻す方法について説明します。

[DataAdapter イベントを処理する](handle-dataadapter-events.md)  
`DataAdapter` のイベントおよびその使用方法について説明します。

[DataAdapter を使用したバッチ操作](batch-operations-using-dataadapters.md)  
`DataSet` から更新を適用する際に、SQL Server へのラウンド トリップ回数を減らすことにより、アプリケーションのパフォーマンスを向上させる方法について説明します。

## <a name="see-also"></a>関連項目

- [データ ソースへの接続](connecting-to-data-source.md)
- [コマンドとパラメーター](commands-parameters.md)
- [トランザクションとコンカレンシー](transactions-and-concurrency.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
