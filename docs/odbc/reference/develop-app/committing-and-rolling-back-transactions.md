---
description: トランザクションのコミットとロールバック
title: トランザクションのコミットとロールバック |Microsoft Docs
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
- transactions [ODBC], committing
ms.assetid: 800f2c1a-6f79-4ed1-830b-aa1a62ff5165
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b84be4d2734d9485748351c99ff2675bf3b54213
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424844"
---
# <a name="committing-and-rolling-back-transactions"></a>トランザクションのコミットとロールバック
手動コミットモードでトランザクションをコミットまたはロールバックするには、アプリケーションが **SQLEndTran**を呼び出します。 トランザクションをサポートする Dbms のドライバーは、通常、 **COMMIT** または **ROLLBACK** ステートメントを実行してこの関数を実装します。 接続が自動コミットモードの場合、ドライバーマネージャーは **SQLEndTran** を呼び出しません。アプリケーションがトランザクションをロールバックしようとした場合でも、単に SQL_SUCCESS を返します。 トランザクションをサポートしていない Dbms のドライバーは常に自動コミットモードであるため、 **SQLEndTran** を実装して、何も実行したり、まったく実装したりせずに SQL_SUCCESS を返すことができます。  
  
> [!NOTE]  
>  アプリケーションでは、 **Sqlexecute**または**SQLExecDirect**を指定して**commit**ステートメントまたは**ROLLBACK**ステートメントを実行することで、トランザクションをコミットまたはロールバックすることはできません。 この操作による影響は未定義です。 発生する可能性のある問題には、トランザクションがアクティブであるときにドライバーが認識しなくなったことと、トランザクションをサポートしていないデータソースに対してこれらのステートメントが失敗することがあります。 これらのアプリケーションは、代わりに **SQLEndTran** を呼び出す必要があります。  
  
 アプリケーションが環境ハンドルを **SQLEndTran** に渡しても接続ハンドルが渡されない場合、ドライバーマネージャーは概念的に、環境内で1つ以上のアクティブな接続を持つ各ドライバーの環境ハンドルを使用して **SQLEndTran** を呼び出します。 次に、ドライバーは、環境内の各接続のトランザクションをコミットします。 ただし、ドライバーとドライバーマネージャーのどちらも環境内の接続に対して2フェーズコミットを実行しないことを理解しておくことが重要です。これは、環境内のすべての接続に対して **SQLEndTran** を同時に呼び出すプログラミングに便利です。  
  
 ( *2 フェーズコミット* は、通常、複数のデータソースに分散されたトランザクションをコミットするために使用されます。 最初のフェーズでは、トランザクションの一部をコミットできるかどうかについて、データソースがポーリングされます。 2番目のフェーズでは、トランザクションはすべてのデータソースで実際にコミットされます。 データソースがトランザクションをコミットできないことを示す最初のフェーズで応答する場合、2番目のフェーズは発生しません。)
