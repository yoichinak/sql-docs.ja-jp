---
description: SQLFreeConnect のマッピング
title: SQLFreeConnect Mapping |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLFreeConnect
- SQLFreeConnect function [ODBC], mapping
ms.assetid: 8a844538-93c0-4709-bab6-35c45e771d80
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e63a4609636d1fbea5ddf83ff629bf50a827cd4a
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99202837"
---
# <a name="sqlfreeconnect-mapping"></a>SQLFreeConnect のマッピング
アプリケーションが ODBC *3. x* ドライバーを介して **SQLFreeConnect** を呼び出すとき、  
  
```  
SQLFreeConnect(hdbc)   
```  
  
 がにマップされています  
  
```  
SQLFreeHandle(SQL_HANDLE_DBC,Handle)  
```  
  
 *Handle* 引数を *hdbc* の値に設定します。
