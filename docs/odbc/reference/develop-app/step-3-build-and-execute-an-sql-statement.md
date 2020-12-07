---
description: 手順 3:SQL ステートメントのビルドと実行
title: '手順 3: SQL ステートメントをビルドして実行する |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], building and executing statements
- SQL statements [ODBC], building and executing
ms.assetid: 133b8bd4-a3c8-4f7e-93c5-c05283c8e96f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cf99649ca84ab557457a1fb067e06188552b6aad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461354"
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>手順 3:SQL ステートメントのビルドと実行
3番目の手順では、次の図に示すように、SQL ステートメントをビルドして実行します。 この手順の実行に使用する方法は、大きく異なる可能性があります。 アプリケーションでは、SQL ステートメントを入力したり、ユーザー入力に基づいて SQL ステートメントを作成したり、ハードコーディングされた SQL ステートメントを使用したりするようユーザーに求めることができます。 詳細については、「 [SQL ステートメントの構築](../../../odbc/reference/develop-app/constructing-sql-statements.md)」を参照してください。  
  
 ![SQL ステートメントのビルドと実行](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 SQL ステートメントにパラメーターが含まれている場合、アプリケーションは、各パラメーターに対して **SQLBindParameter** を呼び出すことによって、これらのパラメーターをアプリケーション変数にバインドします。 詳細については、「 [ステートメントパラメーター](../../../odbc/reference/develop-app/statement-parameters.md)」を参照してください。  
  
 SQL ステートメントが作成され、すべてのパラメーターがバインドされると、 **SQLExecDirect**を使用してステートメントが実行されます。 ステートメントが複数回実行される場合は、 **SQLPrepare** で準備し、 **sqlexecute**を使用して実行できます。 詳細については、「 [ステートメントの実行](../../../odbc/reference/develop-app/executing-a-statement.md)」を参照してください。  
  
 また、アプリケーションでは、SQL ステートメントを完全に実行し、代わりに関数を呼び出して、使用可能な列やテーブルなどのカタログ情報を含む結果セットを返すことも済ませるます。 詳細については、「 [カタログデータの使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)」を参照してください。  
  
 アプリケーションの次のアクションは、実行された SQL ステートメントの種類によって異なります。  
  
|SQL ステートメントの種類|続行|  
|---------------------------|----------------|  
|**SELECT** または catalog 関数|[手順 4a: 結果をフェッチする](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**更新**、 **削除**、または **挿入**|[手順 4b: 行数をフェッチする](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|その他のすべての SQL ステートメント|手順 3: SQL ステートメントをビルドして実行する (このトピック)、または [手順 5: トランザクションをコミットする](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|
