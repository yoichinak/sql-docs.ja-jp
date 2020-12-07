---
description: PolyBase でのプッシュダウン計算
title: PolyBase でのプッシュダウン計算 | Microsoft Docs
dexcription: Enable pushdown computation to improve performance of queries on your Hadoop cluster. You can select a subset of rows/columns in an external table for pushdown.
ms.date: 11/17/2020
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: 59ff1e7807a8bdd8427e3b902bf53c111d52c7b7
ms.sourcegitcommit: 4c3949f620d09529658a2172d00bfe37aeb1a387
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2020
ms.locfileid: "96127844"
---
# <a name="pushdown-computations-in-polybase"></a>PolyBase でのプッシュダウン計算

[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

プッシュダウン計算を使用すると、外部データ ソースに対するクエリのパフォーマンスが向上します。 SQL Server 2016 以降では、プッシュダウン計算は Hadoop の外部データ ソースで使用できました。 SQL Server 2019 には、他の種類の外部データ ソースのプッシュダウン計算が導入されています。

## <a name="enable-pushdown-computation"></a> プッシュダウン計算を有効にする

次の記事には、特定の種類の外部データ ソース用のプッシュダウン計算の構成に関する情報が含まれています。

- [Enable pushdown computation in Hadoop (Hadoop でのプッシュダウン計算を有効にする)](polybase-configure-hadoop.md#pushdown)
- [Oracle 上の外部データにアクセスするための PolyBase の構成](polybase-configure-oracle.md)
- [Teradata 上の外部データにアクセスするための PolyBase の構成](polybase-configure-teradata.md)
- [MongoDB 上の外部データにアクセスするための PolyBase の構成](polybase-configure-mongodb.md)
- [ODBC ジェネリック型の外部データにアクセスするための PolyBase の構成](polybase-configure-odbc-generic.md)
- [SQL Server 上の外部データにアクセスするための PolyBase の構成](polybase-configure-sql-server.md)

## <a name="select-a-subset-of-rows"></a>行のサブセットを選択する

外部テーブルから行のサブセットを選択するクエリのパフォーマンスを改善するには、述語のプッシュダウンを使用します。

この例では、SQL Server 2016 は map-reduce ジョブを開始して、Hadoop で述語 `customer.account_balance < 200000` である行を取得します。 このクエリは、テーブルのすべての行をスキャンせずに完了できるため、述語の条件に合う行のみが SQL Server にコピーされます。 この方法で時間が大幅に短縮され、残高が 200000 未満の顧客数が、口座残高が 200000 以上の顧客数と比較して少ない場合に、一時的な記憶域が少なくなります。

```sql
SELECT * FROM customer WHERE customer.account_balance < 200000
SELECT * FROM SensorData WHERE Speed > 65;  
```

### <a name="select-a-subset-of-columns"></a>列のサブセットを選択する

外部テーブルから列のサブセットを選択するクエリのパフォーマンスを改善するには、述語のプッシュダウンを使用します。

このクエリでは、SQL Server で map-reduce ジョブを開始し、Hadoop の区切られたテキスト ファイルを前処理して、customer.name および customer.zip_code という 2 列のデータのみが SQL Server にコピーされるようにします。

```sql
SELECT customer.name, customer.zip_code
FROM customer
WHERE customer.account_balance < 200000
```

### <a name="pushdown-for-basic-expressions-and-operators"></a>基本的な式と演算子のプッシュダウン

SQL Server では、述語のプッシュダウンに次の基本的な式と演算子を使用できます。

- 数値、日付値、時間値の 2 項比較演算子 (`<`、`>`、`=`、`!=`、`<>`、`>=`、`<=`)。
- 算術演算子 (`+`、`-`、`*`、`/`、`%`)。
- 論理演算子 (`AND`、`OR`)。
- 単項演算子 (`NOT`、`IS NULL`、`IS NOT NULL`)。

`BETWEEN`、`NOT`、`IN`、および `LIKE` の演算子がプッシュダウンされる場合があります。 実際の動作は、クエリ オプティマイザーが演算子式をどのように基本的な関係演算子を使用する一連のステートメントとして書き換えるかに依存します。

この例のクエリには、Hadoop にプッシュダウンできる述語が複数あります。 SQL Server は、map-reduce ジョブを Hadoop にプッシュして、述語 `customer.account_balance <= 200000` を実行できます。 `BETWEEN 92656 AND 92677` の式もまた、Hadoop にプッシュできる 2 項演算子と論理演算子とで構成されます。 `customer.account_balance AND customer.zipcode` 内の論理 **積** が最後の式です。

この述語の組み合わせで、map-reduce ジョブですべての WHERE 句を実行できます。 `SELECT` 条件を満たすデータのみが SQL Server にコピーされて戻されます。

```sql
SELECT * FROM customer 
WHERE customer.account_balance <= 200000 
    AND customer.zipcode BETWEEN 92656 AND 92677
```

## <a name="examples"></a>例

### <a name="force-pushdown"></a>プッシュダウンを強制する

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (FORCE EXTERNALPUSHDOWN);
```

### <a name="disable-pushdown"></a>プッシュダウンを無効にする

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (DISABLE EXTERNALPUSHDOWN);
```

## <a name="next-steps"></a>次のステップ

PolyBase について詳しくは、「[PolyBase とは](polybase-guide.md)」をご覧ください。
