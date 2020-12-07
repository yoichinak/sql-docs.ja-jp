---
title: データ ラングリング タスクのコードを生成する
titleSuffix: Azure Data Studio
description: この記事では、Azure Data Studio の PROSE コード アクセラレータを使用して、一般的なデータ ラングリング タスクのコードを自動的に生成する方法について説明します。
author: dphansen
ms.author: davidph
ms.reviewer: mihaelab
ms.date: 10/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning-bdc
ms.openlocfilehash: 3357757c0cca35be0b3410795cfd89ca75f34dc3
ms.sourcegitcommit: 544706f6725ec6cdca59da3a0ead12b99accb2cc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/27/2020
ms.locfileid: "92638975"
---
# <a name="data-wrangling-using-prose-code-accelerator"></a>PROSE コード アクセラレータを使用したデータ ラングリング

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

PROSE コード アクセラレータでは、データ ラングリング タスク用の読み取り可能な Python コードが生成されます。 Azure Data Studio 内のノートブックで作業するときに、生成されたコードと手書きのコードを混在させることができます。

この記事では、コード アクセラレータの使用方法の概要について説明します。

 > [!NOTE]
 > Program Synthesis using Examples (PROSE ともいう) は、AI を使用して人間が判読できるコードを生成する Microsoft テクノロジです。 これは、ユーザーの意図とデータを分析し、いくつかの候補プログラムを生成し、順位付けアルゴリズムを使用して最適なプログラムを選択することによって行われます。 PROSE テクノロジの詳細については、[PROSE のホームページ](https://microsoft.github.io/prose/)を参照してください。

コード アクセラレータは、Azure Data Studio にプレインストールされています。 ノートブック内の他の Python パッケージと同様にインポートできます。 慣例により、これを略して cx としてインポートします。

```python
import prose.codeaccelerator as cx
```

現在のリリースでは、コード アクセラレータで次のタスクのために Python コードをインテリジェントに生成できます。

- Pandas または Pyspark データフレームにデータ ファイルを読み取る。
- データフレームでデータ型を修正する。
- 文字列のリストでパターンを表す正規表現を見つける。

コード アクセラレータ メソッドの概要については、[このドキュメント](/python/api/overview/azure/prose/intro)を参照してください。

## <a name="reading-data-from-a-file-to-a-dataframe"></a>ファイルからデータフレームへのデータの読み取り

ファイルをデータフレームに読み取るには、ファイルの内容を調べ、データ読み込みライブラリに渡す正しいパラメーターを特定する必要があります。

ファイルの複雑さによっては、正しいパラメーターを識別するために複数の反復処理が必要になる場合があります。

PROSE コード アクセラレータでは、データ ファイルの構造を分析し、ファイルを読み込むコードを自動的に生成することで、この問題を解決します。 通常は、生成されたコードによってデータが正しく解析されます。 場合によっては、ニーズに合わせてコードの調整が必要になることがあります。

次の例を確認してください。

 ```python
import prose.codeaccelerator as cx

# Call the ReadCsvBuilder builder to analyze the file content and generate code to load it
builder = cx.ReadCsvBuilder(r'C:/911.txt')

#Set target to pyspark if generating code to use pyspark library
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
 ```

前のコード ブロックでは、区切られたファイルを読み取るために次の python コードが出力されます。 PROSE で、スキップする行の数、ヘッダー、quotechar、区切り記号などを自動的に判別する方法に注目してください。

 ```python
import pandas as pd

def read_file(file):
    names = ["lat",
             "lng",
             "desc",
             "zip",
             "title"]

    df = pd.read_csv(file,
        skiprows = 11,
        header = None,
        names = names,
        quotechar = "\"",
        delimiter = "|",
        index_col = False,
        dtype = str,
        na_values = [],
        keep_default_na = False,
        skipinitialspace = True)
    return df
 ```

コード アクセラレータでは、区切られたファイル、JSON ファイル、および固定幅のファイルをデータフレームに読み込むコードを生成できます。 固定幅のファイルを読み取る場合、`ReadFwfBuilder` では必要に応じて、列の位置を取得するために解析できる、人間が判読できるスキーマ ファイルを受け取ります。 詳細については、[このドキュメント](/python/api/overview/azure/prose/intro)を参照してください。

## <a name="fixing-data-types-in-a-dataframe"></a>データフレームでのデータ型の修正

一般に、pandas や pyspark データフレームのデータ型は正しくありません。 正しくないデータ型は、列に非準拠の値がいくつかあることが原因で発生します。 その結果、整数はフロートまたは文字列として読み取られ、日付は文字列として読み取られます。 データ型を手動で修正するために必要な作業は、列の数に比例します。

このような状況では、`DetectTypesBuilder` を使用できます。 それによって、データが分析され、データ型を修正するコードが生成されます。 このコードは開始点として機能します。 これを確認、使用、または必要に応じて変更することができます。

```python
import prose.codeaccelerator as cx

builder = cx.DetectTypesBuilder(df)

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
```

詳細については、[このドキュメント](/python/api/overview/azure/prose/fixdatatypes)を参照してください。

## <a name="identifying-patterns-in-strings"></a>文字列でのパターンの識別

p.


|行|名前                      |BirthDate      |
|--:|:-------------------------|:--------------|
| 0 |Bertram du Plessis        |1995           |
| 1 |Naiara Moravcikova        |Unknown        |
| 2 |Jihoo Spel                |2014           |
| 3 |Viachaslau Gordan Hilario |22-Apr-67      |
| 4 |Maya de Villiers          |19-Mar-60      |

データ内のボリュームと多様性によっては、列内のさまざまなパターンの正規表現を記述することが非常に時間のかかるタスクになることがあります。 `FindPatternsBuilder` は、文字列のリストに対して正規表現を生成することによって、上記の問題を解決する強力なコード アクセラレーション ツールです。

```python
import prose.codeaccelerator as cx

builder = cx.FindPatternsBuilder(df['BirthDate'])

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

builder.learn().regexes
```

上述のデータの `FindPatternsBuilder` によって生成される正規表現を以下に示します。

```
^[0-9]{2}-[A-Z][a-z]+-[0-9]{2}$
^[0-9]{2}[\s][A-Z][a-z]+[\s][0-9]{4}$
^[0-9]{4}$
^Unknown$
```

正規表現の生成とは別に、`FindPatternsBuilder` では、生成される正規表現に基づいて値をクラスター化するためのコードを生成することもできます。 また、列のすべての値が、生成される正規表現に準拠していることをアサートすることもできます。 その他の役立つシナリオの詳細については、[このドキュメント](/python/api/overview/azure/prose/findpatterns)を参照してください。