---
description: SQLExecDirect 関数
title: SQLExecDirect 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLExecDirect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLExecDirect
helpviewer_keywords:
- SQLExecDirect function [ODBC]
ms.assetid: 985fcee1-f204-425c-bdd1-deb0e7d7bbd9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0e6f2c3ed2334915d941aa9bffa898627b4dfc2e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476134"
---
# <a name="sqlexecdirect-function"></a>SQLExecDirect 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ISO 92  
  
 **まとめ**  
 **SQLExecDirect** は、ステートメント内にパラメーターが存在する場合、パラメーターマーカー変数の現在の値を使用して準備可能ステートメントを実行します。 **SQLExecDirect** は、1回限りの実行で SQL ステートメントを送信する最速の方法です。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLExecDirect(  
     SQLHSTMT     StatementHandle,  
     SQLCHAR *    StatementText,  
     SQLINTEGER   TextLength);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *StatementText*  
 代入実行する SQL ステートメント。  
  
 *TextLength*  
 代入文字の長さ **StatementText* 。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_STILL_EXECUTING、SQL_ERROR、SQL_NO_DATA、SQL_INVALID_HANDLE、SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLExecDirect**が SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返す場合、関連付けられた SQLSTATE 値を取得するには、 *Handletype* SQL_HANDLE_STMT と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **SQLExecDirect** によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01001|カーソル操作の競合|\**StatementText* には、位置指定の update または delete ステートメントが含まれており、行または複数の行が更新または削除されていません。 (複数の行の更新の詳細については、 **SQLSetStmtAttr**の SQL_ATTR_SIMULATE_CURSOR*属性*の説明を参照してください)。<br /><br /> (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01003|Set 関数で NULL 値が削除される|引数 *StatementText* には、set 関数 ( **AVG**、 **MAX**、 **MIN**など) が含まれていますが、 **COUNT** set 関数は含まれていません。また、関数が適用される前に NULL 引数値が削除されました。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データ、右側が切り捨てられました|入力/出力パラメーターまたは出力パラメーターに対して返された文字列またはバイナリデータにより、空白以外の文字または NULL 以外のバイナリデータが切り捨てられました。 文字列値の場合は、右側が切り捨てられました。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01006|権限が取り消されていません|\**StatementText* に **REVOKE** ステートメントが含まれており、ユーザーに指定された特権がありませんでした。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01007|特権が付与されていません|* \* StatementText*は**GRANT**ステートメントであり、ユーザーには指定された特権を付与できませんでした。|  
|01S02|オプションの値が変更されました|実装の動作条件により、指定されたステートメント属性は無効でした。そのため、類似した値が一時的に置き換えられました。 (**SQLGetStmtAttr** を呼び出して、一時的に置換された値がどのようになるかを判断できます)。代替値は、カーソルが閉じられるまで *StatementHandle* に対して有効です。この時点で、statement 属性は前の値に戻ります。 変更できるステートメント属性は次のとおりです。<br /><br /> SQL_ ATTR_CONCURRENCY SQL_ ATTR_CURSOR_TYPE SQL_ ATTR_KEYSET_SIZE SQL_ ATTR_MAX_LENGTH SQL_ ATTR_MAX_ROWS SQL_ ATTR_QUERY_TIMEOUT SQL_ ATTR_SIMULATE_CURSOR<br /><br /> (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01S07|小数部の切り捨て|入力/出力パラメーターまたは出力パラメーターに対して返されたデータが切り捨てられました。数値データ型の小数部が切り捨てられたか、時刻、タイムスタンプ、または期間データ型の時間部分の小数部が切り捨てられました。<br /><br /> (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|07002|カウントフィールドが正しくありません|**SQLBindParameter**で指定されたパラメーターの数が、StatementText に含まれる SQL ステートメントのパラメーターの数を下回ってい \* *StatementText*ます。<br /><br /> **SQLBindParameter**が null ポインターに設定されているか、SQL_NULL_DATA または SQL_DATA_AT_EXEC に設定されていない*StrLen_or_IndPtr* 、 *inputoutputtype*が SQL_PARAM_OUTPUT に設定さ*れてい*ないため、 **SQLBindParameter**で指定されたパラメーターの数が **StatementText*に含まれる SQL ステートメントのパラメーターの数を超えていたために呼び出されました。|  
|07006|制限されたデータ型の属性違反|バインドされたパラメーターの**SQLBindParameter**の*ValueType*引数によって識別されるデータ値を、 **SQLBindParameter**の*ParameterType*引数で識別されるデータ型に変換できませんでした。<br /><br /> SQL_PARAM_INPUT_OUTPUT または SQL_PARAM_OUTPUT としてバインドされたパラメーターに対して返されたデータ値を、 **SQLBindParameter**の*ValueType*引数で識別されるデータ型に変換できませんでした。<br /><br /> (1 つ以上の行のデータ値を変換できなかったが、1つ以上の行が正常に返された場合、この関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|07007|制限されたパラメーター値の違反|パラメーターの型 SQL_PARAM_INPUT_OUTPUT_STREAM は、パーツでデータを送受信するパラメーターにのみ使用されます。 入力バインドバッファーは、このパラメーターの型には許可されていません。<br /><br /> このエラーは、パラメーターの型が SQL_PARAM_INPUT_OUTPUT で、 \* **SQLBindParameter**で指定された*StrLen_or_IndPtr*が SQL_NULL_DATA、SQL_DEFAULT_PARAM、SQL_LEN_DATA_AT_EXEC (LEN)、または SQL_DATA_AT_EXEC と等しくない場合に発生します。|  
|07S01|既定のパラメーターの使い方が正しくありません|**SQLBindParameter**で設定されたパラメーター値が SQL_DEFAULT_PARAM ましたが、対応するパラメーターに既定値がありませんでした。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|21S01|挿入する値の一覧が列の一覧と一致しません|\**StatementText* に **INSERT** ステートメントが含まれており、挿入される値の数が派生テーブルの次数と一致しませんでした。|  
|21S02|派生テーブルの次数が列の一覧と一致しません|\**StatementText* には **CREATE VIEW** ステートメントが含まれており、非修飾列リスト (sql ステートメントの *列識別子* 引数でビューに指定された列の数) には、sql ステートメントの *クエリ指定* 引数によって定義される派生テーブル内の列数よりも多くの名前が含まれていました。|  
|22001|文字列データ、右切り捨て|文字またはバイナリ値が列に割り当てられた結果、空白以外の文字データまたは null 以外のバイナリデータが切り捨てられました。|  
|22002|インジケーター変数が必要ですが、指定されていません|NULL データは、 **SQLBindParameter**によって設定された*StrLen_or_IndPtr*が null ポインターである出力パラメーターにバインドされました。|  
|22003|数値が有効範囲にありません|**StatementText* には、バインドされた数値パラメーターまたはリテラルを含む SQL ステートメントが含まれています。この値により、関連付けられたテーブル列に割り当てられるときに、数値の一部 (小数部分ではなく) が切り捨てられます。<br /><br /> 1つ以上の入力/出力パラメーターまたは出力パラメーターに対して数値または文字列として数値または文字列として数値を返すと、切り捨てられる数値の一部 (小数部分ではなく) が発生する可能性があります。|  
|22007|無効な datetime 形式|**StatementText* には、バインドされたパラメーターとして日付、時刻、またはタイムスタンプ構造を含む SQL ステートメントが含まれていましたが、パラメーターはそれぞれ無効な日付、時刻、またはタイムスタンプです。<br /><br /> 入力/出力パラメーターまたは出力パラメーターが日付、時刻、またはタイムスタンプ C 構造体にバインドされました。返されたパラメーターの値は、それぞれ無効な日付、時刻、またはタイムスタンプです。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|22008|Datetime フィールドオーバーフロー|**StatementText* には、datetime 式を含む SQL ステートメントが含まれています。これは、計算されると、無効な日付、時刻、またはタイムスタンプ構造になります。<br /><br /> 入力/出力パラメーターまたは出力パラメーターに対して計算された datetime 式で、無効だった日付、時刻、またはタイムスタンプの C 構造体が返されました。|  
|22012|0による除算|**StatementText* に、0による除算の原因となった算術式を含む SQL ステートメントが含まれていました。<br /><br /> 入力/出力パラメーターまたは出力パラメーターに対して計算された算術式により、0除算が発生しました。|  
|22015|間隔フィールドオーバーフロー|* \* StatementText*には、数値または間隔のパラメーターが含まれています。このパラメーターは、interval SQL データ型に変換されると、有効桁数が失われる原因となります。<br /><br /> * \* StatementText*には、複数のフィールドを持つ interval パラメーターが含まれており、列の数値データ型に変換されるとき、数値データ型には表現がありませんでした。<br /><br /> * \* StatementText*には、interval sql 型に割り当てられたパラメーターデータが含まれていましたが、interval sql 型では C 型の値が表現されていませんでした。<br /><br /> 数値または期間が完全な SQL 型である入力/出力パラメーターまたは出力パラメーターを範囲 C 型に代入すると、有効桁数が失われます。<br /><br /> 入力/出力パラメーターまたは出力パラメーターが期間 C 構造体に割り当てられている場合、interval データ構造体にデータは表示されませんでした。|  
|22018|キャストの指定に無効な文字値があります|* \* StatementText*に含まれている c 型は、真数または概数、datetime、または interval データ型で、列の SQL 型が文字データ型で、列の値がバインドされた c 型の有効なリテラルではありませんでした。<br /><br /> 入力/出力パラメーターまたは出力パラメーターが返された場合、SQL 型は正確な数値、概数値、datetime、または interval データ型でした。C 型が SQL_C_CHAR でした。列の値が、バインドされた SQL 型の有効なリテラルではありませんでした。|  
|22019|エスケープ文字が無効です|\**StatementText*を含む SQL ステートメントに含まれている、**LIKE**の述語では、**エスケープ**で、**WHERE**句とエスケープの長さ次の文字**エスケープ**が 1 と等しくありません。|  
|22025|無効なエスケープシーケンスです|\**StatementText*を含む SQL ステートメントに含まれる"**LIKE** _パターン値_ **エスケープ** _エスケープ文字_"で、**WHERE**句、およびパターンの値のエスケープ文字の後の文字が「%」または「_」のいずれか。|  
|23000|整合性制約違反|**StatementText* には、パラメーターまたはリテラルを含む SQL ステートメントが含まれていました。 関連付けられているテーブル列に NOT NULL として定義されている列に対して、パラメーター値が NULL でした。一意の値のみが含まれるように制約された列に重複した値が指定されたか、他の整合性制約に違反しています。|  
|24000|カーソル状態が無効|カーソルは、 **sqlfetch**または**sqlfetchscroll**によって*StatementHandle*に配置されました。 このエラーは、 **Sqlfetch** または **sqlfetchscroll** が SQL_NO_DATA 返されなかった場合にドライバーマネージャーによって返されます。また、 **Sqlfetch** または **sqlfetchscroll** が SQL_NO_DATA を返した場合は、ドライバーによって返されます。<br /><br /> カーソルが開いていましたが、 *StatementHandle*に配置されていません。<br /><br /> **StatementText* には、位置指定の update または delete ステートメントが含まれており、カーソルが結果セットの先頭の前、または結果セットの末尾の後に配置されました。|  
|34000|カーソル名が無効|**StatementText* には、位置指定の update または delete ステートメントが含まれており、実行されているステートメントによって参照されているカーソルが開かれていませんでした。|  
|3D000|無効なカタログ名|*StatementText*で指定されたカタログ名が無効でした。|  
|3F000|スキーマ名が無効です|*StatementText*で指定されたスキーマ名が無効でした。|  
|40001|シリアル化エラー|リソースが別のトランザクションでデッドロックしているため、トランザクションがロールバックされました。|  
|40003|ステートメントの完了が不明です|この関数の実行中に関連付けられた接続に失敗しました。トランザクションの状態を確認できません。|  
|42000|構文エラーまたはアクセス違反|\**StatementText* に、準備可能ではない SQL ステートメントが含まれているか、構文エラーが含まれています。<br /><br /> ユーザーには、**StatementText*に含まれる SQL ステートメントを実行する権限がありませんでした。|  
|42 S01|ベーステーブルまたはビューが既に存在します|\**StatementText* に **CREATE TABLE** または **CREATE VIEW** ステートメントが含まれており、指定されたテーブル名またはビュー名が既に存在します。|  
|42 S02|ベーステーブルまたはビューが見つかりません|\**StatementText* に **drop Table** または **drop view** ステートメントが含まれており、指定されたテーブル名またはビュー名が存在しませんでした。<br /><br /> \**StatementText* に **ALTER TABLE** ステートメントが含まれており、指定されたテーブル名が存在しませんでした。<br /><br /> \**StatementText* に **CREATE VIEW** ステートメントが含まれており、クエリ仕様で定義されているテーブル名またはビュー名が存在しませんでした。<br /><br /> \**StatementText* に **CREATE INDEX** ステートメントが含まれており、指定されたテーブル名が存在しませんでした。<br /><br /> \**StatementText* に **GRANT** ステートメントまたは **REVOKE** ステートメントが含まれており、指定されたテーブル名またはビュー名が存在しませんでした。<br /><br /> \**StatementText* に **select** ステートメントが含まれており、指定されたテーブル名またはビュー名が存在しませんでした。<br /><br /> \**StatementText* に **DELETE**、 **INSERT**、または **UPDATE** ステートメントが含まれていますが、指定されたテーブル名が存在しませんでした。<br /><br /> \**StatementText* に **CREATE TABLE** ステートメントが含まれており、(作成されているテーブル以外のテーブルを参照している) 制約で指定されたテーブルが存在しませんでした。<br /><br /> \**StatementText* に **CREATE SCHEMA** ステートメントが含まれており、指定されたテーブル名またはビュー名が存在しませんでした。|  
|42 S11|インデックスは既に存在します|\**StatementText* に **CREATE INDEX** ステートメントが含まれており、指定されたインデックス名が既に存在します。<br /><br /> \**StatementText* に **CREATE SCHEMA** ステートメントが含まれており、指定されたインデックス名が既に存在します。|  
|42 S12|インデックスが見つかりません|\**StatementText* に **DROP INDEX** ステートメントが含まれており、指定されたインデックス名が存在しませんでした。|  
|42 S21|列は既に存在します|\**StatementText* に **ALTER TABLE** ステートメントが含まれており、 **ADD** 句で指定された列が一意でないか、ベーステーブル内の既存の列を識別しています。|  
|42 S22|列が見つかりません|\**StatementText* に **CREATE INDEX** ステートメントが含まれており、列リストで指定された1つ以上の列名が存在しませんでした。<br /><br /> \**StatementText* に **GRANT** ステートメントまたは **REVOKE** ステートメントが含まれており、指定された列名が存在しませんでした。<br /><br /> \**StatementText* に **select**、 **DELETE**、 **INSERT**、または **UPDATE** ステートメントが含まれており、指定された列名が存在しませんでした。<br /><br /> \**StatementText* に **CREATE TABLE** ステートメントが含まれており、制約 (作成されるテーブル以外のテーブルを参照している) で指定された列が存在しませんでした。<br /><br /> \**StatementText* に **CREATE SCHEMA** ステートメントが含まれており、指定された列名が存在しませんでした。|  
|44000|WITH CHECK OPTION 違反|引数 *StatementText* には、表示されたテーブルに対して実行される **insert** ステートメント、または **WITH CHECK OPTION**を指定して作成されたテーブルから派生したテーブルが含まれています。この場合、 **insert** ステートメントによって影響を受ける1つ以上の行が表示されているテーブルに存在しなくなります。<br /><br /> 引数 *StatementText* には、表示されているテーブルに対して実行される **UPDATE** ステートメント、または **WITH CHECK OPTION**を指定して作成されたテーブルから派生したテーブルが含まれています。この場合、 **update** ステートメントによって影響を受ける1つ以上の行が表示されているテーブルに存在しなくなります。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 関数が呼び出され、実行が完了する前に、 **SQLCancel** または **Sqlcancelhandle** が *StatementHandle*で呼び出されました。 次に、 *StatementHandle*で関数が再度呼び出されました。<br /><br /> 関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqlcancelhandle**が呼び出されました。|  
|HY009|Null ポインターの使い方が正しくありません|(DM) **StatementText* は null ポインターでした。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **SQLExecDirect** 関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が *StatementHandle* に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 引数 *TextLength* が0以下で、SQL_NTS と等しくない。<br /><br /> **SQLBindParameter**で設定されたパラメーター値が null ポインターで、パラメーターの長さの値が0、SQL_NULL_DATA、SQL_DATA_AT_EXEC、SQL_DEFAULT_PARAM、または SQL_LEN_DATA_AT_EXEC_OFFSET 以下でした。<br /><br /> **SQLBindParameter**で設定されたパラメーター値が null ポインターではありませんでした。C データ型が SQL_C_BINARY または SQL_C_CHAR;また、パラメーターの長さの値が0未満ですが、SQL_NTS、SQL_NULL_DATA、SQL_DATA_AT_EXEC、SQL_DEFAULT_PARAM、または SQL_LEN_DATA_AT_EXEC_OFFSET 以下ではありませんでした。<br /><br /> **SQLBindParameter**によってバインドされたパラメーター長値が SQL_DATA_AT_EXEC に設定されました。SQL 型は、SQL_LONGVARCHAR、SQL_LONGVARBINARY、またはデータソース固有の長いデータ型のいずれかです。また、 **SQLGetInfo**の SQL_NEED_LONG_DATA_LEN 情報の種類は "Y" でした。|  
|HY105|パラメーターの型が無効です|**SQLBindParameter**の引数*inputoutputtype*に指定された値が SQL_PARAM_OUTPUT でしたが、パラメーターが入力パラメーターでした。|  
|HY109|カーソル位置が無効です|\**StatementText* には、位置指定の update または delete ステートメントが含まれており、削除された行またはフェッチできなかった行でカーソルが ( **SQLSetPos** または **sqlfetchscroll**によって) 配置されました。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|SQL_ATTR_CONCURRENCY および SQL_ATTR_CURSOR_TYPE statement 属性の現在の設定の組み合わせは、ドライバーまたはデータソースではサポートされていませんでした。<br /><br /> SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE statement 属性が、ドライバーがブックマークをサポートしていないカーソルの種類に設定されました。|  
|HYT00|タイムアウトに達しました|データソースから結果セットが返される前に、クエリのタイムアウト期間が経過しました。 タイムアウト期間は、 **SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT によって設定されます。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 アプリケーションは **SQLExecDirect** を呼び出して、データソースに SQL ステートメントを送信します。 直接実行の詳細については、「 [直接実行](../../../odbc/reference/develop-app/direct-execution-odbc.md)」を参照してください。 ドライバーは、データソースによって使用される SQL の形式を使用するようにステートメントを変更し、データソースに送信します。 特に、ドライバーは、SQL で特定の機能を定義するために使用されるエスケープシーケンスを変更します。 エスケープシーケンスの構文については、「 [ODBC でのエスケープシーケンス](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)」を参照してください。  
  
 アプリケーションでは、SQL ステートメントに1つ以上のパラメーターマーカーを含めることができます。 パラメーターマーカーを含めるには、アプリケーションで適切な位置に疑問符 (?) を SQL ステートメントに埋め込みます。 パラメーターの詳細については、「 [ステートメントパラメーター](../../../odbc/reference/develop-app/statement-parameters.md)」を参照してください。  
  
 SQL ステートメントが **SELECT** ステートメントであり、アプリケーションが **SQLSetCursorName** を呼び出してカーソルをステートメントに関連付ける場合、ドライバーは指定されたカーソルを使用します。 それ以外の場合、ドライバーはカーソル名を生成します。  
  
 データソースが手動コミットモード (明示的なトランザクションの開始が必要) であり、トランザクションがまだ開始されていない場合、ドライバーは SQL ステートメントを送信する前にトランザクションを開始します。 詳細については、「 [手動コミットモード](../../../odbc/reference/develop-app/manual-commit-mode.md)」を参照してください。  
  
 アプリケーションで **SQLExecDirect** を使用して **COMMIT** ステートメントまたは **ROLLBACK** ステートメントを送信する場合、DBMS 製品間で相互運用することはできません。 トランザクションをコミットまたはロールバックするには、アプリケーションが **SQLEndTran**を呼び出します。  
  
 **SQLExecDirect**が実行時データパラメーターを検出すると、SQL_NEED_DATA が返されます。 アプリケーションは、 **Sqlparamdata** と **sqlparamdata**を使用してデータを送信します。 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)、 [sqlparamdata](../../../odbc/reference/syntax/sqlparamdata-function.md)、 [Sqlparamdata](../../../odbc/reference/syntax/sqlputdata-function.md)、および[長いデータの送信](../../../odbc/reference/develop-app/sending-long-data.md)に関する情報を参照してください。  
  
 **SQLExecDirect**を実行すると、データソースの行に影響を与えない、検索された update、insert、または delete ステートメントが実行された場合、 **SQLExecDirect**を呼び出すと SQL_NO_DATA が返されます。  
  
 SQL_ATTR_PARAMSET_SIZE statement 属性の値が1より大きく、SQL ステートメントに少なくとも1つのパラメーターマーカーが含まれている場合、 **SQLExecDirect**は、 **SQLBindParameter**への呼び出しで*parametervaluepointer*引数が指す配列のパラメーター値のセットごとに、sql ステートメントを1回実行します。 詳細については、「 [パラメーター値の配列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)」を参照してください。  
  
 ブックマークが有効になっていて、ブックマークをサポートできないクエリが実行された場合、ドライバーは、属性値を変更して SQLSTATE 01S02 (オプション値が変更されました) を返すことによって、ブックマークをサポートする環境を強制的に実行しようとする必要があります。 属性を変更できない場合、ドライバーは SQLSTATE HY024 (無効な属性値) を返す必要があります。  
  
> [!NOTE]  
>  接続プールを使用する場合、アプリケーションは、データベースまたはデータベースのコンテキストを変更する SQL ステートメントを実行する必要があります。たとえば、データソースによって使用されるカタログを変更する SQL Server の **use** _database_ ステートメントなどです。  
  
## <a name="code-example"></a>コード例  
 「 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)、 [SQLGETDATA](../../../odbc/reference/syntax/sqlgetdata-function.md)、 [Sample ODBC Program](../../../odbc/reference/sample-odbc-program.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|結果セット内の列へのバッファーのバインド|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|コミットまたはロールバック操作の実行|[SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|準備された SQL ステートメントの実行|[SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|複数行のデータのフェッチ|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|データのブロックのフェッチまたは結果セットのスクロール|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|カーソル名を返す|[SQLGetCursorName 関数](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|データ列の一部またはすべてをフェッチしています|[SQLGetData 関数](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|データを送信する次のパラメーターを返す|[SQLParamData 関数](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|実行するステートメントの準備|[SQLPrepare 関数](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|実行時にパラメーターデータを送信する|[SQLPutData 関数](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|カーソル名の設定|[SQLSetCursorName 関数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
|ステートメント属性の設定|[SQLSetStmtAttr 関数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
