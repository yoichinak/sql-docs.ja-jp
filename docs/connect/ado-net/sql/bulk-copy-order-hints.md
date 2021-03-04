---
title: 一括コピー操作の順序のヒント
description: 一括コピー操作で順序のヒントを使用する方法について説明します。
ms.date: 06/15/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: v-daenge
ms.openlocfilehash: ba652ab9eb1cbe6564a8f1b2aa5d7309cba86ac4
ms.sourcegitcommit: 9413ddd8071da8861715c721b923e52669a921d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "101837109"
---
# <a name="order-hints-for-bulk-copy-operations"></a>一括コピー操作の順序のヒント

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

一括コピー操作を使用すると、SQL Server テーブルにデータを読み込む他の方法よりも、パフォーマンスが大幅に向上します。 順序のヒントを使用すると、パフォーマンスをさらに向上させることができます。 一括コピー操作に順序のヒントを指定すると、並べ替えられたデータをクラスター化インデックスを持つテーブルに挿入する時間を短縮することができます。

既定では、一括挿入操作では、受信データが並べ替えられていないことを前提に実行されます。 SQL Server では、このデータを一括読み込みする前に、データが強制的に並べ替えられます。 受信データが既に並べ替えられていることがわかっている場合は、順序のヒントを使用して、クラスター化インデックスの一部である任意のターゲット列の並べ替え順序について、一括コピー操作に指示できます。
  
## <a name="adding-order-hints-to-a-bulk-copy-operation"></a>一括コピー操作への順序のヒントの追加  
次の例では、**AdventureWorks** サンプル データベースのソース テーブルから、同じデータベース内のコピー先テーブルにデータを一括コピーします。 コピー先テーブルの **ProductNumber** 列の並べ替え順序を定義するための SqlBulkCopyColumnOrderHint オブジェクトが作成されます。 次に、順序のヒントが SqlBulkCopy インスタンスに追加されます。これにより、結果の `INSERT BULK` クエリに適切な順序のヒント引数が追加されます。

[!code-csharp [SqlBulkCopy.ColumnOrderHint#1](~/../sqlclient/doc/samples/SqlBulkCopy_ColumnOrderHint.cs#1)]

## <a name="next-steps"></a>次のステップ
- [SQL Server での一括コピー操作](bulk-copy-operations-sql-server.md)
