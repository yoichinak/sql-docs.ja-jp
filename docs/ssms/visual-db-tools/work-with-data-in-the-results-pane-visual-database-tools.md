---
description: 結果ペインのデータの操作 (Visual Database Tools)
title: 結果ペインのデータの操作
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- queries [Visual Database Tools]
- result sets [SQL Server], queries
- Query Designer [SQL Server], Results pane
- results [SQL Server], query
- Visual Database Tools [SQL Server], queries
- queries [SQL Server], results
- Results pane
ms.assetid: 4f8a0080-91ef-4442-83ae-53be2f478c54
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 19730090a82eba0c1511e05145803ac42549ebac
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417708"
---
# <a name="work-with-data-in-the-results-pane-visual-database-tools"></a>結果ペインのデータの操作 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
クエリまたはビューを実行すると、その結果が結果ペインに表示されます。 この結果に対して操作を行うことができます。 たとえば、行の追加や削除、データの入力や変更ができるだけでなく、多数の結果セット間を簡単に移動できます。  
  
次に、問題を回避し、結果セットに対して効果的に操作を行うために役立つ情報を示します。  
  
## <a name="returning-the-results-set"></a>結果セットを返す  
結果はクエリまたはビューのいずれかから返すことができます。また、結果ペインだけを開くか、すべてのペインを開くかを選択できます。 どちらの場合も、クエリまたはビューは、クエリおよびビュー デザイナーで開きます。 異なるのは、前者の場合は結果ペインだけが表示された状態で開き、後者の場合は [オプション] ダイアログ ボックスで選択されたすべてのウィンドウと共に開くという点です。 既定では 4 つのペイン (結果、SQL、ダイアグラム、および抽出条件) がすべて開きます。  
  
詳細については、「[クエリを開く (Visual Database Tools)](../../ssms/visual-db-tools/open-queries-visual-database-tools.md)」を参照してください。  
  
クエリまたはビューのデザインを変更して、別の結果セットを返すか、別の順序でレコードを返すようにするには、「[クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)」に記載されたトピックを参照してください。  
  
また、すべての結果セットを返すか、その一部を返すかを、次の 2 つの方法で決定できます。実行中にクエリを中止するか、返す結果の数をクエリ実行前に指定します。  
  
## <a name="navigating-in-the-results-pane"></a>結果ペイン内を移動する  
結果ペインの下端にあるナビゲーション バーを使用すると、レコード間をすばやく移動できます。  
  
最初のレコードと最後のレコードに移動するボタンや、次のレコードと前のレコードに移動するボタン、特定のレコードに移動するボタンがあります。  
  
特定のレコードに移動するには、ナビゲーション バー内のテキスト ボックスに行番号を入力し、Enter キーを押します。  
  
クエリおよびビュー デザイナーでキーボード ショートカットを使用する方法については、「[クエリおよびビュー デザイナーでの操作 (Visual Database Tools)](../../ssms/visual-db-tools/navigate-in-the-query-and-view-designer-visual-database-tools.md)」を参照してください。  
  
## <a name="committing-changes-to-the-database"></a>データベースに変更内容をコミットする  
結果ペインは、オプティミスティック コンカレンシーを使用しているため、グリッドには、完全にライブのビューではなく、データベース内のデータのコピーが表示されます。 この方法では、行から移動したときに初めて変更内容がデータベースにコミットされます。 これにより、複数のユーザーがデータベースに対して同時に操作を行うことが可能になります。 競合が発生した場合 (たとえば他のユーザーが同じ行を変更して先にデータベースにコミットした場合) は、競合が発生したことを通知すると共に解決策を提供するメッセージが表示されます。  
  
## <a name="undo-changes-using-esc"></a>Esc キーを使用して変更を元に戻す  
変更は、データベースにコミットされる前であれば、元に戻すことができます。 レコードから移動していない場合、またはレコードから移動していても、変更がコミットされないことを示すエラー メッセージが表示された場合は、そのデータはコミットされていません。 変更がコミットされていない場合は、Esc キーを使用して変更を元に戻すことができます。  
  
行内のすべての変更を元に戻すには、その行の編集していないセルに移動して Esc キーを押します。  
  
編集した特定のセルに対する変更を元に戻すには、そのセルに移動して Esc キーを押します。  
  
## <a name="adding-or-deleting-data-in-the-database"></a>データベースのデータを追加または削除する  
データベース デザインの動作を確認するために、データベースにサンプル データを追加する必要性が生じる場合があります。 その場合は、結果ペインに直接データを入力するか、メモ帳や Excel など他のプログラムからデータをコピーして結果ペインに貼り付けます。  
  
結果ペインに行をコピーできるだけでなく、新たなレコードの追加や、既存のレコードの変更または削除もできます。 詳細については、「[結果ペインに新しい行を追加する (Visual Database Tools)](../../ssms/visual-db-tools/add-new-rows-in-the-results-pane-visual-database-tools.md)」、「[結果ペイン内の行の削除 (Visual Database Tools)](../../ssms/visual-db-tools/delete-rows-in-the-results-pane-visual-database-tools.md)」、「[結果ペイン内の行の編集 (Visual Database Tools)](../../ssms/visual-db-tools/edit-rows-in-the-results-pane-visual-database-tools.md)」を参照してください。  
  
## <a name="tips-for-working-with-null-values-and-empty-cells"></a>NULL 値および空のセルに対する操作のヒント  
空の行をクリックして新たなレコードを追加する場合、すべての列の初期値は *NULL*です。 null 値が許可されている列であれば、そのままにしておくことができます。  
  
null 以外の値を null に置き換える場合は、大文字で NULL と入力します。 結果ペインでは、それが文字列ではなく null 値であることを示すために、"NULL" が斜体で表示されます。  
  
"null" という文字列を入力するには、引用符なしで文字を入力します。 文字のうち少なくとも 1 つが小文字であれば、その値は null 値ではなく文字列として扱われます。  
  
データ型が binary である列の値には、既定で NULL 値が割り当てられます。 この値は、結果ペインで変更できません。  
  
null を使用せずに空白を入力するには、既存のテキストを削除してそのセルから離れます。  
  
## <a name="validating-data"></a>データの妥当性を検査する  
クエリおよびビュー デザイナーでは、特定の種類のデータを列のプロパティと照合して検証できます。 たとえば、"abc" という値を float 型の列に入力するとエラーが表示され、その変更がデータベースにコミットされません。  
  
結果ペイン内で列のデータ型を確認するには、ダイアグラム ペインを開き、テーブルまたはテーブル値オブジェクト内の列名にマウスのカーソルを合わせるのが最も簡単な方法です。  
  
> [!NOTE]  
> 結果ペインに表示できる text 型データの最大長は 2,147,483,647 です。  
  
## <a name="keeping-the-results-set-synchronized-with-the-query-definition"></a>結果セットとクエリ定義を同期化する  
クエリまたはビューの結果を操作していると、結果ペイン内のレコードがクエリ定義の同期化対象から外れてしまう場合があります。 たとえば、テーブル内の 5 列のうち 4 列についてクエリを実行し、ダイアグラム ペインを使用して 5 番目の列をクエリの定義に追加した場合、その 5 番目の列のデータは、結果ペインに自動的に追加されません。 結果ペインに新たなクエリ定義を反映するには、再度クエリを実行します。  
  
この現象が発生すると、ユーザーにわかるように、結果ペインの右下隅に警告アイコンと "クエリが変更されました。" というテキストが表示され、ペインの左上隅にも警告アイコンが表示されます。  
  
## <a name="reconciling-changes-made-by-multiple-users"></a>複数のユーザーによる変更を調整する  
クエリまたはビューの結果を操作していると、同じデータベースに対して操作を行っている別のユーザーがレコードを変更する場合があります。  
  
この現象が発生すると、セルから離れて競合が起きた直後に、通知が表示されます。 その際、他のユーザーの変更をオーバーライドするか、結果ペインを他のユーザーの変更に合わせて更新するか、発生した差異を調整せずに結果ペインの編集を続けるかを選択できます。 差異を調整しない場合は、変更がデータベースにコミットされません。  
  
## <a name="limitations-in-the-results-pane"></a>結果ペインの制限  
  
### <a name="what-can-not-be-updated"></a>更新できないもの  
結果ペインのデータを正しく操作するために役立つヒントを以下に示します。  
  
-   複数のテーブルまたはビューの列を含むクエリは更新できません。  
  
-   ビューは、データベースの制約で許可されている場合に限り更新できます。  
  
-   ストアド プロシージャから返された結果は更新できません。  
  
-   GROUP BY 句、DISTINCT 句、または TO XML 句を使用したクエリまたはビューは更新できません。  
  
-   テーブル値関数から返された結果は、一部の場合に限り更新できます。  
  
-   クエリ内の式によって作成された列内のデータは更新できません。  
  
-   プロバイダーが正しく変換できなかったデータは更新できません。  
  
### <a name="what-can-not-be-represented-fully"></a>完全に表現できないもの  
データベースから結果ペインに返される内容は、使用しているデータ ソースのプロバイダーに大きく影響されます。 結果ペインでは、必ずしもすべてのデータベース管理システムからのデータを解釈できるわけではありません。 結果ペインでデータを解釈できないケースを以下に示します。  
  
-   結果ペインで作業する場合、binary データ型は不便な場合が多く、ダウンロードに長時間かかる場合があります。 このため、binary データ型は *<Binary data>* または *Null*と表示されます。  
  
-   有効桁数と小数点以下桁数が保持されない場合があります。 たとえば、結果ペインに表示できる有効桁数は 27 桁です。 これを超える有効桁数を持つデータ型のデータは、27 桁に切り捨てられるか、 *<Unable to read data>* と表示されます。  
  
## <a name="see-also"></a>参照  
[クエリに関する基本操作の実行 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[検索基準の指定 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
