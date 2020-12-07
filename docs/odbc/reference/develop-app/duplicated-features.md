---
description: 重複する機能
title: 重複する特徴 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- duplicated functions [ODBC]
- compatibility [ODBC], duplicated functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], duplicated functions
- backward compatibility [ODBC], duplicated functions
ms.assetid: 641b16bc-f791-46d8-b093-31736473fe3d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0aa03482efbadc8dac2fa887deb0f01d9b167214
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483025"
---
# <a name="duplicated-features"></a>重複する機能
Odbc 3.x 関数によって、次*の odbc 2.x*関数*3.x*が複製されました。 その結果 *、odbc 2.x 関数は*odbc 3.x では非推奨とされ*ます。* ODBC *3. x* 関数は、置換関数と呼ばれます。  
  
 アプリケーションが非推奨の ODBC 2.x *関数を* 使用し、基になるドライバー *が odbc 3.x* ドライバーである場合、ドライバーマネージャーは関数呼び出しを対応する置換関数にマップします。 この規則の唯一の例外は **SQLExtendedFetch**です。 (次の表の最後にある脚注を参照してください)。これらのマッピングの詳細については、「付録 G: 旧バージョンとの互換性のためのドライバーガイドライン」の「 [非推奨の関数のマッピング](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) 」を参照してください。  
  
 アプリケーションが置換関数を使用し、基になるドライバー *が ODBC 2.x* ドライバーである場合、ドライバーマネージャーは関数呼び出しを対応する非推奨の関数にマップします。  
  
|ODBC *2.x* 関数|ODBC *3.x* 関数|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**SQLColAttributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**SQLExtendedFetch**[1]|**SQLFetchScroll**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**、 **SQLGetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**|**SQLBindParameter**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] 関数**SQLExtendedFetch**は重複しています。**Sqlfetchscroll**は ODBC 3.x と同じ機能を提供*します。* ただし *、ODBC 3.x*ドライバーに対して実行する場合、ドライバーマネージャーは**SQLExtendedFetch**を**sqlfetchscroll**にマップしません。 詳細については、「付録 G: ドライバー [マネージャー](../../../odbc/reference/appendixes/what-the-driver-manager-does.md) による旧バージョンとの互換性のためのドライバーガイドライン」を参照してください。 ドライバーマネージャーは *、ODBC 2.x*ドライバーに対して実行するときに**Sqlfetchscroll**を**SQLExtendedFetch**にマップします。  
  
> [!NOTE]
>  関数 **SQLBindParam** は特殊なケースです。 **SQLBindParam** の機能は重複しています。 これ *は ODBC 2.x* 関数ではなく、Open GROUP と ISO 標準に存在する関数です。 この関数によって提供される機能は、 **SQLBindParameter**の機能によって完全に包括されています。 その結果、ドライバーマネージャーは、基になるドライバーが ODBC 3.x ドライバーである場合に、 **SQLBindParam**への呼び出しを**SQLBindParameter**にマップ*します。* ただし、基に *なるドライバーが ODBC 2.x* ドライバーの場合、ドライバーマネージャーはこのマッピングを実行しません。
