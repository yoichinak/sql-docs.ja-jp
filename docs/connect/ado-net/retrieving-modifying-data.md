---
title: データの取得と変更
description: .NET Framework の Microsoft SqlClient Data Provider for SQL Server は、データを読み取って更新するための、アプリケーションとデータ ソース間のブリッジとして機能します。
ms.date: 11/13/2020
ms.assetid: 722e7f87-3691-46c6-87e8-7d159722d675
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: cbe61aafd8dcd1681230c355187a65a231535e00
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126462"
---
# <a name="retrieving-and-modifying-data-in-adonet"></a>ADO.NET でのデータの取得と変更

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

データベース アプリケーションの主な機能は、データ ソースとの接続およびデータベースに格納されているデータの取得です。 SqlClient データ プロバイダーは、アプリケーションとデータ ソースの間のブリッジとして機能し、**DataReader** または **DataAdapter** を使用することで、コマンドを実行したり、データを取得したりできます。 データベースに格納されているデータを更新する機能は、データベース アプリケーションの重要な機能の 1 つです。 Microsoft SqlClient Data Provider for SQL Server でデータを更新するには、**DataAdapter** と <xref:System.Data.DataSet>、および **Command** オブジェクトを使用する必要があります。また、トランザクションを使用することが必要になる場合もあります。

## <a name="in-this-section"></a>このセクションの内容

[データ ソースへの接続](connecting-to-data-source.md) データ ソースへの接続を確立する方法と、接続イベントを使用する方法について説明します。

[接続文字列](connection-strings.md) 接続文字列のキーワード、セキュリティ情報、セキュリティ情報の格納や取得など、接続文字列を使用するときのさまざまな側面に関して説明するトピックが含まれます。

[接続プール](connection-pooling.md) Microsoft SqlClient Data Provider for SQL Server の接続プールについて説明します。

## <a name="see-also"></a>関連項目

- [ADO.NET でのデータ型のマッピング](data-type-mappings-ado-net.md)
- [SQL Server と ADO.NET](./sql/index.md)
