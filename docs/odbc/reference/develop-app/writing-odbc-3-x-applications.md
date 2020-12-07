---
description: ODBC 3.x アプリケーションの作成
title: ODBC 3.x アプリケーションの作成 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], about upgrading
- ODBC drivers [ODBC], backward compatibility
- upgrading applications [ODBC]
- compatibility [ODBC], upgrading applications
- application upgrades [ODBC]
- upgrading applications [ODBC], about upgrading
- backward compatibility [ODBC], upgrading applications
ms.assetid: 19c54fc5-9dd6-49b6-8c9f-a38961b40a65
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7df97b99df10e613ee45aaa3c01174b46160e740
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421356"
---
# <a name="writing-odbc-3x-applications"></a>ODBC 3.x アプリケーションの作成
*Odbc 2.x アプリケーションを*odbc 3.x にアップグレードする場合は *、odbc* *2.x と 2.x*の両方*のドライバーで*動作するように記述する必要があります。 ODBC *3. x* 機能を最大限に活用するには、アプリケーションに条件付きコードを組み込む必要があります。  
  
 SQL_ATTR_ODBC_VERSION 環境属性を SQL_OV_ODBC2 に設定する必要があります。 これにより、「[動作の変更](../../../odbc/reference/develop-app/behavioral-changes.md)」セクションで説明した変更に関して、ドライバーが ODBC 2.x ドライバーのように動作することが保証され*ます。*  
  
 アプリケーションで、「 [新機能](../../../odbc/reference/develop-app/new-features.md)」で説明されている機能のいずれかを使用する場合は、ドライバーが odbc *3.X または odbc 2.x* *ドライバーで* あるかどうかを判断するために、条件付きコードを使用する必要があります。 このアプリケーションでは、 **SQLGetDiagField**と**SQLGetDiagRec**を使用して、これらの条件付きコードフラグメントでエラー処理を行っているときに ODBC 2.x sqlstates を取得*します。* 新しい機能については、次の点を考慮する必要があります。  
  
-   行セットサイズの動作の変更によって影響を受けるアプリケーションは、配列のサイズが1より大きい場合に **Sqlfetch** を呼び出さないように注意する必要があります。 これらのアプリケーションは、 **SQLExtendedFetch** の呼び出しを **SQLSetStmtAttr** の呼び出しに置き換えて、SQL_ATTR_ARRAY_STATUS_PTR Statement 属性と **sqlfetchscroll**を設定します。これにより、ODBC *3. x* ドライバーと odbc *2.x ドライバーの* 両方で動作する共通のコードが使用できるようになります。 **SQLSetStmtAttr** with SQL_ATTR_ROW_ARRAY_SIZE は *、ODBC 2.x*ドライバーの SQL_ROWSET_SIZE と共に**SQLSetStmtAttr**にマップされるため、アプリケーションでは、複数行のフェッチ操作に SQL_ATTR_ROW_ARRAY_SIZE を設定するだけで済みます。  
  
-   アップグレードされるほとんどのアプリケーションは、SQLSTATE コードの変更によって実際に影響を受けることはありません。 影響を受けるアプリケーションに対しては、機械検索を実行でき *ます。ほとんど* の場合、"SQLSTATE マッピング" セクションのエラー変換テーブルを使用して odbc 2.x のエラーコードを odbc 2.x *のコードに* 変換します。 *Odbc 3.X ドライバーマネージャー* *は ODBC 2.x*から odbc *3. x* sqlstates へのマッピングを実行するため、これらのアプリケーションの作成者は odbc *3. x* SQLSTATES をチェックするだけで *、odbc 2.x*を条件付きコードに含める必要がありません。  
  
-   アプリケーションで日付、時刻、およびタイムスタンプデータ型を使用する場合は、アプリケーションがそれ自体を ODBC 2.x アプリケーションとして宣言し、その既存のコードを使用して、エアコンコードを使用することは *できません* 。  
  
 アップグレードには、次の手順も含まれる必要があります。  
  
-   接続を割り当てる前に **SQLSetEnvAttr** を呼び出して、SQL_ATTR_ODBC_VERSION 環境属性を SQL_OV_ODBC2 に設定します。  
  
-   **Sqlallocenv**、 **sqlallocenv**、または**sqlallocenv**へのすべての呼び出しを、SQL_HANDLE_ENV、SQL_HANDLE_DBC、または SQL_HANDLE_STMT の適切な*Handletype*引数を使用して**SQLAllocHandle**への呼び出しで置き換えます。  
  
-   **Sqlfreeenv**または**SQLFreeConnect**のすべての呼び出しを、 **sqlfreeenv**の呼び出しと、SQL_HANDLE_DBC または SQL_HANDLE_STMT の適切な*handletype*引数を使用して置き換えます。  
  
-   **SQLSetConnectOption**のすべての呼び出しを**SQLSetConnectAttr**の呼び出しに置き換えます。 値が文字列である属性を設定する場合は、 *Stringlength* 引数を適切に設定します。 *属性*引数を SQL_XXXX から SQL_ATTR_XXXX に変更します。  
  
-   **SQLGetConnectOption**のすべての呼び出しを**Sqlgetconnectattr**の呼び出しに置き換えます。 文字列属性またはバイナリ属性を取得する場合は、 *Bufferlength* に適切な値を設定し、 *stringlength* 引数を渡します。 *属性*引数を SQL_XXXX から SQL_ATTR_XXXX に変更します。  
  
-   **SQLSetStmtOption**のすべての呼び出しを**SQLSetStmtAttr**の呼び出しに置き換えます。 値が文字列である属性を設定する場合は、 *Stringlength* 引数を適切に設定します。 *属性*引数を SQL_XXXX から SQL_ATTR_XXXX に変更します。  
  
-   **SQLGetStmtOption**のすべての呼び出しを**SQLGetStmtAttr**の呼び出しに置き換えます。 文字列属性またはバイナリ属性を取得する場合は、 *Bufferlength* に適切な値を設定し、 *stringlength* 引数を渡します。 *属性*引数を SQL_XXXX から SQL_ATTR_XXXX に変更します。  
  
-   **Sqltransact**のすべての呼び出しを**SQLEndTran**への呼び出しに置き換えます。 **Sqltransact**呼び出し内の右端の有効なハンドルが環境ハンドルの場合は、適切な*ハンドル*引数を使用して、SQL_HANDLE_ENV の*handletype*引数を**SQLEndTran**呼び出しで使用する必要があります。 **Sqltransact**呼び出し内の右端の有効なハンドルが接続ハンドルの場合は、適切な*ハンドル*引数を使用して、SQL_HANDLE_DBC の*handletype*引数を**SQLEndTran**呼び出しで使用する必要があります。  
  
-   **Sqlcolattributes**のすべての呼び出しを**sqlcolattributes**の呼び出しに置き換えます。 *FieldIdentifier*引数が SQL_COLUMN_PRECISION、SQL_COLUMN_SCALE、または SQL_COLUMN_LENGTH のいずれかである場合は、関数の名前以外を変更しないでください。 それ以外の場合は、 *FieldIdentifier* を SQL_COLUMN_XXXX から SQL_DESC_XXXX に変更します。 場合 *FieldIdentifier* が SQL_DESC_CONCISE_TYPE、データ型が datetime データ型の場合は、対応する ODBC *3. x* データ型に変更します。  
  
-   ブロックカーソル、スクロール可能なカーソル、またはその両方を使用する場合、アプリケーションは次のことを行います。  
  
    -   **SQLSetStmtAttr**を使用して、行セットのサイズ、カーソルの種類、およびカーソルの同時実行を設定します。  
  
    -   **SQLSetStmtAttr**を呼び出して、ステータスレコードの配列を指すように SQL_ATTR_ROW_STATUS_PTR を設定します。  
  
    -   **SQLSetStmtAttr**を呼び出して、SQLINTEGER を指すように SQL_ATTR_ROWS_FETCHED_PTR を設定します。  
  
    -   必要なバインドを実行し、SQL ステートメントを実行します。  
  
    -   ループ内で **Sqlfetchscroll** を呼び出して、行をフェッチし、結果セット内を移動します。  
  
    -   ブックマークによってフェッチする場合、アプリケーションは**SQLSetStmtAttr**を呼び出して、フェッチする行のブックマークを格納する変数に SQL_ATTR_FETCH_BOOKMARK_PTR を設定し、SQL_FETCH_BOOKMARK の*fetchorientation*引数を使用して**sqlfetchscroll**を呼び出します。  
  
-   パラメーターの配列を使用する場合、アプリケーションは次のことを行います。  
  
    -   **SQLSetStmtAttr**を呼び出して、パラメーター配列のサイズに SQL_ATTR_PARAMSET_SIZE 属性を設定します。  
  
    -   **SQLSetStmtAttr**を呼び出して、内部 udword 変数を指すように SQL_ATTR_ROWS_PROCESSED_PTR を設定します。  
  
    -   必要に応じて、準備、バインド、および実行の各操作を実行します。  
  
    -   何らかの理由 (SQL_NEED_DATA など) で実行が停止した場合、SQL_ATTR_ROWS_PROCESSED_PTR が指す位置を調べることによって、パラメーターの "現在の" 行を見つけることができます。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [アプリケーションの旧バージョンとの互換性のためのマッピング置換関数](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [SQLCloseCursor の呼び出し](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [SQLGetDiagField の呼び出し](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [SQLSetPos の呼び出し](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [カーソル ライブラリの操作](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [Cursor Attributes1 の情報の種類のマッピング](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)
