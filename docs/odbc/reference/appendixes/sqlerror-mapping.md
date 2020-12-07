---
description: SQLError のマッピング
title: SQLError マッピング |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLError
- SQLError function [ODBC], mapping
ms.assetid: 802ac711-7e5d-4152-9698-db0cafcf6047
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5d18d1b25acbbe56f29555274a7b8d995b7355d0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466024"
---
# <a name="sqlerror-mapping"></a>SQLError のマッピング
アプリケーション*が ODBC 3.x*ドライバーを使用して**SQLError**を呼び出す場合、  
  
```  
SQLError(henv, hdbc, hstmt, szSqlState, pfNativeError, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)   
```  
  
 がにマップされています  
  
```  
SQLGetDiagRec(HandleType, Handle, RecNumber, szSqlstate, pfNativeErrorPtr, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)  
```  
  
 *Handletype*引数を SQL_HANDLE_ENV の値に設定し、必要に応じて SQL_HANDLE_DBC または SQL_HANDLE_STMT を指定し、必要に応じて*henv*、 *hdbc*、または*hstmt*の値に設定されている*HANDLE*引数を使用します。 *Recnumber*引数は、ドライバーマネージャーによって決定されます。
