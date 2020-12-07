---
description: ステートメント パラメーター
title: ステートメントのパラメーター |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement parameters [ODBC]
ms.assetid: 58d5b166-2578-4699-a560-1f1e6d86c49a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7400367d4b237d2d0e22c6363d1559eb89506d7d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482895"
---
# <a name="statement-parameters"></a>ステートメント パラメーター
*パラメーター*は、SQL ステートメント内の変数です。 たとえば、Parts テーブルに、PartID、Description、および Price という名前の列があるとします。 パラメーターを指定せずにパートを追加するには、次のような SQL ステートメントを構築する必要があります。  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 このステートメントによって新しい注文が挿入されますが、挿入する値をアプリケーションにハードコーディングすることはできないため、注文入力アプリケーションでは適切なソリューションではありません。 別の方法としては、挿入する値を使用して、実行時に SQL ステートメントを作成する方法があります。 これは、実行時にステートメントを構築することが複雑になるため、適切な解決策でもありません。 最適な解決策は、 **VALUES** 句の要素を疑問符 (?) または *パラメーターマーカー*に置き換えることです。  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 これらのパラメーター マーカーは、その後アプリケーション変数にバインドされます。 新しい行を追加するには、アプリケーションで変数の値を設定し、ステートメントを実行するだけです。 ドライバーで、変数から現在値が取得され、データ ソースに送信されます。 ステートメントが複数回実行される場合、アプリケーションはステートメントを準備することで、プロセスをさらに効率的にすることができます。  
  
 表示されたステートメントは、新しい行を挿入するために、注文エントリアプリケーションにハードコーディングされている可能性があります。 ただし、パラメーターマーカーは、垂直方向のアプリケーションに限定されません。 アプリケーションによっては、テキスト間の変換を回避することで、実行時に SQL ステートメントを構築することが困難になります。 たとえば、表示された部分 ID は、アプリケーションに整数として格納される可能性が最も高くなります。 パラメーターマーカーを指定せずに SQL ステートメントを作成した場合、アプリケーションはその部分 ID をテキストに変換する必要があり、データソースはそれを整数に変換する必要があります。 パラメーターマーカーを使用すると、アプリケーションは要素 ID を整数としてドライバーに送信できます。これは通常、整数としてデータソースに送信できます。 これにより、2つの変換が保存されます。 長いデータ値の場合、これは非常に重要です。このような値のテキスト形式は、多くの場合、SQL ステートメントの許容される長さを超えるためです。  
  
 パラメーターは、SQL ステートメント内の特定の場所でのみ有効です。 たとえば、select リスト ( **select** ステートメントによって返される列の一覧) では使用できません。また、等号 (=) などの二項演算子の両方のオペランドとして使用することもできません。これは、パラメーターの型を特定できないためです。 通常、パラメーターはデータ操作言語 (DML) ステートメントでのみ有効で、データ定義言語 (DDL) ステートメントでは有効ではありません。 詳細については、「付録 C: SQL 文法」の「 [パラメーターマーカー](../../../odbc/reference/appendixes/parameter-markers.md) 」を参照してください。  
  
 SQL ステートメントによってプロシージャが呼び出されると、名前付きパラメーターを使用できます。 名前付きパラメーターは、SQL ステートメント内の位置ではなく、名前によって識別されます。 **SQLBindParameter**を呼び出すことでバインドできますが、パラメーターは、 **SQLBindParameter**の*parameternumber*引数ではなく、IPD (実装パラメーター記述子) の SQL_DESC_NAME フィールドによって識別されます。 また、 **SQLSetDescField** または **SQLSetDescRec**を呼び出すことによってバインドすることもできます。 名前付きパラメーターの詳細については、後の「 [名前によるパラメーターのバインド (名前付きパラメーター)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)」を参照してください。 記述子の詳細については、「 [記述子](../../../odbc/reference/develop-app/descriptors.md)」を参照してください。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [パラメーターのバインド](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [パラメーターの値の設定](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [長い形式のデータの送信](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [SQLGetData による出力パラメーターの取得](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [Procedure Parameters](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [パラメーター値の配列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
