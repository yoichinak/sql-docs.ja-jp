---
description: ODBC 関数の概要
title: ODBC 関数の概要 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], listed by task
ms.assetid: 7aa635da-e6b7-439f-8e9b-c3860e24de5e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 50a0b9146acd71f87b4dd65bbdd34c67725e9948
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487375"
---
# <a name="odbc-function-summary"></a>ODBC 関数の概要
次の表に、タスクの種類ごとにグループ化された ODBC 関数の一覧を示します。また、各関数の目的について、準拠の指定と簡単な説明が含まれています。 準拠の表記の詳細については、「 [ODBC と標準 CLI](../../../odbc/reference/odbc-and-the-standard-cli.md)」を参照してください。 各関数の構文とセマンティクスの詳細については、「 [ODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)」を参照してください。  
  
 アプリケーションは **SQLGetInfo** 関数を呼び出して、ドライバーに関する準拠情報を取得できます。 ドライバー内の特定の関数のサポートに関する情報を取得するために、アプリケーションは **Sqlgetfunctions**を呼び出すことができます。  
  
|タスク|関数名|互換性|目的|  
|----------|-------------------|-----------------|-------------|  
|データ ソースに接続する|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|ISO 92|環境、接続、ステートメント、または記述子ハンドルを取得します。|  
||[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|ISO 92|データソース名、ユーザー ID、およびパスワードを指定して、特定のドライバーに接続します。|  
||[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|ODBC|接続文字列によって特定のドライバーに接続します。または、ドライバーマネージャーとドライバーにユーザーの接続ダイアログボックスが表示されるように要求します。|  
||[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|ODBC|連続する接続属性のレベルと有効な属性値を返します。 各接続属性に値が指定されると、はデータソースに接続します。|  
|ドライバーとデータソースに関する情報の取得|[SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)<br /><br /> [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|ISO 92<br /><br /> ODBC|使用できるデータソースの一覧を返します。<br /><br /> インストールされているドライバーとその属性の一覧を返します。|  
||[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|ISO 92|特定のドライバーとデータソースに関する情報を返します。|  
||[SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)|ISO 92|サポートされているドライバー関数を返します。|  
||[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|ISO 92|サポートされているデータ型に関する情報を返します。|  
|ドライバー属性の設定と取得|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)<br /><br /> [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|ISO 92<br /><br /> ISO 92|接続属性を設定します。<br /><br /> 接続属性の値を返します。|  
||[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|ISO 92|環境属性を設定します。|  
||[SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|ISO 92|環境属性の値を返します。|  
||[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|ISO 92|ステートメントの属性を設定します。|  
||[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|ISO 92|ステートメント属性の値を返します。|  
|記述子フィールドの設定と取得|[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)<br /><br /> [SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|ISO 92<br /><br /> ISO 92|単一の記述子フィールドの値を返します。<br /><br /> 複数の記述子フィールドの値を返します。|  
||[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|ISO 92|単一の記述子フィールドを設定します。|  
||[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|ISO 92|複数の記述子フィールドを設定します。|  
||[SQLCopyDesc](../../../odbc/reference/syntax/sqlcopydesc-function.md)|ISO 92|記述子の情報を1つの記述子ハンドルから別の記述子ハンドルにコピーします。|  
|SQL 要求の準備|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|ISO 92|後で実行するために SQL ステートメントを準備します。|  
||[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|ODBC|SQL ステートメントのパラメーターにストレージを割り当てます。|  
||[SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|ISO 92|ステートメントハンドルに関連付けられたカーソル名を返します。|  
||[SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|ISO 92|カーソル名を指定します。|  
||[SQLSetScrollOptions](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|ODBC|カーソルの動作を制御するオプションを設定します。|  
|要求の送信|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)<br /><br /> [SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|ISO 92<br /><br /> ISO 92|準備されたステートメントを実行します。<br /><br /> ステートメントを実行します。|  
||[SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)|ODBC|ドライバーによって変換された SQL ステートメントのテキストを返します。|  
||[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|ODBC|ステートメント内の特定のパラメーターの説明を返します。|  
||[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|ISO 92|ステートメント内のパラメーターの数を返します。|  
||[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|ISO 92|実行時にパラメーターデータを提供するために、 **Sqlputdata** と組み合わせて使用されます。 (長いデータ値に役立ちます)。|  
||[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|ISO 92|パラメーターのデータ値の一部またはすべてを送信します。 (長いデータ値に役立ちます)。|  
|結果と結果に関する情報の取得|[SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md)<br /><br /> [SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|ISO 92<br /><br /> ISO 92|挿入、更新、または削除要求の影響を受けた行数を返します。<br /><br /> 結果セット内の列数を返します。|  
||[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|ISO 92|結果セットの列について説明します。|  
||[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|ISO 92|結果セットの列の属性について説明します。|  
||[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|ISO 92|結果列にストレージを割り当て、データ型を指定します。|  
||[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|ISO 92|複数の結果行を返します。|  
||[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|ISO 92|スクロール可能な結果行を返します。|  
||[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|ISO 92|結果セットの1つの行の1つの列の一部またはすべてを返します。 (長いデータ値に役立ちます)。|  
||[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|ODBC|フェッチされたデータブロック内にカーソルを配置し、アプリケーションが行セット内のデータを更新したり、結果セット内のデータを更新または削除したりできるようにします。|  
||[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|ODBC|更新、削除、およびブックマークによるフェッチを含む一括挿入操作と一括ブックマーク操作を実行します。|  
||[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|ODBC|より多くの結果セットが使用可能かどうかを判断し、存在する場合は、次の結果セットの処理を初期化します。|  
||[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|ISO 92|追加の診断情報 (診断データ構造の1つのフィールド) を返します。|  
||[SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|ISO 92|追加の診断情報 (診断データ構造の複数のフィールド) を返します。|  
|データソースのシステムテーブルに関する情報の取得 (カタログ関数)|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)<br /><br /> [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|ODBC<br /><br /> [グループを開く]|1つ以上のテーブルについて、列と関連付けられている権限の一覧を返します。<br /><br /> 指定されたテーブル内の列名の一覧を返します。|  
||[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|ODBC|指定されたテーブルに外部キーが存在する場合は、外部キーを構成する列名の一覧を返します。|  
||[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|ODBC|テーブルの主キーを構成する列名の一覧を返します。|  
||[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|ODBC|入力パラメーターと出力パラメーターの一覧、および指定されたプロシージャの結果セットを構成する列を返します。|  
||[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|ODBC|特定のデータソースに格納されているプロシージャ名の一覧を返します。|  
||[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|[グループを開く]|指定されたテーブル内の行を一意に識別する最適な列のセット、または行のいずれかの値がトランザクションによって更新されたときに自動的に更新される列の情報を返します。|  
||[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|ISO 92|1つのテーブルに関する統計と、テーブルに関連付けられているインデックスの一覧を返します。|  
||[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|ODBC|テーブルと、各テーブルに関連付けられている権限の一覧を返します。|  
||[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|[グループを開く]|特定のデータソースに格納されているテーブル名の一覧を返します。|  
|ステートメントを終了する|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|ISO 92|ステートメントの処理を終了し、保留中の結果を破棄します。また、必要に応じて、ステートメントハンドルに関連付けられているすべてのリソースを解放します。|  
||[SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)|ISO 92|ステートメントハンドルで開かれたカーソルを閉じます。|  
||[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|ISO 92|ステートメントの処理をキャンセルします。|  
||[SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|ODBC|ステートメントまたは接続の処理をキャンセルします。|  
||[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|ISO 92|トランザクションをコミットまたはロールバックします。|  
|接続を終了しています|[SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|ISO 92<br /><br /> ISO 92|接続を閉じます。<br /><br /> 環境、接続、ステートメント、または記述子ハンドルを解放します。|
