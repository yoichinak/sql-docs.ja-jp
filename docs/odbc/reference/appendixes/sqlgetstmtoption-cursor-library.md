---
description: SQLGetStmtOption (カーソル ライブラリ)
title: SQLGetStmtOption (カーソルライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], Cursor Library
ms.assetid: 986170b3-fba8-4323-9224-60b381c7effb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 38755e654e089dd764796a65b34ebc1fdbe8c701
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99202732"
---
# <a name="sqlgetstmtoption-cursor-library"></a>SQLGetStmtOption (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックでは、カーソルライブラリでの **SQLGetStmtOption** 関数の使用について説明します。 **SQLGetStmtOption** の一般的な情報については、「 [SQLGetStmtOption 関数](../../../odbc/reference/syntax/sqlgetstmtoption-function.md)」を参照してください。  
  
 カーソルライブラリでは、 **SQLGetStmtOption** を使用した次のステートメントオプションがサポートされています。  

:::row:::
    :::column:::
        SQL_BIND_TYPE  
        SQL_CONCURRENCY  
        SQL_CURSOR_TYPE  
        SQL_GET_BOOKMARK  
    :::column-end:::
    :::column:::
        SQL_ROW_NUMBER  
        SQL_ROWSET_SIZE  
        SQL_SIMULATE_CURSOR  
    :::column-end:::
:::row-end:::
