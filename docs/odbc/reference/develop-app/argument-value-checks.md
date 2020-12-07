---
description: 引数の値のチェック
title: 引数の値の確認 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- argument value checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 37a65f8b-83aa-456c-b7cf-500404abb38a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5dac29eea6c9a2b5f178aa233520674ea466cf48
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465954"
---
# <a name="argument-value-checks"></a>引数の値のチェック
ドライバーマネージャーは、次の種類の引数を確認します。 特に明記されていない限り、ドライバーマネージャーは引数値のエラーに対して SQL_ERROR を返します。  
  
-   通常、環境、接続、およびステートメントハンドルを null ポインターにすることはできません。 ドライバーマネージャーは、null ハンドルを検出すると SQL_INVALID_HANDLE を返します。  
  
-   **SQLAllocHandle**の*OutputHandlePtr*や**SQLSetCursorName**の*カーソル名*など、必要なポインター引数を null ポインターにすることはできません。  
  
-   ドライバー固有の値をサポートしていないオプションフラグは、有効な値である必要があります。 たとえば、 **SQLSetPos**の*操作*は、SQL_POSITION、SQL_REFRESH、SQL_UPDATE、SQL_DELETE、または SQL_ADD である必要があります。  
  
-   オプションフラグは、ドライバーでサポートされている ODBC のバージョンでサポートされている必要があります。 たとえば、 *InfoType* in **SQLGETINFO** は、odbc 2.0 ドライバーを呼び出すときに SQL_ASYNC_MODE (odbc 3.0 で導入) することはできません。  
  
-   列とパラメーターの数は、関数に応じて、0より大きいか0以上である必要があります。 ドライバーは、現在の結果セットまたは SQL ステートメントに基づいて、これらの引数値の上限を確認する必要があります。  
  
-   長さ/インジケーターの引数とデータバッファーの長さの引数には、適切な値が含まれている必要があります。 たとえば、 **Sqlcolumns** (*NameLength3*) のテーブル名の長さを指定する引数には SQL_NTS または0より大きい値を指定する必要があります。**SQLDescribeCol**の*bufferlength*には、0以上の値を指定する必要があります。 ドライバーは、これらの引数を確認する必要がある場合もあります。 たとえば、 *NameLength3* がデータソース内のテーブル名の最大長以下であることを確認できます。
