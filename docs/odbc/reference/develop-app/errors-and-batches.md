---
description: エラーおよびバッチ
title: エラーとバッチ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC], errors
- sql_success_with_info [ODBC]
- sql_success [ODBC]
- SQL statements [ODBC], batches
- sql_error [ODBC]
ms.assetid: 6debd41d-9f4c-4f4c-a44b-2993da5306f0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1e5cdf4d394ffa1c17173aedc4485b6979cf371e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461494"
---
# <a name="errors-and-batches"></a>エラーおよびバッチ
SQL ステートメントのバッチの実行中にエラーが発生すると、次の4つのいずれかの結果が得られます。 (考えられる各結果はデータソース固有であり、バッチに含まれるステートメントにも依存する可能性があります)。  
  
-   バッチ内のステートメントは実行されません。  
  
-   バッチ内のステートメントは実行されず、トランザクションはロールバックされます。  
  
-   Error ステートメントの前にあるすべてのステートメントが実行されます。  
  
-   Error ステートメントを除くすべてのステートメントが実行されます。  
  
 最初の2つのケースでは、 **Sqlexecute** と **SQLExecDirect** は SQL_ERROR を返します。 後者の2つのケースでは、実装によっては SQL_SUCCESS_WITH_INFO または SQL_SUCCESS が返されることがあります。 どのような場合でも、 **SQLGetDiagField**、 **SQLGetDiagRec**、または **SQLError**を使用してさらにエラー情報を取得できます。 ただし、この情報の性質と深さは、データソース固有のものです。 また、この情報は、エラーのステートメントを正確に特定することはほとんどありません。
