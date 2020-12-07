---
description: SQLAllocConnect のマッピング
title: SQLAllocConnect マッピング |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f89ae59ca171fbcfbb9f6b75fdad639e31ea8fe0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429524"
---
# <a name="sqlallocconnect-mapping"></a>SQLAllocConnect のマッピング
アプリケーションが ODBC 3 を介して **Sqlallocconnect** を呼び出すとき。*x* ドライバー: **sqlallocconnect**(*henv*, *phdbc*) の呼び出しは、次のように **SQLAllocHandle** にマップされます。  
  
1.  ドライバーマネージャーによって接続が割り当てられ、アプリケーションに返されます。  
  
2.  アプリケーションが接続を確立すると、ドライバーマネージャーはを呼び出します。  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     *InputHandle*が*henv*に設定されているドライバーで、 *OutputHandlePtr*を*phdbc*に設定します。
