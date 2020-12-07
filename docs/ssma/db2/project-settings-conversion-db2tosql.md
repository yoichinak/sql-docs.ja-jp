---
description: プロジェクトの設定 (変換) (DB2ToSQL)
title: プロジェクトの設定 (変換) (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 538c93cf-c5bb-43d5-b758-186d9fb00c19
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 165287fd2d699c56dc635d85fd58a1b081a497a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427034"
---
# <a name="project-settings-conversion-db2tosql"></a>プロジェクトの設定 (変換) (DB2ToSQL)
[ **プロジェクトの設定** ] ダイアログボックスの [変換] ページには、SSMA が DB2 構文を構文に変換する方法をカスタマイズする設定が含まれてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
[変換] ペインは、[ **プロジェクトの設定** ] ダイアログボックスと [ **既定のプロジェクトの設定** ] ダイアログボックスで使用できます。  
  
-   すべての SSMA プロジェクトの設定を指定するには、[ **ツール** ] メニューの [ **既定のプロジェクト設定**] をクリックし、[移行の **対象バージョン** ] ドロップダウンから設定を表示または変更する必要がある [移行プロジェクトの種類] を選択し、左側のウィンドウの下部にある [ **全般** ] をクリックし、[ **変換**] をクリックします。  
  
-   現在のプロジェクトの設定を指定するには、[ **ツール** ] メニューの [ **プロジェクトの設定**] をクリックし、左側のウィンドウの下部にある [ **全般** ] をクリックして、[ **変換**] をクリックします。  
  
## <a name="conversion-messages"></a>変換メッセージ  
  
### <a name="generate-messages-about-issues-applied"></a>適用された問題に関するメッセージを生成する  
SSMA が変換中に情報メッセージを生成し、出力ペインに表示し、変換されたコードに追加するかどうかを指定します。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティックモード:** 違います  
  
**フルモード:** 違います  
  
## <a name="miscellaneous-options"></a>その他のオプション  
  
### <a name="cast-rownum-expressions-as-integers"></a>ROWNUM 式を整数としてキャストする  
SSMA が ROWNUM 式を変換すると、式が TOP 句に変換され、その後に式が変換されます。 次の例は、DB2 の DELETE ステートメントでの ROWNUM を示しています。  
  
`DELETE FROM Table1`  
  
`WHERE ROWNUM < expression and Field1 >= 2`  
  
次の例は、結果のを示してい [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。  
  
`DELETE TOP (expression-1)`  
  
`FROM Table1`  
  
`WHERE Field1>=2`  
  
TOP では、TOP 句の式が整数に評価される必要があります。 整数が負の値の場合、ステートメントによってエラーが生成されます。  
  
-   [ **はい**] を選択すると、ssma は式を整数としてキャストします。  
  
-   [ **いいえ**] を選択すると、ssma は、変換されたコード内のすべての整数以外の式をエラーとしてマークします。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/フルモード:** 違います  
  
**オプティミスティックモード:** うん  
  
### <a name="default-schema-mapping"></a>既定のスキーママッピング  
この設定では、DB2 スキーマを SQL Server スキーマにマップする方法を指定します。 この設定では、次の2つのオプションを使用できます。  
  
1.  **データベースへのスキーマ:** このモードでは、DB2 スキーマ ' sch1 ' は、既定で SQL Server データベース ' sch1 ' の ' dbo ' SQL Server スキーマにマップされます。  
  
2.  スキーマ**からスキーマへ:** このモードでは、DB2 スキーマ ' sch1 ' は、既定では、接続ダイアログで指定された既定の SQL Server データベースの ' sch1 ' SQL Server スキーマにマップされます。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティック/フルモード:** データベースへのスキーマ  
  
### <a name="conversion-ways-of-merge-statement"></a>MERGE ステートメントの変換方法  
  
-   **Insert、update、delete ステートメントを使用して**を選択した場合、ssma は、マージステートメントを INSERT、UPDATE、delete ステートメントに変換します。  
  
-   [ **Merge ステートメントを使用**する] を選択した場合、ssma は、のマージステートメントを merge ステートメントに変換 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。  
  
> [!WARNING]  
> このプロジェクト設定オプションは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008、2012、2014でのみ使用でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティック/フルモード:** MERGE ステートメントの使用  
  
### <a name="convert-calls-to-subprograms-that-use-default-arguments"></a>既定の引数を使用するサブプログラムへの呼び出しを変換する  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 関数は、関数呼び出しのパラメーターの省略をサポートしていません。 また、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 関数とプロシージャは、式を既定のパラメーター値としてサポートしていません。  
  
-   [ **はい]** を選択し、関数呼び出しでパラメーターが省略されている場合、ssma はキーワード **default** を関数に挿入し、正しい位置でを呼び出します。 次に、警告を使用して呼び出しをマークします。  
  
-   [ **いいえ**] を選択すると、ssma は関数呼び出しをエラーとしてマークします。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティック/フルモード:** うん  
  
### <a name="convert-count-function-to-count_big"></a>COUNT 関数を COUNT_BIG に変換します  
カウント関数が2147483647より大きい値 (2<sup>31</sup>-1) を返す可能性がある場合は、関数を COUNT_BIG に変換する必要があります。  
  
-   [ **はい**] を選択すると、ssma はすべての使用量を COUNT_BIG に変換します。  
  
-   [ **いいえ**] を選択した場合、関数はカウントとして残ります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 関数が 2<sup>31</sup>-1 より大きい値を返すと、はエラーを返します。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/フルモード:** うん  
  
**オプティミスティックモード:** 違います  
  
### <a name="convert-forall-statement-to-while-statement"></a>FORALL ステートメントを WHILE ステートメントに変換します  
SSMA が PL/SQL collection 要素の FORALL ループを処理する方法を定義します。  
  
-   [ **はい**] を選択すると、ssma によって、コレクション要素が1つずつ取得される while ループが作成されます。  
  
-   [ **いいえ**] を選択すると、ssma は nodes () メソッドを使用してコレクションから行セットを生成し、それを1つのテーブルとして使用します。 これはより効率的ですが、出力コードが読みにくくなります。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティックモード:** 違います  
  
**フルモード:** うん  
  
### <a name="convert-foreign-keys-with-set-null-referential-action-on-column-that-is-not-null"></a>NULL 以外の列に対する SET NULL 参照操作による外部キーの変換  
DB2 では foreign key 制約を作成できます。参照先の列では null 値が許可されていないため、SET NULL 操作を実行できない可能性があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、このような外部キーの構成は許可されません。  
  
-   [ **はい**] を選択した場合、ssma は DB2 のように参照アクションを生成しますが、制約をに読み込む前に手動で変更を加える必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 たとえば、[NULL の設定] ではなく [アクションなし] を選択できます。  
  
-   [ **いいえ**] を選択した場合、制約はエラーとしてマークされます。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティック/フルモード:** 違います  
  
### <a name="convert-function-calls-to-procedure-calls"></a>関数呼び出しをプロシージャ呼び出しに変換する  
一部の DB2 関数は、自律トランザクションとして定義されているか、では無効なステートメントを含んでい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 このような場合は、プロシージャのラッパーであるプロシージャと関数が SSMA によって作成されます。 変換された関数は、実装するプロシージャを呼び出します。  
  
SSMA は、ラッパー関数への呼び出しをプロシージャの呼び出しに変換できます。 これにより、読みやすいコードが作成され、パフォーマンスが向上します。 ただし、コンテキストによって常に許可されるわけではありません。たとえば、SELECT リスト内の関数呼び出しをプロシージャ呼び出しに置き換えることはできません。 SSMA には、一般的なケースに対応するためのオプションがいくつかあります。  
  
-   **Always**を選択すると、ssma はラッパー関数呼び出しをプロシージャ呼び出しに変換しようとします。 現在のコンテキストでこの変換が許可されていない場合は、エラーメッセージが生成されます。 このように、生成されたコードに関数呼び出しは残されません。  
  
-   **可能な**場合に選択すると、ssma では、関数に出力パラメーターがある場合にのみ、プロシージャ呼び出しに移動します。 移動できない場合、パラメーターの出力属性は削除されます。 それ以外の場合、SSMA は関数呼び出しを残します。  
  
-   [ **なし**] を選択した場合、ssma は関数呼び出しとしてすべての関数呼び出しをそのままにします。 この選択は、パフォーマンス上の理由から許容できない場合があります。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティック/フルモード:** 可能な場合  
  
### <a name="convert-lock-table-statements"></a>LOCK TABLE ステートメントの変換  
SSMA では、多くのロックテーブルステートメントをテーブルヒントに変換できます。 SSMA では、PARTITION 句、副句、および NOWAIT 句を含むロックテーブルステートメントを変換することはできません @dblink 。また、このようなステートメントには変換エラーメッセージをマークします。  
  
-   [ **はい**] を選択すると、ssma はサポートされているロックテーブルステートメントをテーブルヒントに変換します。  
  
-   [ **いいえ**] を選択した場合、ssma は、すべてのロックテーブルステートメントに変換エラーメッセージをマークします。  
  
次の表は、SSMA が DB2 ロックモードを変換する方法を示しています。  
  
|DB2 ロックモード|SQL Server テーブルヒント|  
|-|-|  
|行共有|ROWLOCK、HOLDLOCK|  
|行排他|ROWLOCK、XLOCK、HOLDLOCK|  
|共有更新 = 行共有|ROWLOCK、HOLDLOCK|  
|共有|TABLOCK、HOLDLOCK|  
|行を排他的に共有|TABLOCK、XLOCK、HOLDLOCK|  
|外税|TABLOCKX、HOLDLOCK|  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティック/フルモード:** うん  
  
### <a name="convert-open-for-statements-for-ref-cursor-out-parameters"></a>REF CURSOR OUT パラメーターのための OPEN ステートメントの変換  
DB2 では、OPEN FOR ステートメントを使用して、REF CURSOR 型の subprogram の OUT パラメーターに結果セットを返すことができます。 では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、ストアドプロシージャは SELECT ステートメントの結果を直接返します。  
  
SSMA では、多数の OPEN ステートメントを SELECT ステートメントに変換できます。  
  
-   [ **はい**] を選択した場合、ssma は、OPEN ステートメントを select ステートメントに変換します。これにより、結果セットがクライアントに返されます。  
  
-   [ **いいえ**] を選択すると、ssma は変換されたコードと出力ウィンドウにエラーメッセージを生成します。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティック/フルモード:** うん  
  
### <a name="convert-record-as-a-list-of-separates-variables"></a>レコードを分離される変数の一覧として変換する  
SSMA では、DB2 レコードを、特定の構造を持つ変数と XML 変数に分けることができます。  
  
-   [ **はい**] を選択した場合、ssma は、可能であれば、変数を分離した一覧にレコードを変換します。  
  
-   [ **いいえ**] を選択した場合、ssma は、特定の構造を持つ XML 変数にレコードを変換します。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティック/フルモード:** うん  
  
### <a name="convert-substr-function-calls-to-substring-function-calls"></a>SUBSTR 関数呼び出しから SUBSTRING 関数呼び出しへの変換  
SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、パラメーターの数に応じて、DB2 SUBSTR 関数呼び出しを **substring** 関数呼び出しに変換できます。 SSMA で SUBSTR 関数呼び出しを変換できない場合、またはパラメーターの数がサポートされていない場合、SSMA は SUBSTR 関数呼び出しをカスタム SSMA 関数呼び出しに変換します。  
  
-   [ **はい**] を選択すると、ssma は、3つのパラメーターを使用する SUBSTR 関数呼び出しを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **部分文字列**に変換します。 その他の SUBSTR 関数は、カスタム SSMA 関数を呼び出すように変換されます。  
  
-   [ **いいえ**] を選択すると、SSMA は SUBSTR 関数呼び出しをカスタム ssma 関数呼び出しに変換します。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティックモード:** うん  
  
**フルモード:** 違います  
  
### <a name="convert-subtypes"></a>サブタイプの変換  
SSMA では、次の2つの方法で PL/SQL のサブタイプを変換できます。  
  
-   [ **はい**] を選択すると、ssma は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サブタイプからユーザー定義型を作成し、このサブタイプの各変数に対して使用します。  
  
-   [ **いいえ**] を選択すると、ssma は、サブタイプのすべてのソース宣言を基になる型に置き換え、結果を通常どおりに変換します。 この場合、追加の型はで作成されません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティック/フルモード:** 違います  
  
### <a name="convert-synonyms"></a>シノニムの変換  
次の DB2 オブジェクトのシノニムは、に移行でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
-   テーブルとオブジェクト テーブル  
  
-   ビューとオブジェクト ビュー  
  
-   ストアドプロシージャと関数  
  
-   具体化されたビュー  
  
次の DB2 オブジェクトのシノニムは、オブジェクトへの直接参照で置き換えることができます。  
  
-   シーケンス  
  
-   パッケージ  
  
-   Java クラス スキーマ オブジェクト  
  
-   ユーザー定義オブジェクト型  
  
その他のシノニムは移行できません。 SSMA は、シノニムとシノニムを使用するすべての参照のエラーメッセージを生成します。  
  
-   [ **はい**] を選択すると、ssma は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 前の一覧に従ってシノニムとダイレクトオブジェクト参照を作成します。  
  
-   [ **いいえ**] を選択した場合、ssma はここに記載されているすべてのシノニムに対して直接オブジェクト参照を作成します。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティック/フルモード:** うん  
  
### <a name="convert-to_chardate-format"></a>変換 TO_CHAR (日付、形式)  
SSMA では、DB2 TO_CHAR (date、format) を sysdb データベースのプロシージャに変換できます。  
  
-   [ **TO_CHAR_DATE 関数を使用**する] を選択した場合、ssma は TO_CHAR (DATE, format) を変換に英語 (*) を使用して TO_CHAR_DATE 関数に変換します。  
  
-   [ **TO_CHAR_DATE_LS 関数 (NLS ケア) を使用**する] を選択した場合、ssma は、変換にセッション言語を使用して、TO_CHAR (DATE、format) を TO_CHAR_DATE_LS 関数に変換します。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティックモード:** TO_CHAR_DATE 関数の使用  
  
**フルモード:** TO_CHAR_DATE_LS 関数の使用 (NLS ケア)  
  
### <a name="convert-transaction-processing-statements"></a>トランザクション処理ステートメントの変換  
SSMA は、DB2 トランザクション処理ステートメントを変換できます。  
  
-   [ **はい**] を選択した場合、SSMA は DB2 トランザクション処理ステートメントをステートメントに変換 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。  
  
-   [ **いいえ**] を選択した場合、ssma はトランザクション処理ステートメントを変換エラーとしてマークします。  
  
> [!NOTE]  
> DB2 はトランザクションを暗黙的に開きます。 でこの動作をエミュレートするに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、トランザクションを開始する BEGIN TRANSACTION ステートメントを手動で追加する必要があります。 または、セッションの開始時に SET IMPLICIT_TRANSACTIONS ON コマンドを実行します。 SSMA では、自律トランザクションでサブルーチンを変換するときに、SET IMPLICIT_TRANSACTIONS が自動的に追加されます。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティック/フルモード:** うん  
  
### <a name="emulate-db2-null-behavior-in-order-by-clauses"></a>DB2 の null 動作を ORDER BY 句でエミュレートする  
と DB2 では、NULL 値は異なる順序で並べ替えられ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
-   で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、NULL 値は順序付きリストの最小値です。 昇順の一覧では、NULL 値が最初に表示されます。  
  
-   DB2 では、NULL 値は順序付きリストの最大値です。 既定では、NULL 値は昇順の一覧の最後に表示されます。  
  
-   DB2 には、最初と NULL の null が含まれています。これにより、DB2 の順序を変更できます。  
  
SSMA では、NULL 値をチェックすることによって DB2 ORDER BY 動作をエミュレートできます。 次に、指定した順序で NULL 値によって並べ替えられた後、他の値で並べ替えられます。  
  
-   [ **はい**] を選択した場合、ssma は DB2 の順序をエミュレートするように db2 ステートメントを変換します。  
  
-   [ **いいえ**] を選択すると、SSMA は DB2 の規則を無視し、NULL の最初と NULL の最後の句が検出されたときにエラーメッセージを生成します。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティックモード:** 違います  
  
**フルモード:** うん  
  
### <a name="emulate-row-count-exceptions-in-select"></a>SELECT での行数の例外のエミュレート  
INTO 句を含む SELECT ステートメントが行を返さない場合、DB2 は NO_DATA_FOUND 例外を発生させます。 ステートメントが2つ以上の行を返す場合は、TOO_MANY_ROWS 例外が発生します。 の変換されたステートメントでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 行数が1と異なる場合、例外は発生しません。  
  
-   [ **はい**] を選択した場合、ssma は各 select ステートメントの後 db_error_exact_one_row_check sysdb プロシージャに呼び出しを追加します。 この手順では、NO_DATA_FOUND と TOO_MANY_ROWS の例外をエミュレートします。 これは既定の設定であり、DB2 の動作をできるだけ近い方法で再現できます。 ソースコードにこれらのエラーを処理する例外ハンドラーがある場合は、常に **[はい]** を選択する必要があります。 SELECT ステートメントがユーザー定義関数内で発生した場合、このモジュールはストアドプロシージャに変換されます。ストアドプロシージャを実行し、例外を発生させることは、関数コンテキストと互換性がないためです [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   [ **いいえ**] を選択すると、例外は生成されません。 これは、SSMA がユーザー定義関数を変換するときに、その関数を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティック/フルモード:** うん  
  
### <a name="generate-error-for-dbms_sqlparse"></a>DBMS_SQL のエラーを生成します。分解  
  
-   [ **エラー**] を選択すると、ssma によって変換 DBMS_SQL にエラーが生成されます。分解.  
  
-   [ **警告**] を選択した場合、ssma は変換 DBMS_SQL に警告を生成します。分解.  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティック/フルモード:** エラー  
  
### <a name="generate-rowid-column"></a>ROWID 列の生成  
SSMA がでテーブルを作成するときに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、ROWID 列を作成できます。 データが移行されると、各行は newid () 関数によって生成された新しい UNIQUEIDENTIFIER 値を取得します。  
  
-   [ **はい**] を選択すると、すべてのテーブルに ROWID 列が作成され、値を挿入するときに guid が生成され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 SSMA Tester の使用を計画している場合は、常に **[はい]** を選択します。  
  
-   [ **いいえ**] を選択した場合、ROWID 列はテーブルに追加されません。  
  
-   **トリガーを含むテーブルの rowid 列を追加** トリガーを含むテーブルの rowid を追加します。  
  
> [!WARNING]  
> SQL Server 2005、SQL Server 2008、SQL Server 2012 および2014の場合の既定の設定では、 **トリガーを含むテーブルに ROWID 列を追加**します。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティックモード:** トリガーを含むテーブルの ROWID 列を追加する  
  
**フルモード:** うん  
  
### <a name="generate-unique-index-on-rowid-column"></a>ROWID 列に一意のインデックスを生成します  
SSMA が ROWID によって生成される列に一意のインデックス列を生成するかどうかを指定します。 オプションが "YES" に設定されている場合は、一意インデックスが生成され、"NO" に設定されている場合は、ROWID 列で一意のインデックスが生成されません。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティック/フルモード:** うん  
  
### <a name="local-modules-conversion"></a>ローカルモジュールの変換  
DB2 の入れ子になった subprogram の種類 (スタンドアロンストアドプロシージャまたは関数で宣言) を定義します。  
  
-   [ **インライン**] を選択した場合、入れ子になった subprogram の呼び出しはその本文で置き換えられます。  
  
-   **ストアドプロシージャ**を選択した場合、入れ子になった subprogram は SQL Server ストアドプロシージャに変換され、その呼び出しはこのプロシージャ呼び出しで置き換えられます。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティック/フルモード:** インライン  
  
### <a name="use-isnull-in-string-concatenation"></a>文字列の連結で ISNULL を使用する  
文字列の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連結に NULL 値が含まれている場合、DB2 とは異なる結果を返します。 DB2 では、空の文字セットと同様に NULL 値が処理されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NULL を返します。  
  
-   [ **はい**] を選択すると、SSMA は DB2 連結文字 (| |) を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連結文字 (+) に置き換えます。 SSMA では、連結の両側の式も NULL 値に対してチェックされます。  
  
-   [ **いいえ**] を選択した場合、ssma は連結文字を置き換えますが、NULL 値はチェックされません。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
### <a name="use-isnull-in-replace-function-calls"></a>関数呼び出しの置換で ISNULL を使用する  
ISNULL ステートメントは、DB2 の動作をエミュレートするために、REPLACE 関数呼び出しで使用されます。 この設定には、次のオプションがあります。  
  
-   YES  
  
-   NO  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティックモード:** 違います  
  
**フルモード:** うん  
  
### <a name="use-isnull-in-concat-function-calls"></a>CONCAT 関数呼び出しで ISNULL を使用する  
ISNULL ステートメントは、DB2 の動作をエミュレートするために、CONCAT 関数呼び出しで使用されます。 この設定には、次のオプションがあります。  
  
-   YES  
  
-   NO  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティックモード:** 違います  
  
**フルモード:** うん  
  
### <a name="use-native-convert-function-when-possible"></a>可能な場合はネイティブの convert 関数を使用する  
  
-   [ **はい**] を選択した場合、ssma は、可能な場合は TO_CHAR (date, format) をネイティブの convert 関数に変換します。  
  
-   [ **いいえ**] を選択した場合、ssma は TO_CHAR (日付、形式) を TO_CHAR_DATE または TO_CHAR_DATE_LS に変換します ("Convert TO_CHAR (date, format)" オプションで定義されています)。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティックモード:** うん  
  
**フルモード:** 違います  
  
### <a name="use-selectfor-xml-when-converting-selectinto-for-record-variable"></a>SELECT...SELECT... を変換するときに FOR XMLレコード変数の場合  
レコード変数を選択したときに XML 結果セットを生成するかどうかを指定します。  
  
-   [ **はい**] を選択すると、select ステートメントによって XML が返されます。  
  
-   [ **いいえ**] を選択すると、select ステートメントによって結果セットが返されます。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティック/フルモード:** 違います  
  
## <a name="returning-clause-conversion"></a>返す句の変換  
  
### <a name="convert-returning-clause-in-delete-statement-to-output"></a>DELETE ステートメントの戻り句を OUTPUT に変換します  
DB2 は、削除された値をすぐに取得する手段として、返される句を提供します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OUTPUT 句を使用してこの機能を提供します。  
  
-   [ **はい**] を選択すると、SSMA は DELETE ステートメント内の句を返すを OUTPUT 句に変換します。 テーブルのトリガーによって値が変更される可能性があるため、戻り値は DB2 とは異なる場合があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
-   [ **いいえ**] を選択すると、ssma は、返された値を取得するために DELETE ステートメントの前に select ステートメントを生成します。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティック/フルモード:** うん  
  
### <a name="convert-returning-clause-in-insert-statement-to-output"></a>INSERT ステートメントの戻り句を OUTPUT に変換します  
DB2 は、挿入された値をすぐに取得する手段として、返される句を提供します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OUTPUT 句を使用してこの機能を提供します。  
  
-   [ **はい**] を選択すると、SSMA は INSERT ステートメント内の返す句を出力に変換します。 テーブルのトリガーによって値が変更される可能性があるため、戻り値は DB2 とは異なる場合があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
-   [ **いいえ**] を選択した場合、ssma は、参照テーブルから値を挿入して選択することによって DB2 の機能をエミュレートします。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティック/フルモード:** うん  
  
### <a name="convert-returning-clause-in-update-statement-to-output"></a>UPDATE ステートメント内の句を OUTPUT に変換します  
DB2 では、更新された値をすぐに取得する手段として、戻り値の句が提供されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OUTPUT 句を使用してこの機能を提供します。  
  
-   [ **はい**] を選択すると、SSMA は UPDATE ステートメント内の句を返すを OUTPUT 句に変換します。 テーブルのトリガーによって値が変更される可能性があるため、戻り値は DB2 とは異なる場合があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
-   [ **いいえ**] を選択すると、SSMA は UPDATE ステートメントの後に select ステートメントを生成し、戻り値を取得します。  
  
[ **モード** ] ボックスで変換モードを選択すると、ssma によって次の設定が適用されます。  
  
**既定/オプティミスティック/フルモード:** うん  
  
## <a name="sequence-conversion"></a>シーケンス変換  
  
### <a name="convert-sequence-generator"></a>シーケンスジェネレーターの変換  
DB2 では、シーケンスを使用して一意の識別子を生成できます。  
  
SSMA では、シーケンスを次のように変換できます。  
  
-   SQL Server シーケンスジェネレーターを使用する (このオプションは、SQL Server 2012 および SQL Server 2014) に変換する場合にのみ使用できます。  
  
-   SSMA シーケンスジェネレーターを使用します。  
  
-   列 id を使用します。  
  
SQL Server 2012 または SQL Server 2014 に変換する場合の既定のオプションは SQL Server シーケンスジェネレーターを使用することです。 ただし、SQL Server 2012 および SQL Server 2014 では、現在のシーケンス値 (DB2 sequence の例など) の取得はサポートされていません。 DB2 sequence のメソッドの移行に関するガイダンスについては、SSMA チームのブログサイトを参照してください。  
  
SSMA には、DB2 シーケンスを SSMA シーケンスエミュレーターに変換するオプションも用意されています。 2012より前の SQL Server に変換する場合、これが既定のオプションです。  
  
最後に、テーブルの列に割り当てられたシーケンスを変換して、id 値を SQL Server することもできます。 DB2 **テーブル** タブの id 列へのシーケンス間のマッピングを指定する必要があります  
  
### <a name="convert-currval-outside-triggers"></a>トリガーの外部の中の VAL を変換する  
Convert シーケンスジェネレーターが **列 id を使用**するように設定されている場合にのみ表示されます。 DB2 シーケンスはテーブルとは別のオブジェクトであるため、シーケンスを使用する多くのテーブルでは、トリガーを使用して新しいシーケンス値を生成して挿入します。 SSMA は、これらのステートメントをコメントアウトするか、コメントアウトによってエラーが生成されるときにエラーとしてマークします。  
  
-   [ **はい**] を選択した場合、ssma は、変換されたシーケンスに対する外部トリガーへのすべての参照を警告付きでマークします。  
  
-   [ **いいえ**] を選択すると、ssma は、変換されたシーケンスで、外部トリガーへのすべての参照をエラーとしてマークします。  
  
## <a name="see-also"></a>関連項目  
[ユーザーインターフェイスリファレンス &#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
