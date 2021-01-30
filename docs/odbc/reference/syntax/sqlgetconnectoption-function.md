---
description: SQLGetConnectOption 関数
title: SQLGetConnectOption 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectOption
helpviewer_keywords:
- SQLGetConnectOption function [ODBC]
ms.assetid: 59cde899-7957-4b5e-8677-f34d3b859bfd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f518915bb9813fd6d0c17e1b37f436ae4379e12d
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99203412"
---
# <a name="sqlgetconnectoption-function"></a>SQLGetConnectOption 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: 非推奨  
  
 **要約**  
 *Odbc 3.x では、* odbc 2.X 関数 **SQLGetConnectOption** が **sqlgetconnectattr** に置き換えられまし *た。* 詳細については、「 [Sqlgetconnectattr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)」を参照してください。  
  
> [!NOTE]
>  *Odbc 2.x アプリケーションが* odbc *2.x ドライバーで* 動作しているときに、ドライバーマネージャーがこの機能をマップする方法の詳細については、「付録 G: 旧バージョンとの互換性のためのドライバーガイドライン」の「[非推奨の関数のマッピング](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)」を参照してください。  
> 
> [!NOTE]
>  ODBC 3.8 で導入された属性 SQL_ASYNC_DBC_FUNCTION_ENABLE は、 **SQLGetConnectOption** ではサポートされていません。 接続ハンドルで非同期操作を使用するアプリケーションでは、 **Sqlgetconnectattr** を使用する必要があります。  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
