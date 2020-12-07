---
description: DBMS ベースのドライバー診断の例
title: DBMS ベースのドライバー診断の例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBMS-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: a80d54b0-43ff-4dfd-b6cb-f4694a5ed765
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5425afb18a5582a840966798ea7a7209dba7e1e6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424744"
---
# <a name="dbms-based-driver-diagnostic-example"></a>DBMS ベースのドライバー診断の例
DBMS ベースのドライバーは、DBMS に要求を送信し、ドライバーマネージャーを使用してアプリケーションに情報を返します。 ドライバーはドライバーマネージャーとのインターフェイスを持つコンポーネントであるため、 **SQLGetDiagRec**の引数を書式設定して返します。  
  
 たとえば、SQL/Services を使用している場合、Microsoft driver for Oracle Rdb で無効なカーソル名が検出された場合は、 **SQLGetDiagRec**から次の値が返される可能性があります。  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 ドライバーでエラーが発生したため、ベンダー ([Microsoft]) とドライバー ([ODBC Rdb ドライバー]) の診断メッセージにプレフィックスが追加されました。  
  
 DBMS が EMPLOYEE テーブルを見つけることができなかった場合、ドライバーは **SQLGetDiagRec**から次の値を書式設定して返します。  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 データソースでエラーが発生したため、ドライバーによってデータソース識別子 ([Rdb]) のプレフィックスが診断メッセージに追加されました。 ドライバーは、データソースとの通信を行うコンポーネントであったので、そのベンダー ([Microsoft]) と識別子 ([ODBC Rdb ドライバー]) のプレフィックスが診断メッセージに追加されました。
