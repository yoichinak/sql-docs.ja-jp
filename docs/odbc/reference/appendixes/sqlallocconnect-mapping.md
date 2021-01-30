---
description: SQLAllocConnect のマッピング
title: SQLAllocConnect マッピング |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3fd1659e4faaee713a2b9d942deb53fe00ea367c
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99202978"
---
# <a name="sqlallocconnect-mapping"></a>SQLAllocConnect のマッピング
アプリケーションが ODBC 3 を介して **Sqlallocconnect** を呼び出すとき。*x* ドライバー: **sqlallocconnect**(*henv*, *phdbc*) の呼び出しは、次のように **SQLAllocHandle** にマップされます。  
  
1.  ドライバーマネージャーによって接続が割り当てられ、アプリケーションに返されます。  
  
2.  アプリケーションが接続を確立すると、ドライバーマネージャーはを呼び出します。  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     *InputHandle* が *henv* に設定されているドライバーで、 *OutputHandlePtr* を *phdbc* に設定します。
