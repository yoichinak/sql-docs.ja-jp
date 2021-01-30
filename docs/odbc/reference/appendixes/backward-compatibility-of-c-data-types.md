---
description: C データ型の下位互換性
title: C データ型の旧バージョンとの互換性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- backward compatibility [ODBC], C data types
- compatibility [ODBC], C data types
- data types [ODBC], backward compatibility
- C data types [ODBC], backward compatibility
ms.assetid: b1453a65-ae03-4061-b0cf-a8434d8bc40b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 75ea0c53091faaece23f9d7316c9a6f242677a41
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99212512"
---
# <a name="backward-compatibility-of-c-data-types"></a>C データ型の下位互換性
SQL_C_SHORT、SQL_C_LONG、および SQL_C_TINYINT は、符号付きおよび符号なしの型によって ODBC で置き換えられました。 SQL_C_SSHORT と SQL_C_USHORT、SQL_C_SLONG と SQL_C_ULONG、および SQL_C_STINYINT と SQL_C_UTINYINT です。 ODBC 2.x アプリケーションで動作する ODBC *3.x ドライバーは* 、SQL_C_SHORT、SQL_C_LONG、および SQL_C_TINYINT をサポートする必要が *あります。* これらが呼び出されると、ドライバーマネージャーによってドライバーに渡されます。
