---
description: 記述子ハンドル
title: 記述子ハンドル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application parameter descriptor [ODBC]
- automatically allocated descriptors [ODBC]
- implementation row descriptor [ODBC]
- descriptor handles [ODBC]
- handles [ODBC], descriptor
- implementation parameter descriptor [ODBC]
- apd [ODBC]
- ard [ODBC]
- explicitly allocated descriptors [ODBC]
- ipd [ODBC]
- ird [ODBC]
- application row descriptor [ODBC]
ms.assetid: 7741035c-f3e7-4c89-901e-fe528392f67d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 859071eacbfa65f360965cf5c5df17d4fbf6361d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476724"
---
# <a name="descriptor-handles"></a>記述子ハンドル
*記述子*は、アプリケーションまたはドライバー (*実装*とも呼ばれます) に示されているように、SQL ステートメントまたは結果セットの列のパラメーターを記述するメタデータのコレクションです。 このため、記述子は次の4つのロールのいずれかを満たすことができます。  
  
-   **アプリケーションパラメーター記述子 (APD)。** SQL ステートメント内のパラメーターにバインドされたアプリケーションバッファーに関する情報を格納します (アドレス、長さ、C データ型など)。  
  
-   **実装パラメーター記述子 (IPD)。** Sql のデータ型、長さ、null 値の許容など、SQL ステートメントのパラメーターに関する情報を格納します。  
  
-   **アプリケーションの行記述子 (標準)。** アドレス、長さ、C データ型など、結果セット内の列にバインドされたアプリケーションバッファーに関する情報を格納します。  
  
-   **実装行記述子 (IRD)。** SQL データ型、長さ、null 値の許容など、結果セット内の列に関する情報を格納します。  
  
 ステートメントが割り当てられると、4つの記述子 (各ロールの入力1つ) が自動的に割り当てられます。 これらは *自動的に割り当てら* れた記述子と呼ばれ、常にそのステートメントに関連付けられています。 アプリケーションでは、 **SQLAllocHandle**を使用して記述子を割り当てることもできます。 これらは、 *明示的に割り当てら*れた記述子と呼ばれます。 これらは接続に割り当てられ、その接続上の1つ以上のステートメントと関連付けて、APD の役割を果たすことができます。また、これらのステートメントを使用することもできます。  
  
 ODBC のほとんどの操作は、アプリケーションによって明示的に記述子を使用せずに実行できます。 ただし、記述子は、一部の操作に便利なショートカットを提供します。 たとえば、アプリケーションが2つの異なるバッファーセットからデータを挿入しようとしているとします。 バッファーの最初のセットを使用するには、 **SQLBindParameter** を繰り返し呼び出して、それらを **INSERT** ステートメントのパラメーターにバインドした後、ステートメントを実行します。 2番目のバッファーセットを使用するには、このプロセスを繰り返します。 または、1つの記述子のバッファーの最初のセットと、別の記述子の2番目のバッファーセットへのバインドを設定することもできます。 一連のバインドを切り替えるには、アプリケーションは単に **SQLSetStmtAttr** を呼び出し、正しい記述子を APD としてステートメントに関連付けます。  
  
 記述子の詳細については、「 [記述子の型](../../../odbc/reference/develop-app/types-of-descriptors.md)」を参照してください。
