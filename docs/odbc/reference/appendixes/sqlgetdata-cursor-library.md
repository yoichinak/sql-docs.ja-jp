---
description: SQLGetData (カーソル ライブラリ)
title: SQLGetData (カーソルライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], Cursor Library
ms.assetid: ff40c9c0-b847-4426-a099-1bff47e6e872
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5288c46dc731f1bee8727e3825c95ccae663f871
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421466"
---
# <a name="sqlgetdata-cursor-library"></a>SQLGetData (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックでは、カーソルライブラリでの **SQLGetData** 関数の使用について説明します。 **SQLGetData**の一般的な情報については、「 [SQLGetData 関数](../../../odbc/reference/syntax/sqlgetdata-function.md)」を参照してください。  
  
 カーソルライブラリでは、最初に、現在の行のバインドされている各列のキャッシュに格納されている値を列挙する**WHERE**句を使用**して SELECT**ステートメントを構築することで、 **SQLGetData**を実装します。 次に、 **SELECT** ステートメントを実行して行を再選択し、ドライバーで **SQLGetData** を呼び出してデータソースからデータを取得します (キャッシュではなく)。  
  
> [!CAUTION]  
>  現在の行を識別するためにカーソルライブラリによって構築された **where** 句は、行の識別、別の行の識別、または複数の行の識別に失敗することがあります。 詳細については、「 [検索ステートメントの構築](../../../odbc/reference/appendixes/constructing-searched-statements.md)」を参照してください。  
  
 SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_VARIABLE に設定されている場合、列0で **SQLGetData** を呼び出してブックマークデータを返すことができます。  
  
 **SQLGetData**の呼び出しには、次の制限が適用されます。  
  
-   **SQLGetData** は、順方向専用カーソルに対して呼び出すことはできません。  
  
-   **SQLGetData** は、次の条件が満たされた場合にのみ呼び出すことができます。 **SELECT** ステートメントは、結果セットを生成します。 **SELECT** ステートメントに Join、 **UNION** 句、または **GROUP BY** 句が含まれていませんでした。また、選択リスト内の別名または式を使用した列は、 **SQLBindCol**にバインドされていませんでした。  
  
-   ドライバーが1つのアクティブステートメントのみをサポートしている場合、カーソルライブラリは、 **SELECT** ステートメントを実行して **SQLGetData**を呼び出す前に、残りの結果セットをフェッチします。
