---
description: Cursor Attributes1 の情報の種類のマッピング
title: Cursor Attributes1 Information Types | をマップするMicrosoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], mapping cursor attributes1 information types
- application upgrades [ODBC], mapping cursor attributes1 information types
- mapping cursor attributes1 information types [ODBC]
- backward compatibility [ODBC], mapping cursor attributes1 information types
- upgrading applications [ODBC], mapping cursor attributes1 information types
ms.assetid: 9f112449-ca86-45ac-a865-e6174d67f91b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fcd4c1eaa6ddd2e6db4f2634cc22d3148e7977cf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461404"
---
# <a name="mapping-the-cursor-attributes1-information-types"></a>Cursor Attributes1 の情報の種類のマッピング
ODBC 3 の場合。*x* アプリケーションは、SQL_XXXX_CURSOR_ATTRIBUTES1 情報の種類 (動的、順方向専用、キーセット、または静的カーソル用) を使用して、odbc 2.x ドライバーの **SQLGetInfo** を呼び出し*ます。ドライバー* マネージャーによって返されるビットの設定は、odbc 2 によって異なります。*x* ドライバーは、対応する ODBC 2 に対してを返します。*x* 情報の種類。 ビットは、次の表に示すように設定されます。  
  
|Bit in<br /><br /> SQL_XXXX_CURSOR_ATTRIBUTES1|カーソルの種類|ODBC 2.*x* 情報<br /><br /> type|  
|-----------------------------------------------|-----------------|-------------------------------------|  
|SQL_CA1_NEXT|All|SQL_FETCH_DIRECTION|  
|SQL_CA1_ABSOLUTE SQL_CA1_RELATIVE SQL_CA1_BOOKMARK|Dynamic、keyset-driver、static|SQL_FETCH_DIRECTION|  
|SQL_CA1_LOCK_NO_CHANGE SQL_CA1_LOCK_UNLOCK SQL_CA1_LOCK_EXCLUSIVE|Dynamic、keyset-driver、static|SQL_LOCK_TYPES|  
|SQL_CA1_POSITIONED_UPDATE SQL_CA1_POSITIONED_DELETE SQL_CA1_SELECT_FOR_UPDATE|All|SQL_POSITIONED_STATEMENTS|  
|SQL_CA1_POS_POSITION SQL_CA1_POS_DELETE SQL_CA1_POS_REFRESH SQL_CA1_POS_BULK_ADD|Dynamic、keyset-driver、static|SQL_POS_OPERATIONS|
