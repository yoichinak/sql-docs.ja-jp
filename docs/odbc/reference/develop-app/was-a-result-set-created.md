---
description: 結果セットは作成されましたか?
title: 結果セットは作成されましたか? | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], determining if created
ms.assetid: 4a83b8cb-2d57-4e64-b497-80bd587ee1f9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 57b65c254f48d9c3f5078c3b2c1f576ae54d4740
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421386"
---
# <a name="was-a-result-set-created"></a>結果セットは作成されましたか?
ほとんどの場合、アプリケーションのプログラマは、アプリケーションが実行するステートメントによって結果セットが作成されるかどうかを判断します。 これは、アプリケーションがプログラマによって記述されたハードコーディングされた SQL ステートメントを使用する場合に当てはまります。 アプリケーションが実行時に SQL ステートメントを構築する場合は、通常、 **SELECT** ステートメントまたは **INSERT** ステートメントが構築されているかどうかを示すコードをプログラマが簡単に含めることができます。 場合によっては、プログラマがステートメントで結果セットを作成するかどうかを判断できないことがあります。 これは、ユーザーが SQL ステートメントを入力して実行するための方法をアプリケーションが提供する場合に当てはまります。 これは、アプリケーションが実行時にプロシージャを実行するステートメントを構築する場合にも当てはまります。  
  
 このような場合、アプリケーションは **Sqlnumresultcols** を呼び出して、結果セット内の列の数を決定します。 0の場合、ステートメントは結果セットを作成しませんでした。それ以外の数値の場合は、ステートメントによって結果セットが作成されます。  
  
 アプリケーションでは、ステートメントが準備または実行された後、いつでも **Sqlnumresultcols** を呼び出すことができます。 ただし、一部のデータソースは、準備されたステートメントによって作成される結果セットを簡単に表すことができないため、ステートメントが準備されてから実行されるまでの間に **Sqlnumresultcols** が呼び出された場合、パフォーマンスが低下します。  
  
 一部のデータソースでは、SQL ステートメントが結果セットで返す行の数を決定することもできます。 これを行うには、アプリケーションが **SQLRowCount**を呼び出します。 行数が表す内容は、SQL_DYNAMIC_CURSOR_ATTRIBUTES2、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2、SQL_KEYSET_CURSOR_ATTRIBUTES2、または SQL_STATIC_CURSOR_ATTRIBUTES2 オプションの設定 (カーソルの種類によって異なります) が **SQLGetInfo**の呼び出しによって示されます。 このビットマスクは、返される行数が正確であるか、概数であるか、またはまったく使用できないかを、カーソルの種類ごとに示します。 静的カーソルまたはキーセットドリブンカーソルの行数が、 **Sqlbulkoperations** または **SQLSetPos**を使用して行われた変更、または位置指定 update ステートメントまたは delete ステートメントによって影響を受けるかどうかは、前に示した同じオプション引数によって返される他のビットによって決まります。 詳細については、 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 関数の説明を参照してください。
