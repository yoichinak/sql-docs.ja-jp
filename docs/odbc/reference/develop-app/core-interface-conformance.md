---
description: コア インターフェイスの適合性
title: コアインターフェイスの準拠 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- core-level interface conformance levels [ODBC]
ms.assetid: aaaa864a-6477-45ff-a50a-96d8db66a252
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1ca38e2b616c39839cfe813dad984f7eba3796a6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465844"
---
# <a name="core-interface-conformance"></a>コア インターフェイスの適合性
すべての ODBC ドライバーは、少なくともコアレベルのインターフェイスへの準拠を示す必要があります。 コアレベルの機能は、ほとんどの一般的な相互運用可能なアプリケーションで必要とされる機能なので、ドライバーはこのようなアプリケーションで動作します。 コアレベルの機能は、ISO CLI 仕様で定義されている機能と、Open Group CLI 仕様で定義されているオプション以外の機能にも対応しています。 コアレベルのインターフェイスに準拠した ODBC ドライバーを使用すると、アプリケーションは次のすべての操作を実行できます。  
  
-   **SQLAllocHandle**と**sqlfreehandle**を呼び出すことによって、すべての種類のハンドルを割り当て、解放します。  
  
-   **SQLFreeStmt**関数のすべての形式を使用します。  
  
-   **SQLBindCol**を呼び出して、結果セットの列をバインドします。  
  
-   **SQLBindParameter**および**sqlnumparams**を呼び出して、パラメーターの配列を含む動的パラメーターを入力方向にのみ処理します。 (出力方向のパラメーターは、 [レベル2のインターフェイス準拠](../../../odbc/reference/develop-app/level-2-interface-conformance.md)の機能203です)。  
  
-   バインドオフセットを指定します。  
  
-   **Sqlparamdata**および**sqlparamdata**の呼び出しに関連する、実行時データダイアログを使用します。  
  
-   **SqlcloSQLSetCursorName**、 **sqlgetcursor Name**、および**SQLSetCursorName**を呼び出して、カーソルとカーソル名を管理します。  
  
-   **Sqlcolattribute**、 **SQLDescribeCol**、 **sqlnumresultcols**、および**SQLRowCount**を呼び出すことにより、結果セットの説明 (メタデータ) にアクセスできます。 (列番号0に対してこれらの関数を使用すると、ブックマークメタデータを取得できます。これは、 [レベル2のインターフェイス準拠](../../../odbc/reference/develop-app/level-2-interface-conformance.md)の機能204です)。  
  
-   カタログ関数 **Sqlcolumns**、 **SQLGetTypeInfo**、 **Sqlcolumns**、および **sqlcolumns**を呼び出して、データディクショナリに対してクエリを実行します。  
  
     このドライバーは、データベーステーブルおよびビューのマルチパート名をサポートするためには必要ありません。 (詳細については、「 [level 1 Interface 適合性](../../../odbc/reference/develop-app/level-1-interface-conformance.md) 」の「feature 101」と「 [Level 2 interface 適合性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)」の機能201を参照してください)。ただし、列の修飾やインデックスの名前など、SQL-92 仕様の特定の機能は、マルチパートの名前付けと構文的に比較されます。 現在の ODBC 機能の一覧は、SQL-92 のこれらの側面に新しいオプションを導入するためのものではありません。  
  
-   **SQLConnect**、 **sqldatasources**、 **sqldatasources**、 **SQLDriverConnect**を呼び出すことによって、データソースと接続を管理します。 **Sqldrivers**を呼び出すことによって、サポートされている ODBC レベルに関係なく、ドライバーに関する情報を取得します。  
  
-   **SQLExecDirect**、 **Sqlexecute**、および**SQLPrepare**を呼び出すことにより、SQL ステートメントを準備して実行します。  
  
-   **Sqlfetch**を呼び出すか、または*fetchorientation*引数を SQL_FETCH_NEXT に設定して**sqlfetchscroll**を呼び出して、結果セットの1行または複数行を前方方向にのみフェッチします。  
  
-   **SQLGetData**を呼び出して、部分的にバインドされていない列を取得します。  
  
-   **Sqlgetconnectattr**、 **SQLGetEnvAttr**、および**SQLGetStmtAttr**を呼び出してすべての属性の現在の値を取得し、すべての属性を既定値に設定し、 **SQLSetConnectAttr**、 **SQLSetEnvAttr**、および**SQLSetStmtAttr**を呼び出して、特定の属性を既定値以外の値に設定します。  
  
-   **Sqlcopydesc**、 **SQLGetDescField**、 **sqlgetdescrec**、 **SQLSetDescField**、および**SQLSetDescRec**を呼び出して、特定のフィールドの記述子を操作します。  
  
-   **SQLGetDiagField**と**SQLGetDiagRec**を呼び出して、診断情報を取得します。  
  
-   **Sqlgetfunctions**と**SQLGetInfo**を呼び出して、ドライバーの機能を検出します。 また、 **Sqlnativesql**を呼び出して、SQL ステートメントに対して行われたすべてのテキスト置換の結果をデータソースに送信する前に検出します。  
  
-   **SQLEndTran**の構文を使用してトランザクションをコミットします。 コアレベルのドライバーでは、真のトランザクションをサポートする必要はありません。そのため、アプリケーションでは、SQL_ATTR_AUTOCOMMIT 接続属性に SQL_ROLLBACK と SQL_AUTOCOMMIT_OFF を指定することはできません。 (詳細については、「 [Level 2 Interface 適合性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)」の「feature 109」を参照してください)。  
  
-   **SQLCancel**を呼び出して、実行時データダイアログをキャンセルし、マルチスレッド環境で、別のスレッドで実行されている ODBC 関数をキャンセルします。 コアレベルのインターフェイスへの準拠では、関数の非同期実行のサポートは行われません。また、 **SQLCancel** を使用して非同期に実行する ODBC 関数を取り消すこともできません。 ドライバーが独立したアクティビティを同時に実行するには、プラットフォームも ODBC ドライバーもマルチスレッドである必要はありません。 ただし、マルチスレッド環境では、ODBC ドライバーがスレッドセーフである必要があります。 アプリケーションからの要求のシリアル化は、パフォーマンスに重大な問題が発生する可能性がある場合でも、この仕様を実装するための準拠した方法です。  
  
-   **Sql特徴的な列**を呼び出して、テーブルの SQL_BEST_ROWID 行を識別する列を取得します。 (SQL_ROWVER のサポートは、 [レベル2のインターフェイス準拠](../../../odbc/reference/develop-app/level-2-interface-conformance.md)の機能208です)。  
  
    > [!IMPORTANT]  
    >  ODBC ドライバーは、コアインターフェイスの準拠レベルで関数を実装する必要があります。
