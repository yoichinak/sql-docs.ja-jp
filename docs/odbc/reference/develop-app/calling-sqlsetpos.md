---
description: SQLSetPos の呼び出し
title: SQLSetPos | を呼び出していますMicrosoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], calling
- upgrading applications [ODBC], SQLSetPos
- backward compatibility [ODBC], SqlSetPos
- application upgrades [ODBC], SQLSetPos
ms.assetid: 846354b8-966c-4c2c-b32f-b0c8e649cedd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ecb1708b6d5fe9877ab647b11488131645e56690
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494713"
---
# <a name="calling-sqlsetpos"></a>SQLSetPos の呼び出し
*ODBC 2.x では、行*状態配列へのポインターは**SQLExtendedFetch**の引数でした。 行の状態の配列は、 **SQLSetPos**の呼び出しによって後で更新されました。 一部のドライバーでは、 **SQLExtendedFetch** と **SQLSetPos**の間でこの配列が変更されないという事実に依存しています。 *ODBC 3.x では、状態*配列へのポインターは記述子フィールドであるため、アプリケーションは簡単に別の配列を指すように変更できます。 ODBC *2.x アプリケーションが* odbc *2.x ドライバーを* 使用しているときに、 **SQLSetStmtAttr** を呼び出して配列の状態ポインターを設定し、データをフェッチするために **sqlfetchscroll** を呼び出している場合に、この問題が発生することがあります。 ドライバーマネージャーは、 **SQLExtendedFetch**への一連の呼び出しとしてそれをマップします。 次のコードでは、通常、ODBC 2.x ドライバーを操作するときに Driver Manager が2番目の**SQLSetStmtAttr**呼び出しをマップすると、エラーが発生*します。*  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStatus, 0);  
SQLFetchScroll(hstmt, fFetchType, iRow);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStat1, 0);  
SQLSetPos(hstmt, iRow, fOption, fLock);  
```  
  
 ODBC 2.x の行ステータスポインターを**SQLExtendedFetch**の呼び出し*間で変更*する方法がない場合、エラーが発生します。 代わりに、ドライバーマネージャーは、ODBC 2.x ドライバーを使用するときに次の手順を実行*します。*  
  
1.  内部ドライバーマネージャーフラグ *fSetPosError* を TRUE に初期化します。  
  
2.  アプリケーションが **Sqlfetchscroll**を呼び出すと、ドライバーマネージャーは *fSetPosError* を FALSE に設定します。  
  
3.  アプリケーションが SQL_ATTR_ROW_STATUS_PTR を設定するために **SQLSetStmtAttr** を呼び出すと、ドライバーマネージャーは *FSetPosError* equal totrue を設定します。  
  
4.  アプリケーションが**sqlsetpos**を呼び出し、 *fSetPosError*が TRUE の場合、ドライバーマネージャーは SQLSTATE HY011 (属性を設定できません) を使用して SQL_ERROR を発生させ、アプリケーションが行ステータスポインターを変更した後、 **sqlfetchscroll**を呼び出す前に**sqlsetpos**を呼び出そうとしたことを示します。
