---
description: SQLSetScrollOptions のマッピング
title: SQLSetScrollOptions Mapping |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetScrollOptions
ms.assetid: a0fa4510-8891-4a61-a867-b2555bc35f05
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 111fb84cd584e23b18d889634893556de86311a2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476924"
---
# <a name="sqlsetscrolloptions-mapping"></a>SQLSetScrollOptions のマッピング
アプリケーションが ODBC *3. x*ドライバーを介して**SQLSetScrollOptions**を呼び出し、ドライバーが**SQLSetScrollOptions**をサポートしていない場合、  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 次のようになります。  
  
-   の呼び出し  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     *InfoType*引数が、 **SQLSetScrollOptions**の*keysetsize*引数の値に応じて、次の表のいずれかの値に設定されている。  
  
    |*KeysetSize 引数*|*InfoType 引数*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |*RowsetSize*引数より大きい値|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     *Keysetsize*引数の値が前の表に記載されていない場合、 **SQLSetScrollOptions**の呼び出しは SQLSTATE S1107 (範囲外の行値) を返し、次の手順は実行されません。  
  
     次に、ドライバーマネージャーは、 **SQLSetScrollOptions**の*Concurrency*引数の値に従って、 **SQLGetInfo**への呼び出しによって返される **infovalueptr*値に適切なビットが設定されているかどうかを確認します。  
  
    |*Concurrency* 引数|*InfoType* の設定|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     *同時実行*引数が前の表のいずれかの値ではない場合、 **SQLSetScrollOptions**を呼び出すと SQLSTATE S1108 (concurrency オプションが有効範囲外) が返され、次のいずれの手順も実行されません。 前の表に示されている適切なビットが、*同時実行*引数に*対応する値*の1つに設定されていない場合、 **SQLSETSCROLLOPTIONS**の呼び出しは SQLSTATE S1C00 (ドライバーに対応していません) を返し、次の手順は実行されません。  
  
-   の呼び出し  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CURSOR_TYPE, ValuePtr, 0)  
    ```  
  
     **SQLSetScrollOptions**の*keysetsize*引数の値に従って、 * \* valueptr*を次の表のいずれかの値に設定します。  
  
    |*Keysetsize* 引数|*\*ValuePtr*|  
    |---------------------------|------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_CURSOR_FORWARD_ONLY|  
    |SQL_SCROLL_STATIC|SQL_CURSOR_STATIC|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_CURSOR_KEYSET_DRIVEN|  
    |SQL_SCROLL_DYNAMIC|SQL_CURSOR_DYNAMIC|  
    |*RowsetSize*引数より大きい値|SQL_CURSOR_KEYSET_DRIVEN|  
  
-   の呼び出し  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CONCURRENCY, ValuePtr, 0)  
    ```  
  
     * \* Valueptr*を**SQLSetScrollOptions**の*Concurrency*引数に設定します。  
  
-   **SQLSetScrollOptions**への呼び出しの*keysetsize*引数が正の場合は、を呼び出します。  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_KEYSET_SIZE, ValuePtr, 0)  
    ```  
  
     * \* Valueptr*を**SQLSetScrollOptions**の*keysetsize*引数に設定します。  
  
-   の呼び出し  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ROWSET_SIZE, ValuePtr, 0)  
    ```  
  
     * \* Valueptr*を**SQLSetScrollOptions**の*RowsetSize*引数に設定します。  
  
    > [!NOTE]  
    >  ドライバーマネージャーが、 **SQLSetScrollOptions**をサポートしていない ODBC 3.x ドライバーを使用しているアプリケーションの**SQLSetScrollOptions**をマップする場合、ドライバーマネージャーは、 **SQLSetScrollOption**の*RowsetSize*引数に、ステートメントの SQL_ATTR_ROW_ARRAY_SIZE の属性ではなく SQL_ROWSET_SIZE ステートメントオプションを設定*します。* 結果として、 **Sqlfetch**または**sqlfetchscroll**の呼び出しによって複数の行をフェッチするときに、アプリケーションで**SQLSetScrollOptions**を使用することはできません。 **SQLExtendedFetch**の呼び出しによって複数の行をフェッチする場合にのみ使用できます。
