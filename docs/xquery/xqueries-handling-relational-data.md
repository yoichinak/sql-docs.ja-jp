---
title: リレーショナルデータを処理する XQueries |Microsoft Docs
description: 'XQuery 拡張機能 sql: column () および sql: variable () を使用して、xml 以外のリレーショナルデータを XML にバインドする方法について説明します。'
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- relational data [XQuery]
- XQuery, relational data
ms.assetid: 9812b71a-52ec-48a0-92f3-016a93660229
author: rothja
ms.author: jroth
ms.openlocfilehash: 6ac32119090ba7973ad628c35f6b5b994eb03561
ms.sourcegitcommit: f29f74e04ba9c4d72b9bcc292490f3c076227f7c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2021
ms.locfileid: "98172354"
---
# <a name="xqueries-handling-relational-data"></a>リレーショナル データを処理する XQuery
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  **Xml 型の** 列または変数に対して XQuery を指定するには、 [xml データ型のメソッド](../t-sql/xml/xml-data-type-methods.md)のいずれかを使用します。 これには、 **query ()**、 **value ()**、 **exist ()**、 **modify ()** が含まれます。 XQuery は、XML を生成するクエリで識別される XML インスタンスに対して実行されます。  
  
 XQuery の実行によって生成される XML には、他の Transact-SQL 変数や行セット列から取得される値を含めることができます。 XML 以外のリレーショナルデータを結果の XML にバインドするために、SQL Server には XQuery 拡張として次の擬似関数が用意されています。  
  
-   **sql:column()** function  
  
-   **sql:variable()** function  
  
 **Xml** データ型の **query ()** メソッドで xquery を指定するときに、これらの xquery 拡張機能を使用できます。 その結果、 **query ()** メソッドは、**xml データ型と xml 以外** のデータ型のデータを結合する xml を生成できます。  
  
 これらの関数は、 **xml** データ型のメソッド **modify ()**、 **value ()**、 **query ()**、および **exist ()** を使用して xml 内部のリレーショナル値を公開する場合にも使用できます。  
  
 詳細については、「 [sql: column () 関数 (xquery)](../xquery/xquery-extension-functions-sql-column.md) 」および「 [sql: variable () 関数 (xquery)](../xquery/xquery-extension-functions-sql-variable.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [XML データ &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 言語リファレンス &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [XML 構築 &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)  
  
  
