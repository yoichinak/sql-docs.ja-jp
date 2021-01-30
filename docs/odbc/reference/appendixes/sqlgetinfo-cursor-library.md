---
description: SQLGetInfo (カーソル ライブラリ)
title: SQLGetInfo (カーソルライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- SQLGetInfo function [ODBC], Cursor Library
ms.assetid: 1b4d220d-2c07-4f56-987e-36813bb1a6ce
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9fc11d16d145a37db4fdc50ad7f9907532fe747c
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99202756"
---
# <a name="sqlgetinfo-cursor-library"></a>SQLGetInfo (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックでは、カーソルライブラリで **SQLGetInfo** 関数を使用する方法について説明します。 **Sqlgetinfo** に関する一般的な情報については、「 [sqlgetinfo 関数](../../../odbc/reference/syntax/sqlgetinfo-function.md)」を参照してください。  
  
 カーソルライブラリは、 *InfoType* の次の値の値を返します (&#124; はビットごとの or を表します)。 *InfoType* のその他のすべての値については、ドライバーで **SQLGetInfo** を呼び出します。  
  
|*InfoType*|戻り値|  
|----------------|--------------------|  
|SQL_BOOKMARK_PERSISTENCE|SQL_BP_SCROLL|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|0|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|0|  
|SQL_FETCH_DIRECTION [1]|SQL_FD_FETCH_ABSOLUTE &#124; SQL_FD_FETCH_FIRST &#124; SQL_FD_FETCH_LAST &#124; SQL_FD_FETCH_NEXT &#124; SQL_FD_FETCH_PRIOR &#124; SQL_FD_FETCH_RELATIVE &#124; SQL_FD_FETCH_BOOKMARK|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|SQL_CA1_NEXT &#124; SQL_CA1_ABSOLUTE &#124; SQL_CA1_RELATIVE &#124; SQL_CA1_LOCK_NO_CHANGE &#124; SQL_CA1_POS_POSITION &#124; SQL_CA1_POSITIONED_DELETE &#124; SQL_CA1_POSITIONED_UPDATE &#124; SQL_CA1_SELECT_FOR_UPDATE|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|SQL_CA2_READ_ONLY_CONCUR &#124; SQL_CA2_OPT_VALUES_CONCURRENCY &#124; SQL_CA2_SENSITIVITY_UPDATES|  
|SQL_GETDATA_EXTENSIONS|ドライバーによって返されるすべての値 &#124; SQL_GD_BLOCK **:** **sqlfetchscroll** を使用してデータを取得すると、 **SQLGetData** は、SQL_GD_ANY_COLUMN と SQL_GD_BOUND ビットマスクで指定された機能をサポートします。|  
|SQL_KEYSET_DRIVEN_CURSOR_ATTRIBUTES1|0|  
|SQL_KEYSET_DRIVEN_CURSOR_ATTRIBUTES2|0|  
|SQL_LOCK_TYPES [1]|SQL_LCK_NO_CHANGE|  
|SQL_STATIC_CURSOR_ATTRIBUTES1|SQL_CA1_NEXT &#124; SQL_CA1_ABSOLUTE &#124; SQL_CA1_RELATIVE &#124; SQL_CA1_BOOKMARK &#124; SQL_CA1_LOCK_NO_CHANGE &#124; SQL_CA1_POS_POSITION &#124; SQL_CA1_POSITIONED_DELETE &#124; SQL_CA1_POSITIONED_UPDATE &#124; SQL_CA1_SELECT_FOR_UPDATE|  
|SQL_STATIC_CURSOR_ATTRIBUTES2|SQL_CA2_READ_ONLY_CONCUR &#124; SQL_CA2_OPT_VALUES_ 同時実行 &#124; SQL_CA2_SENSITIVITY_UPDATES|  
|SQL_POS_OPERATIONS [1]|SQL_POS_POSITION|  
|SQL_POSITIONED_STATEMENTS [1]|SQL_PS_POSITIONED_DELETE &#124; SQL_PS_POSITIONED_UPDATE &#124; SQL_PS_SELECT_FOR_UPDATE|  
|SQL_ROW_UPDATES|"Y"|  
|SQL_SCROLL_CONCURRENCY [1]|SQL_SCCO_READ_ONLY &#124; SQL_SCCO_OPT_VALUES|  
|SQL_SCROLL_OPTIONS|SQL_SO_FORWARD_ONLY &#124; SQL_SO_STATIC|  
|SQL_STATIC_SENSITIVITY [1]|SQL_SS_UPDATES|  
  
 [1] カーソルライブラリが ODBC 2.x ドライバーで使用されている場合にのみ使用されます。  
  
> [!IMPORTANT]  
>  トランザクションがデータソースとしてコミットまたはロールバックされる場合、カーソルライブラリは同じカーソル動作を実装します。 つまり、 **SQLEndTran** を呼び出すか SQL_ATTR_AUTOCOMMIT 接続属性を使用して、トランザクションをコミットまたはロールバックすると、データソースによってアクセスプランが削除され、接続上のすべてのステートメントのカーソルが閉じられる可能性があります。 詳細については、「 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)」の SQL_CURSOR_COMMIT_BEHAVIOR と SQL_CURSOR_ROLLBACK_BEHAVIOR の情報の種類を参照してください。
