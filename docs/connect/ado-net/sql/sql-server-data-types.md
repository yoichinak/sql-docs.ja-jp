---
title: SQL Server のデータ型と ADO.NET
description: SQL Server データ型を操作する方法と、.NET データ型を操作する方法について説明します。
ms.date: 08/15/2019
ms.assetid: 81b43550-23e8-43bb-b460-7eb8ac825c33
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 57e0cec178c407cda530e6699e51743094c57dca
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725593"
---
# <a name="sql-server-data-types-and-adonet"></a>SQL Server のデータ型と ADO.NET

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server と .NET は異なる型システムに基づいているため、データ損失の可能性があります。 データの整合性を確保するために、Microsoft SqlClient Data Provider for SQL Server (<xref:Microsoft.Data.SqlClient>) には、SQL Server データを操作するための型指定されたアクセサー メソッドが用意されています。 <xref:System.Data.SqlDbType> クラスの列挙値を使用して、<xref:Microsoft.Data.SqlClient.SqlParameter> データ型を指定できます。  
  
SQL Server 2008 では、業務上のニーズに対応して、日時データ、構造化データ、半構造化データ、および非構造化データを扱うための新しいデータ型が導入されました。 新しいデータ型は、SQL Server 2008 オンライン ブックで説明されています。  
  
アプリケーションで使用可能な SQL Server のデータ型は、使用する SQL Server のバージョンによって異なります。 詳細については、SQL Server オンライン ブックの「[データ型 (データベース エンジン)](/previous-versions/sql/sql-server-2008-r2/ms187594(v=sql.105))」 を参照してください。
  
## <a name="in-this-section"></a>このセクションの内容  
[SqlTypes と DataSet](sqltypes-dataset.md)  
`SqlTypes` 内の `DataSet` に対する型のサポートについて説明します。  
  
[null 値の処理](handle-null-values.md)  
null 値と 3 値ロジックの使用例を示します。  
  
[GUID と uniqueidentifier 値の比較](compare-guid-uniqueidentifier-values.md)  
SQL Server と .NET で GUID と uniqueidentifier 値を操作する方法について説明します。  
  
[日付型と時刻型のデータ](date-time-data.md)  
SQL Server 2008 で導入された新しい日付と時刻のデータ型の使用方法について説明します。  
  
[大きな UDT](large-udts.md)  
SQL Server 2008 で導入された大きな値の UDT からデータを取り出す方法の例を示します。  
  
[SQL Server における XML データ](xml-data-sql-server.md)  
SQL Server から取得した XML データを使用する方法について説明します。  
  
## <a name="reference"></a>関連項目  
<xref:System.Data.DataSet>  
`DataSet` クラスおよびそのすべてのメンバーについて説明します。  
  
<xref:System.Data.SqlTypes>  
`SqlTypes` 名前空間およびそのすべてのメンバーについて説明します。  
  
<xref:System.Data.SqlDbType>  
`SqlDbType` 列挙体およびそのすべてのメンバーについて説明します。  
  
<xref:System.Data.DbType>  
`DbType` 列挙型およびそのすべてのメンバーについて説明します。  
  
## <a name="next-steps"></a>次のステップ
- [テーブル値パラメーター](table-valued-parameters.md)
- [SQL Server のバイナリ データと大きな値のデータ](sql-server-binary-large-value-data.md)