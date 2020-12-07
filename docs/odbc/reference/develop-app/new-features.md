---
description: 新機能
title: 新機能 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], new features in release
- ODBC drivers [ODBC], backward compatibility
- new features [ODBC]
- compatibility [ODBC], new features in release
- ODBC [ODBC], new features
ms.assetid: a8fcdd00-6cb3-4871-9489-6018b3d0d65f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2015d424e0c755352fa66f3ac67503b612b6982f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429234"
---
# <a name="new-features"></a>新機能
ODBC 3.x では、次の新機能が導入されまし*た。* *Odbc 2.x アプリケーションで*odbc 2.x ドライバーを操作すると、この機能を使用できなく*なります。* *Odbc 2.x* driver Manager では *、odbc 2.x*ドライバーを使用する場合、これらの機能はマップされません。  
  
-   記述子ハンドルを引数として受け取る関数: **SQLSetDescField**、 **SQLGetDescField**、 **SQLSetDescRec**、 **Sqlgetdescrec**、および **sqlcopydesc**。  
  
-   関数 **SQLSetEnvAttr** と **SQLGetEnvAttr**。  
  
-   **SQLAllocHandle**を使用して記述子ハンドルを割り当てます。 ( **SQLAllocHandle** を使用して環境、接続、およびステートメントハンドルを割り当てることは、新機能ではなく複製されています)。  
  
-   **Sqlgetconnectattr**を使用して、SQL_ATTR_AUTO_IPD 接続属性を取得します。 ( **SQLSetConnectAttr** を設定し、 **Sqlgetconnectattr** を取得するために使用します。その他の接続属性は重複していますが、新機能ではありません)。  
  
-   **SQLSetStmtAttr**を使用して、次のステートメント属性を設定し、 **SQLGetStmtAttr**を取得します。 ( **SQLSetStmtAttr** を使用してを設定し、 **SQLGetStmtAttr** を取得するために、新しい機能ではなく、他のステートメント属性が複製されています)。  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_ENABLE_AUTO_IPD  
  
     SQL_ATTR_FETCH_BOOKMARK_PTR  
  
     SQL_ATTR_BIND_OFFSET  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     SQL_DESC_PARAM_STATUS_PTR  
  
     SQL_ATTR_PARAMS_PROCESSED_PTR  
  
     SQL_ATTR_PARAMSET_SIZE  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_ROW_ARRAY_SIZE  
  
-   **SQLGetStmtAttr**を使用して、次のステートメント属性を取得します。 ( **SQLGetStmtAttr** を使用して他のステートメント属性を取得することは、新機能ではなく、重複する機能です)。  
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   Interval C データ型、interval SQL データ型、BIGINT C データ型、および SQL_C_NUMERIC データ構造体の使用。  
  
-   パラメーターの行方向のバインド。  
  
-   オフセットベースのブックマークをフェッチします。たとえば、SQL_FETCH_BOOKMARK の*Fetchorientation*引数を使用して**sqlfetchscroll**を呼び出し、0以外のオフセットを指定します。  
  
-   **Sqlfetch** は、行の状態の配列、フェッチされた行数を返します。複数の行をフェッチし、 **sqlfetchscroll**を使用して混在させ呼び出しを、 **Sqlbulkoperations** または **SQLSetPos**を使用して混在させを呼び出します。 詳細については、次のセクション、 [ブロックカーソル、スクロール可能なカーソル、および ODBC 3. x アプリケーションの旧バージョンとの互換性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)に関するセクションを参照してください。  
  
-   名前付きパラメーター。  
  
-   ODBC *3. x*固有の **SQLGetInfo** オプションのいずれか。 ( *Odbc 2.x アプリケーションが* *odbc 2.x ドライバーを* 使用して動作している場合、いくつかの odbc *2.* x 情報の種類に置き換えられた SQL_XXX_CURSOR_ATTRIBUTES1 情報の種類を呼び出すと、一部の情報が信頼できるようになりますが、信頼性が低い場合があります。 詳細については、「 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)」を参照してください。)  
  
-   オフセットをバインドします。  
  
-   ( **Sqlbulkoperations**を呼び出すことによって) ブックマークによる更新、更新、および削除。  
  
-   S5 状態の **Sqlbulkoperations** または **SQLSetPos** を呼び出しています。  
  
-   診断レコードの ROW_NUMBER および COLUMN_NUMBER フィールド (置換関数 **SQLGetDiagField** または **SQLGetDiagRec**によって取得される必要があります)。  
  
-   おおよその行数。  
  
-   警告情報 ( **Sqlfetchscroll**からの SQL_ROW_SUCCESS_WITH_INFO)。  
  
-   可変長のブックマーク。  
  
-   パラメーターの配列の拡張エラー情報。  
  
-   カタログ関数によって返される結果セット内のすべての新しい列。  
  
-   列0で **SQLDescribeCol** と **sqlcolattribute** を使用します。  
  
-   **Sqlcolattribute**の呼び出しでの ODBC *3. x*固有の列属性の使用。  
  
-   複数の環境ハンドルの使用。  
  
 ここでは、次のトピックについて説明します。  
  
-   [ODBC 3.x アプリケーション用のブロック カーソル、スクロール可能なカーソル、および下位互換性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
