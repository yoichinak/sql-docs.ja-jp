---
description: SQL_C_TCHAR
title: SQL_C_TCHAR |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- sql_c_tchar [ODBC]
- pseudo-type identifiers [ODBC], SQL_C_TCHAR
- data types [ODBC], pseudo-type identifiers
ms.assetid: 9e27c8bd-ee15-4ce9-b70a-34cf1bf16f4c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a399570a15f04d8ace61664a445c5283d629bf6a
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99193043"
---
# <a name="sql_c_tchar"></a>SQL_C_TCHAR
SQL_C_TCHAR 型識別子は実際にはデータ型を識別しません。これは、Unicode 変換のヘッダーファイル内に存在するマクロです。 UNICODE **#define** の設定によっては、SQL_C_CHAR または SQL_C_WCHAR に置き換えられます。 ANSI と Unicode の両方のアプリケーションとしてコンパイルされた文字データをアプリケーションが転送する場合に便利です。
