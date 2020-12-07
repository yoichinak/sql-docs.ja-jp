---
description: 非推奨の関数のマッピング
title: 非推奨の関数のマッピング |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], about mapping deprecated functions
- backward compatibility [ODBC], mapping deprecated functions
- deprecated functions [ODBC]
- compatibility [ODBC], mapping deprecated functions
- functions [ODBC], mapping deprecated functions
- mapping deprecated functions [ODBC]
ms.assetid: ee462617-1d79-4c88-afeb-b129cff34cc6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9c990646c54fd0d0698482c5f8dc3f87df80fe93
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429614"
---
# <a name="mapping-deprecated-functions"></a>非推奨の関数のマッピング
このセクションでは、odbc 2.x アプリケーションで使用される ODBC *3.x ドライバーの*旧バージョンとの互換性を保証するために、非推奨の関数*が Odbc* *3.x ドライバーマネージャー*によってどのようにマップされるかについて説明します。 ドライバーマネージャーは、アプリケーションのバージョンに関係なく、このマッピングを実行します。 次の一覧に示す*odbc 2.x 関数は*それぞれ *、odbc 3.x ドライバーで*呼び出された場合に対応する odbc 3.x 関数にマップされるため *、ODBC 3.x ドライバーで**は odbc* *2.x 関数を*実装する必要はありません。  
  
 ドライバー *が ODBC 3.x* ドライバーであり、ドライバーがマップされている関数をサポートしていない場合、一覧内のマッピングがトリガーされます。  
  
 次の表は、ODBC *3. x*で導入されたすべての重複機能を示しています。  
  
|ODBC *2.x* 関数|ODBC *3.x* 関数|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**SQLBindParam**[1]|**SQLBindParameter**|  
|**SQLColAttributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|SQL_DROP の*オプション*を使用した**SQLFreeStmt**|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**[2]|**SQLBindParameter**|  
|**SQLSetScrollOption**|**SQLSetStmtAttr**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] この関数が ODBC 2.x に存在しなかった場合で *も、オープン*グループおよび ISO 標準になっています。  
  
 [2] ODBC 1.0 関数です。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [SQLAllocConnect のマッピング](../../../odbc/reference/appendixes/sqlallocconnect-mapping.md)  
  
-   [SQLAllocEnv のマッピング](../../../odbc/reference/appendixes/sqlallocenv-mapping.md)  
  
-   [SQLAllocStmt のマッピング](../../../odbc/reference/appendixes/sqlallocstmt-mapping.md)  
  
-   [SQLBindParam のマッピング](../../../odbc/reference/appendixes/sqlbindparam-mapping.md)  
  
-   [SQLColAttributes のマッピング](../../../odbc/reference/appendixes/sqlcolattributes-mapping.md)  
  
-   [SQLError のマッピング](../../../odbc/reference/appendixes/sqlerror-mapping.md)  
  
-   [SQLFreeConnect のマッピング](../../../odbc/reference/appendixes/sqlfreeconnect-mapping.md)  
  
-   [SQLFreeEnv のマッピング](../../../odbc/reference/appendixes/sqlfreeenv-mapping.md)  
  
-   [SQLFreeStmt のマッピング](../../../odbc/reference/appendixes/sqlfreestmt-mapping.md)  
  
-   [SQLGetConnectOption のマッピング](../../../odbc/reference/appendixes/sqlgetconnectoption-mapping.md)  
  
-   [SQLGetStmtOption のマッピング](../../../odbc/reference/appendixes/sqlgetstmtoption-mapping.md)  
  
-   [SQLInstallTranslator のマッピング](../../../odbc/reference/appendixes/sqlinstalltranslator-mapping.md)  
  
-   [SQLParamOptions のマッピング](../../../odbc/reference/appendixes/sqlparamoptions-mapping.md)  
  
-   [SQLSetConnectOption のマッピング](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)  
  
-   [SQLSetParam のマッピング](../../../odbc/reference/appendixes/sqlsetparam-mapping.md)  
  
-   [SQLSetScrollOptions のマッピング](../../../odbc/reference/appendixes/sqlsetscrolloptions-mapping.md)  
  
-   [SQLSetStmtOption のマッピング](../../../odbc/reference/appendixes/sqlsetstmtoption-mapping.md)  
  
-   [SQLTransact のマッピング](../../../odbc/reference/appendixes/sqltransact-mapping.md)
