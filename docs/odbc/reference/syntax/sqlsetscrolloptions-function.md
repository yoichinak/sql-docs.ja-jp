---
description: SQLSetScrollOptions 関数
title: SQLSetScrollOptions 関数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLSetScrollOptions
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetScrollOptions
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC]
ms.assetid: 2a825ba7-7942-4c23-bcdb-c80dc12f8c86
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69e592350680b4cf3244df823324fb85b8d6153e
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99188024"
---
# <a name="sqlsetscrolloptions-function"></a>SQLSetScrollOptions 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: 非推奨  
  
 **要約**  
 ODBC 3.x では、ODBC 2.0 関数 **SQLSetScrollOptions** は **SQLGetInfo** と **SQLSetStmtAttr** の呼び出しに置き換えられてい *ます。*  
  
> [!NOTE]
>  *Odbc 2.x アプリケーションが* odbc *2.x ドライバーで* 動作しているときに、ドライバーマネージャーがこの機能をマップする方法の詳細については、「付録 G: 旧バージョンとの互換性のためのドライバーガイドライン」の「[非推奨の関数のマッピング](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)」を参照してください。  
> 
> [!NOTE]
>  ドライバーマネージャーが、 **SQLSetScrollOptions** をサポートしていない ODBC 3.x ドライバーを使用しているアプリケーションの **SQLSetScrollOptions** をマップする場合、ドライバーマネージャーは、 **SQLSetScrollOption** の *RowsetSize* 引数に、ステートメントの SQL_ATTR_ROW_ARRAY_SIZE の属性ではなく SQL_ROWSET_SIZE ステートメントオプションを設定 *します。* 結果として、 **Sqlfetch** または **sqlfetchscroll** の呼び出しによって複数の行をフェッチするときに、アプリケーションで **SQLSetScrollOptions** を使用することはできません。 **SQLExtendedFetch** の呼び出しによって複数の行をフェッチする場合にのみ使用できます。  
  
## <a name="remarks"></a>コメント  
 アプリケーションが64ビットオペレーティングシステムで実行される場合は、「 [ODBC 64 ビット情報](../../../odbc/reference/odbc-64-bit-information.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
