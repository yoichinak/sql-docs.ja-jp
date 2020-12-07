---
description: コア レベルの API 関数 (ODBC Driver for Oracle)
title: コアレベルの API 関数 (ODBC Driver for Oracle) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- core level API functions [ODBC]
- ODBC core level API functions [ODBC]
ms.assetid: 8596eed7-bda6-4cac-ae1f-efde1aab785f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c0940dd9fbabc02a5fd384208b2dcd4803f4f24a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471654"
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>コア レベルの API 関数 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用してください。  
  
 このレベルの関数は、ODBC ドライバーのインターフェイス準拠の最小レベルを構成します。  
  
|API 関数|ノート|  
|------------------|-----------|  
|**SQLAllocConnect**|*Henv*によって識別される環境内の接続ハンドル*hdbc*にメモリを割り当てます。 ドライバーマネージャーはこの呼び出しを処理し、 **SQLConnect**、 **SQLBrowseConnect**、または**SQLDriverConnect**が呼び出されるたびに、ドライバーの**sqlallocconnect**関数を呼び出します。|  
|**SQLAllocEnv**|Oracle クライアントソフトウェアの要件を指定するダイアログボックスを表示し、SQL_NULL_HANDLE を返します。 Oracle クライアントソフトウェアがインストールされていない場合、この関数は環境ハンドル *henv*にメモリを割り当て、アプリケーションで使用するために ODBC 呼び出しレベルインターフェイスを初期化します。|  
|**SQLAllocStmt**|ステートメントハンドルにメモリを割り当て、hdbc によって指定された接続にステートメントハンドルを関連付けます。 ドライバーマネージャーは、この呼び出しをドライバーに渡します。これにより、hstmt 構造体のメモリが割り当てられます。|  
|**SQLBindCol**|結果列にストレージ領域を割り当て、結果の型を指定します。|  
|**SQLCancel**|ステートメントハンドルである hstmt の処理を取り消します。 場合によっては、Oracle では実行中のステートメントを取り消すことができません。 つまり、実行中のステートメントは、Oracle がプロセスを完了するまで続行されます。この時点で、ステートメントの結果は ODBC Driver for Oracle によって取り消されます。|  
|**SQLColAttributes**|結果セットの列の記述子情報を返します。 記述子情報は、文字列、32ビット記述子に依存する値、または整数値として返されます。|  
|**SQLConnect**|データソースに接続します。 Oracle オペレーティングシステム認証を使用するには、 *Szuid* パラメーターとして "/" を指定し、"" を *szauthstr* パラメーターとして指定します。|  
|**SQLDescribeCol**|指定された結果列の名前、型、有効桁数、小数点以下桁数、および null 値の許容属性を返します。 **注: SQLDescribeCol では** 、計算列が SQL_VARCHAR として報告されます。|  
|**SQLDisconnect**|接続を閉じます。 共有環境に対して接続プールが有効になっていて、アプリケーションがその環境の接続で **Sqldisconnect** を呼び出した場合、接続は接続プールに返され、同じ共有環境を使用している他のコンポーネントでも使用できます。|  
|**SQLError**|前回のエラーに関するエラーまたは状態の情報を返します。 ドライバーは、 **SQLError**の呼び出し方法に応じて、 *hstmt*、 *hdbc*、および*henv*引数に対して返される可能性のあるスタックまたはエラーの一覧を保持します。 エラーキューは、各ステートメントの後にフラッシュされます。 は通常、Oracle エラーメッセージを取得し、それ以外は空です。|  
|**SQLExecDirect**|新しい準備されていない SQL ステートメントを実行します。 ステートメントにパラメーターが存在する場合、ドライバーはパラメーターマーカー変数の現在の値を使用します。 テーブル、ビュー、またはフィールドの名前にスペースが含まれている場合は、名前を後方引用符で囲みます。 たとえば、データベースに *My table* という名前のテーブルとフィールド *my field*が含まれている場合は、識別子の各要素を次のように囲みます。<br /><br /> [テーブル] を選択し \` \` ます。 \`Field1 \` 、; \`マイテーブル \` 。 \`\`テーブルからのマイ Field2 \`\`|  
|**SQLExecute**|準備された SQL ステートメント ( **SQLPrepare**によって既に準備されているステートメント) を実行します。 ステートメントにパラメーターが存在する場合、ドライバーはパラメーターマーカー変数の現在の値を使用します。|  
|**SQLFetch**|**SQLBindCol**の前の呼び出しで指定された場所に、結果セットから1つの行を取得します。 バインドされていない列の **SQLGetData** の呼び出しをドライバーに準備します。|  
|**SQLFreeConnect**|接続ハンドルを解放し、そのハンドルに割り当てられたすべてのメモリを解放します。|  
|**SQLFreeEnv**|ODBC Driver for Oracle を閉じ、ドライバーに関連付けられているすべてのメモリを解放します。|  
|**SQLFreeStmt**|特定の hstmt に関連付けられている処理を停止し、その hstmt に関連付けられている開いているカーソルを閉じ、保留中の結果を破棄し、オプションでステートメントハンドルに関連付けられているすべてのリソースを解放します。|  
|**SQLGetCursorName**|指定された hstmt に関連付けられているカーソルの名前を返します。|  
|**SQLNumResultCols**|結果セットのカーソル内の列の数を返します。|  
|**SQLPrepare**|ステートメントを最適化および実行する方法を計画して、SQL ステートメントを準備します。 SQL ステートメントは、 **SQLExecDirect**によって実行されるようにコンパイルされます。<br /><br /> テーブル、ビュー、またはフィールドの名前にスペースが含まれている場合は、名前を後方引用符で囲みます。 たとえば、データベースに *My table* という名前のテーブルとフィールド *my field*が含まれている場合は、識別子の各要素を次のように囲みます。<br /><br /> [テーブル] を選択し \` \` ます。 \`\`テーブルからのマイフィールド \`\`<br /><br /> 配列を含む結果セットを仮パラメーターとして使用する方法の詳細については、「 [ストアドプロシージャから配列パラメーターを返す](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)」を参照してください。|  
|**SQLRowCount**|Oracle では、最後の行をフェッチしてから、-1 を返すまで、結果セット内の行の数を確認する方法は提供されていません。|  
|**SQLSetCursorName**|カーソル名をアクティブなステートメントハンドルである *hstmt*に関連付けます。|  
|**SQLSetParam**|ODBC 2 では SQLBindParameter に置き換えられました。*x*。|  
|**SQLTransact**|接続に関連付けられているすべてのステートメントハンドル (hstmts) のすべてのアクティブな操作、または環境ハンドル *henv*に関連付けられているすべての接続に対して、コミットまたはロールバックの操作を要求します。 手動モードでコミットが失敗した場合、トランザクションはアクティブのままです。トランザクションをロールバックするか、コミット操作を再試行するかを選択できます。 自動トランザクションモードでコミット操作が失敗した場合、トランザクションは自動的にロールバックされます。トランザクションを非アクティブにすることはできません。|
