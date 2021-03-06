---
description: SELECT FOR UPDATE ステートメントの処理
title: SELECT FOR UPDATE ステートメントの処理 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], select for update statements
- select for update [ODBC]
- SQL statements [ODBC], cursor library
- cursor library [ODBC], select for update statements
- ODBC cursor library [ODBC], select for update statements
- cursor library [ODBC], statement processing
ms.assetid: 8d2e79a4-5daf-458e-a536-d8b6e588753e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 116a87e12d1f765e3e33aa5b446743acfd8d429b
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99189739"
---
# <a name="processing-select-for-update-statements"></a>SELECT FOR UPDATE ステートメントの処理
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 相互運用性を最大にするには、 **SELECT FOR update** ステートメントを実行して、配置された update ステートメントで更新される結果セットをアプリケーションで生成する必要があります。 カーソルライブラリはこれを必要としませんが、位置指定の update ステートメントをサポートするほとんどのデータソースで必要になります。  
  
 **SELECT FOR update** ステートメントの **for update** 句の列は、カーソルライブラリによって無視されます。ステートメントをドライバーに渡す前に、この句を削除します。 カーソルライブラリでは、SQL_ATTR_CONCURRENCY statement 属性と、前のセクションで説明した制限を使用して、結果セット内の列を更新できるかどうかを制御します。
