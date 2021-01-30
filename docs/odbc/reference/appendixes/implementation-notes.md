---
description: 実装に関するメモ
title: 実装に関するメモ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: 7ec14b9c-69b8-4c6e-838a-88d1ebdc8725
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3a3e23225183a023435aa06ba47a3e0033cad955
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99208558"
---
# <a name="implementation-notes"></a>実装に関するメモ
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 ここでは、ODBC カーソルライブラリの実装方法について説明します。 カーソルライブラリがどのようにキャッシュを保持し、SQL ステートメントを実行し、ODBC 関数を実装するかについて説明します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [カーソル ライブラリのキャッシュ](../../../odbc/reference/appendixes/cursor-library-cache.md)  
  
-   [SQL ステートメントの処理](../../../odbc/reference/appendixes/processing-sql-statements.md)  
  
-   [ODBC 関数およびカーソル ライブラリ](../../../odbc/reference/appendixes/odbc-functions-and-the-cursor-library.md)
