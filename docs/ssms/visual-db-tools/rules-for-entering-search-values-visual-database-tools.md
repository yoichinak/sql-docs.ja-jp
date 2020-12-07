---
description: 検索値を入力するときの規則 (Visual Database Tools)
title: 検索値を入力するときのルール
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- time [SQL Server], searches
- date searches
- dates [SQL Server], searches
- embedding apostrophes [SQL Server]
- logical value searches [SQL Server]
- case-sensitive search matches
- search criteria [SQL Server], rules
- text value searches [SQL Server]
- numeric value searches [SQL Server]
ms.assetid: 3c8134b7-83f4-41b4-99c8-e3949a685ff5
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 6943034cbad433254c576d68a631d45be470b49c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462722"
---
# <a name="rules-for-entering-search-values-visual-database-tools"></a>検索値を入力するときの規則 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
このトピックでは、検索条件に対して次の種類のリテラル値を入力するときに従う規則について説明します。  
  
-   文字列値  
  
-   数値  
  
-   日付  
  
-   論理値  
  
> [!NOTE]  
> このトピックの情報は、標準の SQL-92 に対する規則に基づいていますが、 各データベースは SQL を独自の方法で実装している場合があります。 したがって、ここに示すガイドラインはすべての場合に当てはまるわけではありません。 特定のデータベースでの検索値の入力方法に関して不明な点がある場合は、使用しているデータベースのドキュメントを参照してください。  
  
## <a name="searching-on-text-values"></a>文字列値の検索  
次の規則は、検索条件に文字列値を入力するときに適用されます。  
  
-   **引用符** : 次に示す姓の例のように、文字列値は単一引用符で囲みます。  
  
    ```  
    'Smith'  
    ```  
  
    [抽出条件ペイン](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)で検索条件を入力する場合は、単に文字列値を入力するだけです。クエリおよびビュー デザイナーにより、自動的に単一引用符が付加されます。  
  
    > [!NOTE]  
    > 一部のデータベースでは、単一引用符で囲まれた項目がリテラル値として解釈され、二重引用符で囲まれた項目が列やテーブル参照などのデータベース オブジェクトとして解釈されます。 このため、クエリおよびビュー デザイナーでは二重引用符で囲まれた項目も受け入れることができますが、その項目が期待どおりに解釈されるとは限りません。  
  
-   **アポストロフィの埋め込み** : 検索するデータに単一引用符 (アポストロフィ) が含まれる場合は、その単一引用符が区切り記号でなくリテラル値であることを示すために、2 つの単一引用符を入力します。 たとえば、次の条件は "Swann's Way" という値を検索します。  
  
    ```  
    ='Swann''s Way'  
    ```  
  
-   **長さの制限** : 長い文字列を入力するときには、データベースにおける SQL ステートメントの最大長を超えないようにします。  
  
-   **大文字小文字の区別** : 使用しているデータベースの大文字小文字の区別の規則に従います。 使用しているデータベースによって、文字列の検索で大文字小文字が区別されるかどうかが異なります。 たとえば、あるデータベースでは演算子 "=" は厳密に大文字小文字を区別した一致を意味しますが、別のデータベースでは大文字と小文字の任意の組み合わせの一致が許されます。  
  
    データベースで大文字小文字が区別して検索されるかどうかがわからない場合は、次の例に示すように、検索条件で UPPER 関数または LOWER 関数を使用して検索データを大文字または小文字に変換してください。  
  
    ```  
    WHERE UPPER(lname) = 'SMITH'  
    ```  
  
## <a name="searching-on-numeric-values"></a>数値の検索  
次の規則は、検索条件に数値を入力するときに適用されます。  
  
-   **引用符** : 数値は引用符で囲まないでください。  
  
-   **数値以外の文字** : 小数点記号 (Windows コントロール パネルの **[地域のオプション]** ダイアログ ボックスで定義) と負の符号 (-) を除き、非数値文字を入力することはできません。 桁区切り記号 (3 桁ごとに挿入されるコンマなど) や通貨記号を入力することはできません。  
  
-   **小数点** : 数を入力するときは、検索する値が整数か実数かに関係なく、小数点を含めることができます。  
  
-   **指数表記** : 非常に大きな数や非常に小さな数は、次の例のように指数表記で入力できます。  
  
    ```  
    > 1.23456e-9  
    ```  
  
## <a name="searching-on-dates"></a>日付の検索  
日付を入力するときに使用する形式は、使用しているデータベースによって異なります。また、クエリおよびビュー デザイナーのどのペインに日付を入力するかによっても異なります。  
  
> [!NOTE]  
> データ ソースが使用している形式が不明な場合は、抽出条件ペインのフィルター列に任意の形式で日付を入力してください。 クエリおよびビュー デザイナーは、このような入力のほとんどを適切な形式に変換します。  
  
クエリおよびビュー デザイナーは、次の日付形式を処理できます。  
  
-   **ロケール固有** : Windows の **[地域のオプション]** ダイアログ ボックスで指定された日付の形式。  
  
-   **データベース固有** : データベースによって認識される任意の形式。  
  
-   **ANSI 標準日付** : 次の例のように、中かっこ ({})、日付を指定するマーカー 'd'、および日付の文字列を使用する形式。  
  
    ```  
    { d '1990-12-31' }  
    ```  
  
-   **ANSI 標準日付/時刻** : ANSI 標準日付に似ていますが、'd' の代わりに 'ts' を使用し、日付に時、分、秒 (24 時間表記) を付加します。1990 年 12 月 31 日の例を次に示します。  
  
    ```  
    { ts '1990-12-31 00:00:00' }  
    ```  
  
    一般に、通常の日付型を使用して日付を表現するデータベースでは、ANSI 標準の日付形式が使用されます。 一方、datetime データ型をサポートするデータベースでは、datetime 形式が使用されます。  
  
次の表は、クエリおよびビュー デザイナーの各ペインで使用できる日付形式を示しています。  
  
|**ペイン**|**日付の形式**|  
|------------|-------------------|  
|条件|ロケール固有&#x2028;データベース固有&#x2028;ANSI 標準<br /><br />[抽出条件ペイン](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md) で入力された日付は、SQL ペインではデータベース互換の形式に変換されます。|  
|SQL|データベース固有&#x2028;ANSI 標準|  
|結果|ロケール固有|  
  
## <a name="searching-on-logical-values"></a>論理値の検索  
論理データの形式はデータベースごとに異なります。 多くのデータベースで、False の値はゼロ (0) として格納されます。 多くのデータベースでは、True の値は 1 として格納されます。ただし、True の値を -1 として格納するデータベースもあります。 検索条件に論理値を入力するときには、次のガイドラインが適用されます。  
  
-   False の値を検索する場合は、次の例のようにゼロを使用します。  
  
    ```  
    SELECT * FROM authors  
    WHERE contract = 0  
    ```  
  
-   True の値を検索するときにどの形式を使用するかわからない場合は、次の例のように 1 を使用します。  
  
    ```  
    SELECT * FROM authors  
    WHERE contract = 1  
    ```  
  
-   または、次の例のように、ゼロでない任意の値を検索することで、検索のスコープを拡張することもできます。  
  
    ```  
    SELECT * FROM authors  
    WHERE contract <> 0  
    ```  
  
## <a name="see-also"></a>参照  
[検索基準の指定 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
