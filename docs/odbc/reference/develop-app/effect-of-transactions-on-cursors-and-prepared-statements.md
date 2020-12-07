---
description: カーソルと準備されたステートメントでのトランザクションの影響
title: カーソルおよび準備されたステートメントに対するトランザクションの影響 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- cursors [ODBC], transaction commits or roll backs
- prepared statements [ODBC]
- transactions [ODBC], cursors
ms.assetid: 523e22a2-7b53-4c25-97c1-ef0284aec76e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 495bb8455c3e13b88d2d3ae6b400c5c0f2167604
ms.sourcegitcommit: 0f484f32709a414f05562bbaafeca9a9fc57c9ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2020
ms.locfileid: "94631678"
---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>カーソルと準備されたステートメントでのトランザクションの影響
トランザクションのコミットまたはロールバックには、カーソルとアクセスプランに関して次のいずれかの影響があります。  
  
-   すべてのカーソルが閉じられ、その接続での準備されたステートメントのアクセスプランが削除されます。  
  
-   すべてのカーソルが閉じられ、その接続で準備されたステートメントのアクセスプランはそのまま残ります。 
  
-   すべてのカーソルは開いたままになり、その接続での準備されたステートメントのアクセスプランはそのまま残ります。  
  
 たとえば、この一覧の最初の動作がデータソースによって示されているとします。これらの動作のうち、最も制限の厳しいものがあります。 ここで、アプリケーションで次のことを実行するとします。  
  
1.  コミットモードを手動コミットに設定します。  
  
2.  ステートメント1で販売注文の結果セットを作成します。  
  
3.  ステートメント2で、ユーザーがその注文を強調表示したときに、販売注文の行の結果セットを作成します。  
  
4.  ユーザーが行を更新すると、 **Sqlexecute** を呼び出して、ステートメント3で準備された位置指定更新ステートメントを実行します。  
  
5.  **SQLEndTran** を呼び出して、位置指定更新ステートメントをコミットします。  
  
 データソースの動作により、手順 5. で **SQLEndTran** を呼び出すと、ステートメント1および2のカーソルが閉じられ、すべてのステートメントでアクセスプランが削除されます。 アプリケーションでは、ステートメント1と2を再実行して結果セットを再作成し、ステートメント3でステートメントを再準備する必要があります。  
  
 自動コミットモードでは、 **SQLEndTran** commit トランザクション以外の関数は次のようになります。  
  
-   前の例では、 **sqlexecute** または **SQLExecDirect** を実行します。手順4で **sqlexecute** を呼び出すと、トランザクションがコミットされます。 これにより、データソースは、ステートメント1および2のカーソルを閉じ、その接続のすべてのステートメントでアクセスプランを削除します。  
  
-   前の例の **Sqlbulkoperations** または **sqlsetpos** は、手順 4. で、ステートメント3で位置指定された UPDATE ステートメントを実行するのではなく、ステートメント2の SQL_UPDATE オプションを使用して **sqlsetpos** を呼び出すとします。 これによりトランザクションがコミットされ、データソースによってステートメント1および2のカーソルが閉じられ、その接続のすべてのアクセスプランが破棄されます。  
  
-   **Sqlcloセキュリティー** 前の例では、ユーザーが別の販売注文を強調表示すると、アプリケーションは、新しい販売注文の行の結果を作成する前に、ステートメント2で **Sqlcloを** 呼び出します。 **Sqlcloを** 呼び出すと、行の結果セットを作成した **select** ステートメントがコミットされ、データソースによってステートメント1のカーソルが閉じられ、その接続のすべてのアクセスプランが破棄されます。  
  
 アプリケーション (特に、ユーザーが結果セットをスクロールして行を更新または削除する画面ベースのアプリケーション) は、この動作をコーディングするために注意する必要があります。  
  
 トランザクションがコミットまたはロールバックされたときにデータソースがどのように動作するかを判断するために、アプリケーションは SQL_CURSOR_COMMIT_BEHAVIOR オプションと SQL_CURSOR_ROLLBACK_BEHAVIOR オプションを使用して **SQLGetInfo** を呼び出します。
