---
description: レベル 2 API 関数 (ODBC Driver for Oracle)
title: レベル2の API 関数 (ODBC Driver for Oracle) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC level 2 API functions [ODBC]
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- ODBC API functions [ODBC]
- API functions [ODBC]
- level 2 API functions [ODBC]
ms.assetid: d9f49520-72d7-4234-8635-260d0ce4199c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bd7e8955ecc0b6e4a82b4468509518ccee9732ad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483535"
---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>レベル 2 API 関数 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用してください。  
  
 このレベルの関数は、レベル1のインターフェイスの準拠に加えて、ブックマークのサポート、動的パラメーター、ODBC 関数の非同期実行などの追加機能を提供します。  
  
|API 関数|ノート|  
|------------------|-----------|  
|**SQLBindParameter**|SQL ステートメントのパラメーターマーカーにバッファーを関連付けます。|  
|**SQLBrowseConnect**|属性と属性値の連続するレベルを返します。|  
|**SQLDataSources**|データソース名を一覧表示します。 ドライバーマネージャーによって実装されます。|  
|**SQLDescribeParam**|準備された SQL ステートメントに関連付けられているパラメーターマーカーの説明を返します。<br /><br /> ステートメントの解析に基づいて、パラメーターがどのようなものかを最も推測したものを返します。 パラメーターの型を特定できない場合、SQL_VARCHAR は長さが2000で返されます。|  
|**SQLDrivers**|ドライバーマネージャーによって実装されます。|  
|**SQLExtendedFetch**|**Sqlfetch**に似ていますが、各列に配列を使用して複数の行を返します。 結果セットは順方向スクロール可能であり、カーソルが順方向専用ではなく静的に定義されている場合は、後方スクロール可能にすることができます。 既定の列バインドを持つ順方向専用カーソルの場合、BUFFERSIZE 接続属性を超えるデータセットの列データは、データバッファーに直接フェッチされます。 では、可変長のブックマークはサポートされません。また、ブックマークからのオフセット (0 以外) での行セットのフェッチはサポートされていません。|  
|**SQLForeignKeys**|1つのテーブル内の外部キーの一覧、または1つのテーブルを参照する他のテーブル内の外部キーの一覧を返します。|  
|**SQLMoreResults**|ステートメントハンドル、hstmt、および SELECT、UPDATE、INSERT、または DELETE の各ステートメントに対してより多くの結果が保留されているかどうかを判断し、存在する場合は、それらの結果の処理を初期化します。<br /><br /> Oracle では、{resultset...} エスケープシーケンスを使用する場合、ストアドプロシージャからの複数の結果セットのみがサポートされます。|  
|**SQLNativeSql**|使用方法の詳細については、「 [ストアドプロシージャから配列パラメーターを返す](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)」を参照してください。|  
|**SQLNumParams**|SQL ステートメント内のパラメーターの数を返します。 パラメーターの数は、 **SQLPrepare**に渡される SQL ステートメントの疑問符の数と同じである必要があります。|  
|**SQLPrimaryKeys**|テーブルの主キーを構成する列名を返します。|  
|**SQLProcedureColumns**|入力パラメーターと出力パラメーター、戻り値、1つのプロシージャの結果セット内の列、および2つの追加の列、オーバーロード、および ORDINAL_POSITION の一覧を返します。 オーバーロードは、Oracle データディクショナリビューの ALL_ARGUMENTS テーブルのオーバーロード列です。 ORDINAL_POSITION は、Oracle データディクショナリビューの ALL_ARGUMENTS テーブルのシーケンス列です。 パッケージ化されたプロシージャの場合、[プロシージャ名] 列は *packagename* 形式で指定します。 は、プロシージャまたは関数を参照する作成されたシノニムのプロシージャ列を返しません。|  
|**SQLProcedures**|データソース内のプロシージャの一覧を返します。 パッケージ化されたプロシージャの場合、[プロシージャ名] 列は *packagename* 形式で指定します。<br /><br /> Oracle ではパッケージ化されたプロシージャとパッケージ化された関数を区別できないため、ドライバーは PROCEDURE_TYPE 列に対して SQL_PT_UNKNOWN を返します。|  
|**SQLSetPos**|行セット内のカーソル位置を設定します。 **SQLSetPos**を**SQLGetData**と共に使用すると、行セット内の特定の行にカーソルを配置した後に、バインドされていない列から行を取得できます。 結果セットに追加された行は、 *Foption* SQL_ADD を使用して、結果セットの最後の行の後に追加されます。|  
|**SQLSetScrollOptions**|ステートメントハンドルの hstmt に関連付けられているカーソルの動作を制御するオプションを設定します。 詳細については、「 [カーソルの種類と同時実行の組み合わせ](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)」を参照してください。|
