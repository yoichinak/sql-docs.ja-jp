---
description: SQL_NO_DATA を返す
title: SQL_NO_DATA | を返すMicrosoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
ms.assetid: deed0163-9d1a-4e9b-9342-3f82e64477d2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 24efdd88d16ba31a2b70dfb75ad21adee08c6f1c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424974"
---
# <a name="returning-sql_no_data"></a>SQL_NO_DATA を返す
*Odbc 2.x アプリケーションが*odbc 2.x アプリケーションをただし時して**SQLExecDirect**、 **Sqlexecute**、または**sqlparamdata**を呼び出し、検索された update または delete ステートメントが実行されたが、データソースの行に影響を与えていない場合、odbc *3. x* *ドライバーは*SQL_SUCCESS を返す必要があります。 *Odbc 3.x アプリケーションで*odbc *3.x ドライバーを*使用する場合、 **SQLExecDirect**、 **Sqlexecute**、または**SQLPARAMDATA**が同じ結果で呼び出されると、odbc *3. x*ドライバーは SQL_NO_DATA を返す必要があります。  
  
 ステートメントのバッチ内の検索された update ステートメントまたは delete ステートメントがデータソースの行に影響を与えない場合は、 **Sqlmoreresults** によって SQL_SUCCESS が返されます。 SQL_NO_DATA を返すことはできません。これは、結果がそれ以上ないことを意味します。行が影響を受けている検索された更新/削除の結果がないということです。
