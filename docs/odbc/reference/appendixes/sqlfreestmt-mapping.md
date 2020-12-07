---
description: SQLFreeStmt のマッピング
title: SQLFreeStmt Mapping |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeStmt function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeStmt
ms.assetid: 267d95f2-4f0c-47ab-9411-5afe105215a2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1f5066593e900fc60eea0ce5a5fc183eb2e83137
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421486"
---
# <a name="sqlfreestmt-mapping"></a>SQLFreeStmt のマッピング
アプリケーションが ODBC *3. x*ドライバーを使用して SQL_DROP の*オプション*引数を使用して**SQLFreeStmt**を呼び出すと、が呼び出されます。  
  
```  
SQLFreeStmt(hstmt, SQL_DROP)   
```  
  
 がにマップされています  
  
```  
SQLFreeHandle(SQL_HANDLE_STMT,Handle)  
```  
  
 *ハンドル*引数が*hstmt*の値に設定されている。
