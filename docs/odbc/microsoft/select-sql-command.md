---
description: SELECT - SQL コマンド
title: SELECT-SQL コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- select [ODBC]
ms.assetid: 2149c3ca-3a71-446d-8d53-3d056e2f301a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2b5fb0e3d38a2e5594cacf77b116844bcce219d7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466424"
---
# <a name="select---sql-command"></a>SELECT - SQL コマンド
1つ以上のテーブルからデータを取得します。  
  
 Visual FoxPro ODBC ドライバーでは、このコマンドのネイティブな Visual FoxPro 言語構文がサポートされています。 ドライバー固有の情報については、「 **ドライバーの解説**」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
SELECT [ALL | DISTINCT]  
   [Alias.] Select_Item [AS Column_Name]  
   [, [Alias.] Select_Item [AS Column_Name] ...]   
FROM [DatabaseName!]Table [Local_Alias]  
   [, [DatabaseName!]Table [Local_Alias] ...]   
[WHERE JoinCondition [AND JoinCondition  
...]  
   [AND | OR FilterCondition [AND | OR FilterCondition ...]]]  
[GROUP BY GroupColumn [, GroupColumn ...]]  
[HAVING FilterCondition]  
[UNION [ALL] SELECTCommand]  
[ORDER BY Order_Item [ASC | DESC] [, Order_Item [ASC | DESC] ...]]  
```  
  
## <a name="arguments"></a>引数  
  
> [!NOTE]  
>  次の引数で参照される *サブクエリ*は select 内の select であり、かっこで囲む必要があります。 WHERE 句では、(入れ子になっていない) 同じレベルで、最大で2つのサブクエリを使用できます。 (引数のセクションを参照してください)。サブクエリには、複数の結合条件を含めることができます。  
  
 [すべての &#124; 個別]  [*別名*] *Select_Item* [ *Column_Name*] [, [*別名*] *Select_Item* [AS *Column_Name*]...]  
 SELECT 句では、クエリ結果に表示されるフィールド、定数、および式を指定します。  
  
 既定では、[すべて] にクエリ結果のすべての行が表示されます。  
  
 DISTINCT は、クエリ結果の行の重複を除外します。  
  
> [!NOTE]  
>  DISTINCT は、SELECT 句ごとに1回だけ使用できます。  
  
 *エイリアス*。 一致する項目名を修飾します。 *Select_Item*で指定する各アイテムによって、クエリ結果の1つの列が生成されます。 複数の項目に同じ名前が指定されている場合は、列が重複しないように、テーブルの別名と項目名の前にピリオドを含めます。  
  
 *Select_Item* 、クエリ結果に含める項目を指定します。 項目には、次のいずれかを指定できます。  
  
-   FROM 句内のテーブルのフィールドの名前。  
  
-   クエリ結果のすべての行に同じ定数値が表示されることを指定する定数。  
  
-   ユーザー定義関数の名前を指定できる式。  
  
 **SELECT を使用したユーザー定義関数**  
  
 SELECT 句でユーザー定義関数を使用すると、明らかに利点がありますが、次の制限も考慮する必要があります。  
  
-   SELECT で実行される操作の速度は、そのようなユーザー定義関数が実行される速度によって制限される場合があります。 ユーザー定義関数に関連する大量の操作は、C またはアセンブリ言語で記述された API およびユーザー定義関数を使用することによって、より適切に行うことができます。  
  
-   SELECT から呼び出されたユーザー定義関数に値を渡す唯一の信頼性のある方法は、呼び出されたときに関数に渡される引数リストです。  
  
-   特定のバージョンの FoxPro で正しく動作する禁止された操作を試して発見したとしても、それが今後のバージョンでも動作する保証はありません。  
  
 これらの制限とは別に、SELECT 句ではユーザー定義関数を使用できます。 ただし、SELECT を使用するとパフォーマンスが低下する可能性があることに注意してください。  
  
 フィールドまたはフィールドを含む式では、次のフィールド関数を使用できます。  
  
-   AVG (*Select_Item*)-数値データの列の平均値。  
  
-   COUNT (*Select_Item*)-列内の選択項目の数をカウントします。 COUNT (*) は、クエリ出力の行数をカウントします。  
  
-   MIN (*Select_Item*)-列の *Select_Item* の最小値を決定します。  
  
-   MAX (*Select_Item*)-列内の *Select_Item* の最大値を決定します。  
  
-   SUM (*Select_Item*)-数値データの列の合計。  
  
 フィールド関数を入れ子にすることはできません。  
  
 AS *Column_Name*  
 クエリ出力の列の見出しを指定します。 これは、 *Select_Item* が式であるか、フィールド関数を含み、列にわかりやすい名前を付けたい場合に便利です。 *Column_Name* は式にすることができますが、テーブルフィールド名で許可されていない文字 (たとえば、スペース) は使用できません。  
  
 [*DatabaseName*!] から*テーブル* [*Local_Alias*] [, [*DatabaseName*!]*テーブル* [*Local_Alias*]...]  
 クエリによって取得されるデータを含むテーブルが一覧表示されます。 テーブルが開かれていない場合、ファイルの場所を指定できるように、[ **開く** ] ダイアログボックスが表示されます。 テーブルを開いた後は、クエリが完了した後もテーブルは開いたままになります。  
  
 *DatabaseName*! データソースで指定されたデータベース以外のデータベースの名前を指定します。 データベースがデータソースで指定されていない場合は、テーブルを含むデータベースの名前を含める必要があります。 データベース名の後とテーブル名の前に、感嘆符 (!) の区切り記号を含めます。  
  
 *Local_Alias* は、 *テーブル*にという名前のテーブルの一時的な名前を指定します。 ローカルエイリアスを指定する場合は、SELECT ステートメント全体でテーブル名の代わりにローカルエイリアスを使用する必要があります。 ローカルエイリアスは、Visual FoxPro 環境には影響しません。  
  
 *Joincondition* [および*joincondition* ...]   [および &#124; または*filtercondition* [および &#124; または*filtercondition* ...]]  
 クエリ結果に特定のレコードのみを含めるように Visual FoxPro に指示します。 複数のテーブルからデータを取得するには、が必要です。  
  
 *Joincondition* は、from 句内のテーブルをリンクするフィールドを指定します。 クエリに複数のテーブルを含める場合は、最初のテーブルの後に、すべてのテーブルに対して結合条件を指定する必要があります。  
  
> [!IMPORTANT]  
>  結合条件を作成するときは、次の情報を考慮してください。  
  
-   クエリに2つのテーブルを含め、結合条件を指定しない場合、フィルター条件が満たされていれば、最初のテーブルのすべてのレコードが2番目のテーブル内のすべてのレコードに結合されます。 このようなクエリを実行すると、長い結果が生成される可能性があります。  
  
-   空のフィールドを含むテーブルを結合する場合は、Visual FoxPro が空のフィールドと一致するため、注意してください。 たとえば、CUSTOMER.ZIP に参加していて INVOICE.ZIP、顧客に100の空の郵便番号が含まれていて、請求書に空の郵便番号が400含まれている場合、クエリ出力には空のフィールドからの4万余分なレコードが含まれます。 空のレコードをクエリ出力から削除するには、 **empty ()** 関数を使用します。  
  
-   複数の結合条件を接続するには、AND 演算子を使用する必要があります。 各結合条件には、次の形式があります。  
  
     *FieldName1 比較 FieldName2*  
  
     *FieldName1* は、1つのテーブルのフィールドの名前、 *FieldName2* は別のテーブルのフィールドの名前、 *比較* は次の表で説明する演算子の1つです。  
  
|演算子|比較|  
|--------------|----------------|  
|=|Equal|  
|==|厳密に等しい|  
|LIKE|SQL のような|  
|<>、! =、#|等しくない|  
|>|より大きい|  
|>=|以下|  
|<|より小さい|  
|<=|以下|  
  
 文字列で = 演算子を使用すると、SET ANSI の設定によって異なる動作になります。 [SET ANSI] がオフに設定されている場合、Visual FoxPro では、Xbase ユーザーになじみのある方法で文字列比較を処理します。 SET ANSI が ON に設定されている場合、Visual FoxPro は、文字列比較のために ANSI 標準に従います。 Visual FoxPro が文字列比較を実行する方法の詳細については、「 [SET ANSI](../../odbc/microsoft/set-ansi-command.md) 」と「 [EXACT set](../../odbc/microsoft/set-exact-command.md) 」を参照してください。  
  
 *Filtercondition* は、クエリ結果に含めるためにレコードが満たす必要のある条件を指定します。 必要な数のフィルター条件をクエリに含め、AND または OR 演算子を使用して接続できます。 また、NOT 演算子を使用して論理式の値を反転させることも、 **empty ()** を使用して空のフィールドをチェックすることもできます。 *Filtercondition* は、次の例のいずれかの形式を取ることができます。  
  
 **例 1** *FieldName1 比較 FieldName2*  
  
 `customer.cust_id = orders.cust_id`  
  
 **例 2** *フィールド名の比較式*  
  
 `payments.amount >= 1000`  
  
 **例 3** *フィールド名の比較* (*サブクエリ*)  
  
 `company < ALL ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 フィルター条件に ALL が含まれている場合、そのレコードがクエリ結果に含まれる前に、そのサブクエリによって生成されるすべての値の比較条件を満たす必要があります。  
  
 **例 4** *フィールド名の比較* &#124; SOME (*サブクエリ*)  
  
 `company < ANY ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 フィルター条件にまたはのいずれかが含まれている場合、フィールドは、サブクエリによって生成された値の少なくとも1つの比較条件を満たしている必要があります。  
  
 次の例では、フィールドの値が指定された値の範囲内にあるかどうかを確認します。  
  
 *Start_Range*と*END_RANGE*の間の**例 5** *フィールド名*[NOT]  
  
 `customer.postalcode BETWEEN 90000 AND 99999`  
  
 次の例では、少なくとも1つの行がサブクエリ内の条件を満たしているかどうかを確認します。 フィルター条件にが存在する場合、フィルター条件は True (と評価されます。T.) は、サブクエリが空のセットに評価される場合を除きます。  
  
 **例 6** [NOT] Exists (*サブクエリ*)  
  
 `EXISTS ;`  
  
 `(SELECT * FROM orders WHERE customer.postalcode =`  
  
 `orders.postalcode)`  
  
 **例 7** *FieldName* [NOT] in *Value_Set*  
  
 `customer.postalcode NOT IN ("98052","98072","98034")`  
  
 フィルター条件にが含まれる場合、そのレコードがクエリ結果に含まれる前に、フィールドに値のいずれかが含まれている必要があります。  
  
 **例 8** *FieldName* [NOT] IN (*サブクエリ*)  
  
 `customer.cust_id IN ;`  
  
 `(SELECT orders.cust_id FROM orders WHERE orders.city="Seattle")`  
  
 ここでは、クエリの結果にレコードが含まれる前に、サブクエリによって返される値の1つがフィールドに含まれている必要があります。  
  
 **例 9** *FieldName* [NOT] は*cexpression*に似ています。  
  
 `customer.country NOT LIKE "USA"`  
  
 このフィルター条件では、 *Cexpression*に一致する各フィールドが検索されます。 パーセント記号 (%) を使用できます。とアンダースコア (_) のワイルドカード文字を *Cexpression*の一部として指定します。 アンダースコアは、文字列内の1つの不明な文字を表します。  
  
 *Groupcolumn* [, *groupcolumn* ...] でグループ化  
 1つまたは複数の列の値に基づいて、クエリ内の行をグループ化します。 *Groupcolumn* には、次のいずれかを指定できます。  
  
-   通常のテーブルフィールドの名前。  
  
-   SQL フィールド関数を含むフィールドです。  
  
-   結果テーブル内の列の位置を示す数値式です。 (左端の列番号は1です)。  
  
 *Filtercondition*を持つ  
 グループがクエリ結果に含めるために満たす必要のあるフィルター条件を指定します。 HAVING は GROUP BY と共に使用する必要があり、必要な数のフィルター条件を AND または OR 演算子で連結できます。 論理式の値を逆にするために NOT を使用することもできます。  
  
 *Filtercondition* にサブクエリを含めることはできません。  
  
 GROUP BY 句のない HAVING 句は、WHERE 句と同様に動作します。 HAVING 句では、ローカルエイリアスとフィールド関数を使用できます。 HAVING 句にフィールド関数が含まれていない場合は、パフォーマンスを向上させるために WHERE 句を使用します。  
  
 [UNION [すべて] *SELECTCommand*]  
 1つの SELECT の最終結果を、別の SELECT の最終結果と結合します。 既定では、UNION は結合された結果をチェックし、重複する行を削除します。 複数の UNION 句を結合するには、かっこを使用します。  
  
 ALL は、UNION によって結合された結果から重複する行を削除しないようにします。  
  
 UNION 句は次の規則に従います。  
  
-   UNION を使用してサブクエリを結合することはできません。  
  
-   どちらの SELECT コマンドも、クエリ出力の列数が同じである必要があります。  
  
-   1つの SELECT のクエリ結果内の各列は、もう一方の SELECT の対応する列と同じデータ型と幅を持つ必要があります。  
  
-   最後の SELECT だけが ORDER BY 句を持つことができます。これは、出力列を数値で参照する必要があります。 ORDER BY 句が含まれている場合は、完全な結果に影響します。  
  
 UNION 句を使用して外部結合をシミュレートすることもできます。  
  
 クエリで2つのテーブルを結合すると、結合フィールドに一致する値を持つレコードだけが出力に含まれます。 親テーブルのレコードの子テーブルに対応するレコードがない場合、親テーブル内のレコードは出力に含まれません。 外部結合を使用すると、親テーブル内のすべてのレコードを、子テーブル内の一致するレコードと共に、出力に含めることができます。 Visual FoxPro で外部結合を作成するには、次の例のように、入れ子になった SELECT コマンドを使用する必要があります。  
  
```  
SELECT customer.company, orders.order_id, orders.emp_id ;  
FROM customer, orders ;  
WHERE customer.cust_id = orders.cust_id ;  
UNION ;  
SELECT customer.company, 0, 0 ;  
FROM customer ;  
WHERE customer.cust_id NOT IN ;  
(SELECT orders.cust_id FROM orders)  
```  
  
> [!NOTE]  
>  各セミコロンの直前にあるスペースが含まれていることを確認してください。 それ以外の場合は、エラーが表示されます。  
  
 UNION 句の前のコマンドのセクションは、一致する値を持つ両方のテーブルからレコードを選択します。 請求書が関連付けられていない顧客企業は含まれません。 UNION 句の後のコマンドのセクションは、orders テーブルに一致するレコードがない customer テーブル内のレコードを選択します。  
  
 コマンドの2番目のセクションについては、次の点に注意してください。  
  
-   かっこ内の SELECT ステートメントは、最初に処理されます。 このステートメントでは、orders テーブル内のすべての顧客番号を選択します。  
  
-   WHERE 句は、orders テーブルにない customer テーブル内のすべての顧客番号を検索します。 コマンドの最初のセクションでは、orders テーブルに顧客番号を持つすべての会社が提供されているので、customer テーブル内のすべての会社がクエリ結果に含まれるようになりました。  
  
-   UNION に含まれるテーブルの構造は同一である必要があるため、2つ目の SELECT ステートメントには2つのプレースホルダーがあります。1つ目の SELECT ステートメントから、 *order_id* と *orders. emp_id* を表します。  
  
    > [!NOTE]  
    >  プレースホルダーは、それらが表すフィールドと同じ型である必要があります。 フィールドが日付型の場合、プレースホルダーは {///} である必要があります。 フィールドが文字フィールドの場合、プレースホルダーは空の文字列 ("") にする必要があります。  
  
 ORDER BY *Order_Item* [ASC &#124; desc] [, *Order_Item* [asc &#124; DESC]...]  
 1つまたは複数の列のデータに基づいてクエリの結果を並べ替えます。 各 *Order_Item* は、クエリ結果の列に対応している必要があり、次のいずれかになります。  
  
-   サブクエリではなく、メイン SELECT 句の選択項目でもある、FROM テーブル内のフィールド。  
  
-   結果テーブル内の列の位置を示す数値式です。 (一番左の列は number 1 です)。  
  
 ASC は、order 項目に従ってクエリの結果の昇順を指定し、ORDER BY の既定値です。  
  
 DESC は、クエリ結果の降順を指定します。  
  
 ORDER BY で order を指定しない場合、クエリ結果は順序なしとして表示されます。  
  
## <a name="remarks"></a>解説  
 SELECT は、他の Visual FoxPro コマンドと同様に、Visual FoxPro に組み込まれている SQL コマンドです。 SELECT を使用してクエリを実行すると、Visual FoxPro はクエリを解釈し、テーブルから指定されたデータを取得します。 SELECT クエリは、コマンドプロンプトウィンドウまたは Visual FoxPro プログラム (他の Visual FoxPro コマンドと同様) のいずれかで作成できます。  
  
> [!NOTE]  
>  [フィルターの設定] で指定された現在のフィルター条件を考慮しません。  
  
## <a name="driver-remarks"></a>ドライバーの解説  
 アプリケーションが ODBC SQL ステートメントをデータソースに送信するとき、Visual FoxPro ODBC ドライバーは、コマンドに ODBC エスケープシーケンスが含まれていない限り、コマンドを変換せずに Visual FoxPro SELECT コマンドに変換します。 ODBC エスケープシーケンスで囲まれた項目は、Visual FoxPro 構文に変換されます。 ODBC エスケープシーケンスの使用方法の詳細については、『 *MICROSOFT Odbc プログラマーズリファレンス*』の「 [Time 関数と Date 関数](../../odbc/microsoft/time-and-date-functions-visual-foxpro-odbc-driver.md)」および「 [odbc でのエスケープシーケンス](../../odbc/reference/develop-app/escape-sequences-in-odbc.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [CREATE TABLE-SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT-SQL](../../odbc/microsoft/insert-sql-command.md)   
 [ANSI の設定](../../odbc/microsoft/set-ansi-command.md)   
 [正確に設定](../../odbc/microsoft/set-exact-command.md)
