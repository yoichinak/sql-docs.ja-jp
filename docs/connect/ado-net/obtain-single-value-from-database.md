---
title: データベースからの単一の値の取得
description: ADO.NET で単一の値を返す方法について説明します。 このコード例は、挿入されたレコードの ID 列の値を返します。
ms.date: 11/25/2020
dev_langs:
- csharp
ms.assetid: b38526cd-a62a-48cb-822a-e91dfa68e02d
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 3937c1d4617f3cecb9012d82d590f75634ab1043
ms.sourcegitcommit: c938c12cf157962a5541347fcfae57588b90d929
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2020
ms.locfileid: "97771494"
---
# <a name="obtaining-a-single-value-from-a-database"></a>データベースからの単一の値の取得

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

テーブルやデータ ストリームの形式ではなく、単に 1 つの値をデータベース情報として返すことが必要な場合があります。 たとえば、COUNT(\*)、SUM(Price)、AVG(Quantity) などの集計関数の結果を返す場合です。 **Command** オブジェクトでは、**ExecuteScalar** メソッドを使用して単一の値を返す機能が提供されています。 **ExecuteScalar** メソッドでは、結果セットの 1 行目の 1 列目の値がスカラー値として返されます。

## <a name="example"></a>例

<xref:Microsoft.Data.SqlClient.SqlCommand> を使用して新しい値をデータベースに挿入するコード サンプルを次に示します。 挿入したレコードの ID 列の値を取得するために、<xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteScalar%2A> メソッドが使用されています。

[!code-csharp[DataWorks SqlCommand.ExecuteScalar#1](~/../sqlclient/doc/samples/SqlCommand_ExecuteScalar_Return_Id.cs#1)]

## <a name="see-also"></a>関連項目

- [コマンドとパラメーター](commands-parameters.md)
- [コマンドの実行](execute-command.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
