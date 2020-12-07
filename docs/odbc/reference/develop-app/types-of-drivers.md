---
description: ドライバーの種類
title: ドライバーの種類 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver compatibility issues [ODBC]
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
ms.assetid: 864c53c1-b68a-48b6-b6bc-5ecb520bb9dc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ae3ab2b0172e97a221b446107ccbf4b6ae4eb7b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476296"
---
# <a name="types-of-drivers"></a>ドライバーの種類
ODBC ドライバーは、次のように分類できます。  
  
-   **32-ビット ODBC 2。**  
     ** _x_ドライバー** A 32 ビットドライバー:  
  
    -   ODBC 2.x 関数のみをエクスポート*します。*  
  
    -   動作変更に関する ODBC 2.x の動作について解説*します。*  
  
-   **ISO とオープングループに準拠しているドライバー** 次のような32ビットドライバー。  
  
    -   Open Group または ISO CLI ドキュメントに記載されているすべての関数をエクスポートします。 これには、ODBC で非推奨とされる関数が含まれます。  
  
    -   動作の変更に対する ODBC 3.0 の動作を解説します。  
  
    -   は必ずしも ODBC 3.0 ドライバーマネージャーを経由するわけではありません。  
  
-   **ODBC 3.0 ドライバー** 次のような32ビットドライバー。  
  
    -   ODBC 3.0 に含まれている関数を非推奨の関数から除き、エクスポートします。  
  
    -   では、SQL_ATTR_APP_ODBC_VERSION 環境属性に基づいて、動作の変更に関し *て odbc 2.x* の動作または odbc 3.0 の動作が可能です。  
  
-   **ODBC 3.5 (またはそれ以降) ANSI ドライバー** 次のような32ビットドライバー。  
  
    -   ODBC 3.5 に含まれている関数を非推奨の関数から除き、エクスポートします。  
  
    -   では、SQL_ATTR_APP_ODBC_VERSION 環境属性に基づいて *、odbc 2.x の動作また* は odbc 3.0 の動作、または動作の変更に関して odbc 3.5 の動作が可能です。  
  
-   **ODBC 3.5 (またはそれ以降) Unicode ドライバー** 次のような32ビットドライバー。  
  
    -   では、ODBC 3.5 ANSI ドライバーのすべての機能がサポートされています。  
  
    -   すべての ODBC 文字列 Api の Unicode バージョンをエクスポートします。  
  
    -   では、データソースに Unicode データを格納して処理できます。  
  
> [!NOTE]  
>  16ビット *odbc ドライバーは、odbc 3.X* ドライバーマネージャーで直接動作しません。 ただし、16ビットドライバーが 2.0 ODBC ドライバーマネージャーで動作する可能性があります。この場合は、その後、 *3. x* ドライバーマネージャーにサンクを行います。
