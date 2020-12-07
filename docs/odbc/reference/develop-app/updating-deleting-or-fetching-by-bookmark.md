---
description: ブックマークによる更新、削除、またはフェッチ
title: ブックマーク | を更新、削除、またはフェッチするMicrosoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating by bookmarks [ODBC]
- result sets [ODBC], bookmarks
- fetches [ODBC], by bookmarks [ODBC]
- deleting by bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: e2ee58d7-c28f-435f-b537-06207215dd2f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2202e3483e13848ccac7f7e6f21145ba9704a8b7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448949"
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>ブックマークによる更新、削除、またはフェッチ
ブックマークを使用すると、結果セットで更新されるデータ、結果セットから削除されるデータ、または結果セットから行セットバッファーにフェッチされるデータを識別できます。 これらの操作は、SQL_UPDATE_BY_BOOKMARK、SQL_DELETE_BY_BOOKMARK、または SQL_FETCH_BY_BOOKMARK の*オプション*引数を使用して**sqlbulkoperations**を呼び出すことによって実行されます。 これらの操作で使用されるブックマークは、行セットバッファーの列0に格納されます。 ブックマークによって更新すると、結果セットの列が更新されるデータが行セットバッファーから取得されます。 詳細については、「 [SQLBulkOperations によるデータの更新](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)」を参照してください。
