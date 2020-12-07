---
description: SQLGetDescField および SQLGetDescRec (カーソル ライブラリ)
title: SQLGetDescField と SQLGetDescRec (カーソルライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetDescField function [ODBC], Cursor Library
- SQLGetDescRec function [ODBC], Cursor Library
ms.assetid: 1a801f22-6fea-48aa-a723-3187a2ad852b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f13b3ff5ed7e54a127089b74b5a45081900edf55
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494752"
---
# <a name="sqlgetdescfield-and-sqlgetdescrec-cursor-library"></a>SQLGetDescField および SQLGetDescRec (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックでは、カーソルライブラリで **SQLGetDescField** 関数と **Sqlgetdescrec** 関数を使用する方法について説明します。 これらの関数の一般的な情報については、「 [SQLGetDescField 関数](../../../odbc/reference/syntax/sqlgetdescfield-function.md) 」と「 [Sqlgetdescrec 関数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)」を参照してください。  
  
 カーソルライブラリは、 **Sqlgetdescrec** を実行してブックマーク列のメタデータを返します。 カーソルライブラリは **SQLGetDescField** を実行して、 **Sqlgetdescrec**によって返されるのと同じフィールドを返します。これは SQL_DESC_NAME、SQL_DESC_TYPE、SQL_DESC_DATETIME_INTERVAL_CODE、SQL_DESC_OCTET_LENGTH、SQL_DESC_PRECISION、SQL_DESC_SCALE、および SQL_DESC_NULLABLE です。 一貫性を確保するために、 **SQLGetDescField** も SQL_DESC_UNNAMED を返します。  
  
 SQLGetDescField、SQL_DESC_INDICATOR_PTR、SQL_DESC_OCTET_LENGTH_PTR、および SQL_DESC_LENGTH のバインドブックマーク SQL_DESC_DATA_PTR 列に設定されている次のフィールドの値を返すために、カーソルライブラリが呼び出されると、 **SQLGetDescField**が実行されます。  
  
 カーソルライブラリは、SQL_DESC_BIND_OFFSET_PTR、SQL_DESC_BIND_TYPE、SQL_DESC_ROW_ARRAY_SIZE、または SQL_DESC_ROW_STATUS_PTR の各フィールドの値を返すために呼び出されると、 **SQLGetDescField** を実行します。 これらのフィールドは、ブックマーク行だけでなく、任意の行に対して返すことができます。  
  
 アプリケーションが **SQLGetDescField** を呼び出して、前に説明した以外のフィールドの値を返す場合、カーソルライブラリは呼び出しをドライバーに渡します。
