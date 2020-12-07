---
description: レベル 1 API 関数 (ODBC Driver for Oracle)
title: レベル1の API 関数 (ODBC Driver for Oracle) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC level 1 API functions [ODBC]
- ODBC driver for Oracle [ODBC], functions
- level 1 API functions [ODBC]
- API functions [ODBC]
ms.assetid: 98cced6f-41b8-43c1-a3cd-f4ea1615c0af
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c82ab0f481fbc60d0308895640371e84886e77e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483545"
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>レベル 1 API 関数 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用してください。  
  
 このレベルの関数は、コアインターフェイスの準拠に加えて、トランザクションサポートなどの追加機能を提供します。  
  
|API 関数|ノート|  
|------------------|-----------|  
|**SQLColumns**|指定されたテーブルの列リストであるテーブルの結果セットを作成します。 パブリックシノニムの列を要求する場合は、SYNONYMCOLUMNS 接続属性を設定し、 *Sztableowner* 引数として空の文字列を指定する必要があります。 パブリックシノニムの列を返す場合、ドライバーはテーブル名列を空の文字列に設定します。 結果セットには、各行の末尾に位置を示す追加の列が含まれています。 この値は、テーブル内の列の序数位置です。|  
|**SQLDriverConnect**|既存のデータソースに接続します。 詳細については、「 [接続文字列の形式と属性](../../odbc/microsoft/connection-string-format-and-attributes.md)」を参照してください。|  
|**SQLGetConnectOption**|接続オプションの現在の設定を返します。 この関数は部分的にサポートされています。 ドライバーは*foption*引数のすべての値をサポートしますが、 *foption*引数[SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md)の一部の*vparam*値をサポートしていません。 詳細については、「 [Connect Options](../../odbc/microsoft/connect-options.md)」を参照してください。|  
|**SQLGetData**|指定された結果セットの現在のレコード内の1つのフィールドの値を取得します。|  
|**SQLGetFunctions**|サポートされているすべての関数に対して TRUE を返します。 ドライバーマネージャーによって実装されます。|  
|**SQLGetInfo**|\*ODBC Driver For Oracle および接続ハンドル*hdbc*に関連付けられているデータソースについて、SQLHDBC、sqlus悪意のある SQLPOINTER、SQLSMALLINT、sqlsmallint などの情報を返します。|  
|**SQLGetStmtOption**|ステートメントオプションの現在の設定を返します。 詳細については、「 [ステートメントオプション](../../odbc/microsoft/statement-options.md)」を参照してください。|  
|**SQLGetTypeInfo**|データソースでサポートされているデータ型に関する情報を返します。 ドライバーは、SQL 結果セットの情報を返します。|  
|**SQLParamData**|ステートメントの実行時にパラメーターデータを指定するために、 **Sqlputdata** と組み合わせて使用されます。|  
|**SQLPutData**|ステートメントの実行時に、アプリケーションからドライバーにパラメーターまたは列のデータを送信できるようにします。|  
|**SQLSetConnectOption**|接続の側面を制御するオプションへのアクセスを提供します。 この関数は部分的にサポートされています。ドライバーは*foption*引数のすべての値をサポートしていますが、 *foption*引数[SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md)の一部の*vparam*値をサポートしていません。 詳細については、「 [Connect Options](../../odbc/microsoft/connect-options.md)」を参照してください。|  
|**SQLSetStmtOption**|ステートメントハンドルの *hstmt*に関連するオプションを設定します。 詳細については、「 [ステートメントオプション](../../odbc/microsoft/statement-options.md)」を参照してください。|  
|**SQLSpecialColumns**|テーブル内の行を一意に識別する最適な列のセットを取得します。|  
|**SQLStatistics**|テーブルに関連付けられた1つのテーブルとインデックス (またはタグ名) に関する統計の一覧を取得します。 ドライバーは、結果セットとして情報を返します。|  
|**SQLTables**|**Sqltables**ステートメント内のパラメーターによって指定されたテーブル名の一覧を返します。 パラメーターが指定されていない場合は、現在のデータソースに格納されているテーブル名を返します。 ドライバーは、結果セットとして情報を返します。<br /><br /> 列挙型の呼び出しは、リモートビューまたはローカルのパラメーター化されたビューに対して結果セットのエントリを受け取りません。 ただし、一意のテーブル名指定子を使用して **Sqltables** を呼び出すと、そのようなビューの一致が検出されます (存在する場合)。これにより、API は、新しいテーブルを作成する前に名前の競合を確認できます。<br /><br /> パブリックシノニムは、TABLE_OWNER 値が "" で返されます。<br /><br /> SYS または SYSTEM が所有するビューは、システムビューとして識別されます。|
