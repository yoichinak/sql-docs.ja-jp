---
description: SQLCloseCursor_ODBC
title: SQLCloseCursor_ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- SQLCloseCursor function [ODBC], ODBC
ms.assetid: 5e47e3f7-e1b8-451f-bf75-daa19b7c7271
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 06943851bc71e5a54792fa24ddb6e8e7908c13c7
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99202904"
---
# <a name="sqlclosecursor_odbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックでは、カーソルライブラリでの **Sqlcloの** 使用方法について説明します。 **Sqlcloに** 関する一般的な情報については、「 [Sqlcloの機能](../../../odbc/reference/syntax/sqlclosecursor-function.md)」を参照してください。  
  
 カーソルライブラリでは、カーソルを開かずに **Sqlcloを** 呼び出すことはできません。 これを試みると、SQLSTATE 24000 (無効なカーソル状態) が返されます。 カーソルが開いていないときに SQL_CLOSE の *オプション* を指定して **SQLFreeStmt** を呼び出すと、カーソルライブラリでサポートされます。
