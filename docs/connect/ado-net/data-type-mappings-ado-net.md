---
title: データ型マッピング
description: Microsoft SqlClient Data Provider for SQL Server によって使用されるデータ型について説明します。
ms.date: 11/13/2020
ms.assetid: d4afab94-ada6-4c77-a73c-41f17bae6b5a
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 03af2a8544763aab7609fd713790622bbb1bfef4
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/01/2020
ms.locfileid: "96419764"
---
# <a name="data-type-mappings-in-adonet"></a>ADO.NET のデータ型のマッピング

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

ADO.NET は、ランタイムでの型の宣言、使用、および管理の方法を定義する、共通型システムに基づいています。 値型と参照型の両方から構成されており、これらはすべて <xref:System.Object> 基本型から派生します。 データ ソースを操作するときは、データ型が明示的に指定されていない場合はデータ プロバイダーから推論されます。 たとえば、<xref:System.Data.DataSet> オブジェクトは、特定のデータ ソースには依存しません。 `DataSet` 内のデータはデータ ソースから取得され、変更は `DataAdapter` によってデータ ソースに反映されます。 `DataAdapter` によってデータ ソースの値を使用して `DataSet` の <xref:System.Data.DataTable> が入力されると、生成される `DataTable` の列のデータ型は、データ ソースへの接続に使用される Microsoft SqlClient Data Provider for SQL Server に固有の型ではなく、.NET Framework 型になることをこのプログラム フローは意味します。

同様に、`DataReader` によってデータ ソースから値が返されるとき、結果の値は .NET Framework 型のローカル変数に格納されます。 `DataAdapter` の `Fill` 操作と `DataReader` の `Get` メソッドのどちらの場合も、.NET Framework 型は Microsoft SqlClient Data Provider for SQL Server から返された値から推論されます。

返される値の型がわかっている場合は、推論されるデータ型を使用するのではなく、`DataReader` の型指定されたアクセサー メソッドを使用できます。 型指定されたアクセサー メソッドを使用して .NET Framework の特定の型として値を返すと、追加の型変換が不要になるため、パフォーマンスが向上します。

> [!NOTE]
> Microsoft SqlClient Data Provider for SQL Server データ型の null 値は `DBNull.Value` によって表されます。

## <a name="in-this-section"></a>このセクションの内容

[SQL Server のデータ型のマッピング](sql-server-data-type-mappings.md) 推論されるデータ型のマッピングと <xref:Microsoft.Data.SqlClient> のデータ アクセサー メソッドの一覧を示します。

[浮動小数点数](floating-point-numbers.md) 開発者が浮動小数点数を操作するときに頻繁に発生する問題について説明します。

## <a name="see-also"></a>関連項目

- [SQL Server データ型と ADO.NET](./sql/sql-server-data-types.md)
- [パラメーターの構成](configure-parameters.md)
