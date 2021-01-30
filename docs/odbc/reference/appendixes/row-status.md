---
description: 行の状態
title: 行の状態 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- row status [ODBC]
- cache [ODBC]
ms.assetid: 0f0b1fb6-f697-4ced-811c-2908e210bc71
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 491e0b420e31f1fe8e66c73f9ab8d89cb1e7e1cd
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99187158"
---
# <a name="row-status"></a>行の状態
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 カーソルライブラリによって、行の状態のバッファーがキャッシュに作成されます。 カーソルライブラリは、このバッファーから行ステータス配列 (SQL_ATTR_ROW_STATUS_PTR statement 属性で指定) の値を取得します。 カーソルライブラリは、各行に対して、このバッファーを次のように設定します。  
  
-   行に位置指定 delete ステートメントを実行するときに SQL_ROW_DELETED します。  
  
-   **Sqlfetch** を使用してデータソースから行を取得中にエラーが発生したときに SQL_ROW_ERROR します。  
  
-   データソースから **Sqlfetch** を使用して行が正常にフェッチされたときに SQL_ROW_SUCCESS します。  
  
-   行に対して位置指定更新ステートメントを実行するときに SQL_ROW_UPDATED します。
