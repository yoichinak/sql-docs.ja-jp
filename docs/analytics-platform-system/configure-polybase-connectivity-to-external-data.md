---
title: PolyBase 接続の構成
description: Parallel Data Warehouse で PolyBase を構成して、外部の Hadoop または Microsoft Azure storage blob データソースに接続する方法について説明します。 PolyBase を使用して、Hadoop、Azure blob ストレージ、並列データウェアハウスなどの複数のソースからのデータを統合するクエリを実行します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 98527bf770da61c98368171e75b3a9b82ceba13c
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767181"
---
# <a name="configure-polybase-connectivity"></a>PolyBase 接続の構成
PolyBase を使用すると、Analytics Platform System (APS) が、外部データソースに対してデータの読み取りと書き込みを行うことができる Transact-sql クエリを処理できます。 外部データにアクセスするのと同じクエリで、関連テーブルを APS に含めることもできます。 これにより、外部ソースのデータと、APS データベースの価値の高いリレーショナルデータを組み合わせることができます。

![PolyBase 論理](media/polybase/polybase-logical.png)

APS の PolyBase では、Hadoop (HDFS) ファイルシステムと Azure Blob Storage の読み取りと書き込みがサポートされています。 PolyBase では、一部の計算を mapreduce ジョブとして Hadoop ノードにプッシュして、クエリの全体的なパフォーマンスを最適化することもできます。 APS の PolyBase は、区切られたテキスト、ORC、および Parquet ファイルに対して動作できます。 詳細な説明とその機能については、「 [PolyBase とは](../relational-databases/polybase/polybase-guide.md) 」を参照してください。

> [!NOTE]
> 現在、APS では、standard 汎用 v1 のローカル冗長 (LRS) Azure Blob Storage のみがサポートされています。

## <a name="features-and-limitations"></a>機能および制限事項
使用可能な PolyBase 機能の概要と、AP およびその他の SQL Server 製品に関する既知の制限事項については、「 [機能と制限](../relational-databases/polybase/polybase-versioned-feature-summary.md) 」を参照してください。

> [!NOTE] 
> 残りの PolyBase 関連記事では、APS 2016 (AU6) 以降で PolyBase を構成する方法について説明します。

## <a name="see-also"></a>参照
- [Hadoop](polybase-configure-hadoop.md)
- [Azure Blob Storage](polybase-configure-azure-blob-storage.md)
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
