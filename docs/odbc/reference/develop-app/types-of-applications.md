---
description: アプリケーションの種類
title: アプリケーションの種類 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading applications [ODBC], application types
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application upgrades [ODBC], application types
- application compatibility issues [ODBC]
ms.assetid: d346a64e-a32c-4153-a40f-5b53c2f57ef2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 54056a6111924fb584ac35a65d6f74e8dab1ba6c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465552"
---
# <a name="types-of-applications"></a>アプリケーションの種類
ODBC アプリケーションは、次のように分類できます。  
  
-   **純粋な ODBC 2。**  
     ** _x_アプリケーション**は、次のような32ビットアプリケーションを実行します。  
  
    -   は ODBC 2 だけを呼び出します。*x* 関数 (ODBC 1.0 関数 **SQLSetParam**を含む)。 これには ODBC 1 が含まれます。32ビットに移植された*x* アプリケーション。  
  
    -   ODBC 2 が必要です。動作が変更された機能の*x* 動作。 (詳細については、「 [動作の変更](../../../odbc/reference/develop-app/behavioral-changes.md) 」を参照してください。)  
  
    -   が ODBC 3.5 ヘッダーを使用して再コンパイルされていません。  
  
-   **純粋な ODBC 2。**  
     **_x_ 再コンパイル済みアプリケーション** の純粋な ODBC 2。ODBCVER = 0x0250 を設定して、ODBC 3.5 ヘッダーファイルを使用して再コンパイルされた*x* アプリケーション。  
  
-   **純粋な ODBC 2。**  
     **_x_ Unicode アプリケーション** を純粋な ODBC 2 にします。Unicode に準拠し、SQL_WCHAR データ型を使用する*x* 再コンパイルされたアプリケーション。  
  
-   **ピュア Open Group と ISO** -準拠している**ODBC アプリケーション**次のような32ビットアプリケーション:  
  
    -   Open Group または ISO CLI 標準で定義されている関数を呼び出します。 (これらの関数には、非推奨の3.0 関数が含まれる場合があります)。  
  
    -   Unicode データ型は使用しません。  
  
    -   動作が変更された機能には ODBC 3.0 の動作が必要です。  
  
-   **純粋な ODBC 3.0 アプリケーション** 次のような32ビットアプリケーション:  
  
    -   は3.0 ヘッダーを使用してコンパイルされます。  
  
    -   ODBC 3.0 関数を呼び出します。非推奨のものも含まれます。  
  
    -   動作が変更された機能には ODBC 3.0 の動作が必要です。  
  
-   **純粋な ODBC 3.5 アプリケーション** 次のような32または64ビットのアプリケーション:  
  
    -   Unicode データ型を使用できます。  
  
    -   ODBC 3.5 関数を呼び出します。非推奨のものも含まれます。  
  
    -   動作が変更された機能には ODBC 3.5 の動作が必要です。  
  
-   **純粋 ODBC 3.8 (またはそれ以降) のアプリケーション** 次のような32ビットまたは64ビットのアプリケーション。  
  
    -   Unicode データ型を使用できます。  
  
    -   ODBC 3.8 関数を呼び出します。非推奨のものも含まれます。  
  
    -   動作が変更された機能には ODBC 3.8 の動作が必要です。  
  
-   **置換** されたアプリケーション次のような32または64ビットのアプリケーション:  
  
    -   重複する機能の新しい動作を実装します。  
  
    -   では、新しいバージョンの ODBC では、条件付きコード内でのみ新しい機能を使用します。  
  
    -   には、動作変更を処理するための条件付きコードが制限されているか、以前のバージョンの ODBC アプリケーションとして登録されています。
