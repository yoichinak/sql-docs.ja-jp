---
description: 遅延フィールド
title: 遅延フィールド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], deferred fields
- deferred fields [ODBC]
ms.assetid: 5abeb9cc-4070-4f43-a80d-ad6a2004e5f3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f8b313f2d77270e95830de1a524706aa7fe36e33
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424694"
---
# <a name="deferred-fields"></a>遅延フィールド
*遅延フィールド*の値は、設定されているときは使用されませんが、遅延効果のために変数のアドレスが保存されます。 アプリケーションパラメーター記述子の場合、ドライバーは、 **SQLExecDirect** または **sqlexecute**の呼び出し時に変数の内容を使用します。 アプリケーションの行記述子の場合、ドライバーは、フェッチ時に変数の内容を使用します。  
  
 遅延フィールドは次のとおりです。  
  
-   記述子レコードの SQL_DESC_DATA_PTR および SQL_DESC_INDICATOR_PTR フィールド。  
  
-   アプリケーション記述子レコードの SQL_DESC_OCTET_LENGTH_PTR フィールド。  
  
-   複数行フェッチの場合、記述子ヘッダーの SQL_DESC_ARRAY_STATUS_PTR および SQL_DESC_ROWS_PROCESSED_PTR フィールドです。  
  
 記述子が割り当てられると、各記述子レコードの遅延フィールドには、最初に null 値が設定されます。 Null 値の意味は次のとおりです。  
  
-   SQL_DESC_ARRAY_STATUS_PTR に null 値が含まれている場合、複数行のフェッチでは、行ごとの診断情報のこのコンポーネントを返すことができません。  
  
-   SQL_DESC_DATA_PTR に null 値が含まれる場合、レコードはバインド解除されます。  
  
-   の SQL_DESC_OCTET_LENGTH_PTR フィールドに null 値が含まれている場合、ドライバーはその列の長さの情報を返しません。  
  
-   APD の SQL_DESC_OCTET_LENGTH_PTR フィールドに null 値が含まれていて、パラメーターが文字列の場合、ドライバーはその文字列が null で終わることを前提としています。 出力動的パラメーターの場合、このフィールドに null 値を指定すると、ドライバーは長さの情報を返すことができません。 (SQL_DESC_TYPE フィールドに文字文字列パラメーターが指定されていない場合、SQL_DESC_OCTET_LENGTH_PTR フィールドは無視されます)。  
  
 アプリケーションでは、遅延フィールドに使用される変数を、フィールドと関連付けられた時刻と、ドライバーが読み書きする時間の間で、割り当てを解除したり破棄したりすることはできません。
