---
title: バックグラウンドでの Azure Synapse Pathway プレビュー。
description: Azure Synapse Pathway によるコードの翻訳方法に関する技術的な詳細。
author: anshul82-ms
ms.author: anrampal.
ms.prod: sql
ms.technology: Azure Synapse Pathway
ms.topic: conceptual
ms.date: 03/02/2021
monikerRange: =azure-sqldw-latest
ms.custom: template-concept
ms.openlocfilehash: dbd362e53b5bfcd916c53e90d6f66c8fb44f0374
ms.sourcegitcommit: 9413ddd8071da8861715c721b923e52669a921d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "101873079"
---
# <a name="azure-synapse-pathway-preview-behind-the-scenes"></a>バックグラウンドでの Azure Synapse Pathway プレビュー
[!INCLUDE [Azure Synapse Analytics](../../includes/applies-to-version/asa.md)]

Azure Synapse Pathway の目標は、Synapse SQL 用に最適化しながら元のコードの機能上の意図を維持することです。 Synapse Pathway では、ソース システムから Azure Synapse SQL に SQL コードを翻訳するために 3 つのステージからなるプロセスを使用します。

各ステージでは、ソース固有のメタデータを含むソースの知識を維持して拡張することで、翻訳における最高品質を保証します。

 ![Azure Synapse Pathway。](./media/technical-deep-dive/behind-the-scene.png)

## <a name="stage-1--lexing-and-parsing"></a>ステージ 1 – 字句解析と構文解析

SQL 言語の構文解析は、何度も解決されてきた問題です。 ソース ステートメントを取得し、それを論理トークンに分割してから、セットまたはパーサー規則に対して実行して言語の一貫性を確保するための、多くの商用およびオープンソースのパーサーがあります。 

Synapse Pathway では、ツールで SQL 入力を識別して処理し、さらに処理するために使用される拡張抽象構文ツリー (AST) を作成できるようにするソース文法を定義します。 

## <a name="stage-2---augmented-abstract-syntax-tree-ast"></a>ステージ 2 - 拡張抽象構文ツリー (AST)

Synapse Pathway では、拡張抽象構文ツリー (AST) 内のすべてのオブジェクトの共通表現を定義します。 Synapse Pathway AST には、2 つのシステム間でコードを翻訳するときに適切な決定を行うために使用される、追加のステートメントまたはフラグメント化されたメタデータが含まれています。

トークンが関数であることだけでなく、ソース システムの種類の要件を追跡することで、スクリプト生成コンポーネントでは Synapse SQL への翻訳について、より賢明な決定を行うことができます。

たとえば、絶対関数のソース関数は次のように定義されます。

```sql  
ABS( float_expression ) 
```

Azure Synapse SQL では、次のように絶対関数を定義します。

```sql  
ABS ( numeric_expression )  
```

このシンプルなケースの場合、Synapse Pathway で、Synapse SQL での float から numeric への変換が暗黙的な[変換](../../t-sql/functions/cast-and-convert-transact-sql?view=azure-sqldw-latest#implicit-conversions)であることが認識され、それ以上の型キャストは必要ありません。 シンプルなクリーンで効果的なコード翻訳。

ソースのステートメントとフラグメントに関するこのメタ情報を維持することは、プラットフォーム間に構造的な違いがある場合に役立ちます。たとえば、WHERE 句の検索条件述語のオプトアウト ロジックでの変換などです。

## <a name="stage-3---syntax-generation"></a>ステージ 3 - 構文の生成

プロセスの最後のステージでは、Synapse SQL の構文を生成します。 ソース ファイルから生成された AST 構造体を使用して、Synapse Pathway によって各 DDL オブジェクトが個々のファイルに書き込まれます。 構文ジェネレーターでは、ターゲット プラットフォームに関する詳細な知識を使用してステートメントが最適化されます。

たとえば、データ読み込みシナリオで見られる一般的なパターンでは、まずステージング テーブル内のすべての内容を削除してから、別のステージング テーブルのデータを INSERT または SELECT の方法で読み込みます。

```sql  
DELETE staging.table1 ALL;
INSERT INTO staging.table1…
FROM staging.table2;
```

Synapse SQL には、このシナリオのために最適化されたパス ([CREATE TABLE AS SELECT](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-develop-ctas)) があります。 CTAS ステートメントはバッチ ベースの操作であり、利用可能なすべてのコンピューティング インフラストラクチャを使用することにより、最小のログ記録で高いパフォーマンスが得られます。 Synapse SQL に関するこの分析情報がないと、多くの場合、ツールでは truncate および INSERT または SELECT ステートメントが生成されます。

```sql  
TRUNCATE TABLE staging.table1;
INSERT INTO staging.table1…
FROM staging.table2;
```

問題はありませんが、このコードを DROP TABLE と CTAS に最適化して、パフォーマンスを向上させることができます。

```sql  
DROP TABLE staging.table1;
CREATE TABLE staging.table1
WITH
(
    -- Derived from the original table definition 
    DISTRIBUTION = HASH(column1),
    -- Derived from the original table definition
    CLUSTERED COLUMNSTORE INDEX
)
AS SELECT  * FROM staging.table2;
```

## <a name="next-steps"></a>次のステップ

- [Azure Synapse Pathway をダウンロードする](synapse-pathway-download.md)
- [FAQ](pathway-faq.md)

