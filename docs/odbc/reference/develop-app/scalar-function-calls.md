---
description: スカラー関数の呼び出し
title: スカラー関数呼び出し |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function calls
ms.assetid: 10cb4dcf-4cd8-4a56-8725-d080bd3ffe47
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b6d0f77adaf6284bceac126b3539121cbdb174ca
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465590"
---
# <a name="scalar-function-calls"></a>スカラー関数の呼び出し
スカラー関数は、各行の値を返します。 たとえば、絶対値スカラー関数は、数値列を引数として受け取り、列の各値の絶対値を返します。 スカラー関数を呼び出すためのエスケープシーケンスは、  
  
 **{fn**  _スカラー関数_ **}**  
  
 ここで、 *スカラー関数* は、 [「付録 E: スカラー関数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)」に記載されている関数の1つです。 スカラー関数のエスケープシーケンスの詳細については、「付録 C: SQL 文法」の「 [スカラー関数のエスケープシーケンス](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md) 」を参照してください。  
  
 たとえば、次の SQL ステートメントでは、大文字の顧客名と同じ結果セットが作成されます。 最初のステートメントでは、エスケープシーケンス構文を使用します。 2番目のステートメントでは、OS/2 の Ingres にネイティブ構文を使用し、相互運用できません。  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 アプリケーションでは、ネイティブ構文を使用するスカラー関数の呼び出しと、ODBC 構文を使用するスカラー関数の呼び出しを混在させることができます。 たとえば、Employee テーブル内の名前が姓、コンマ、および名として格納されているとします。 次の SQL ステートメントでは、Employee テーブル内の従業員の姓の結果セットを作成します。 このステートメントでは、ODBC スカラー関数の **部分文字列** と SQL Server スカラー関数 **CHARINDEX** を使用しており、SQL Server でのみ正しく実行されます。  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) - 1)} FROM Customers  
```  
  
 相互運用性を最大限に高めるには、スカラー関数の出力が必要な型であることを確認するために、アプリケーションでスカラーの **変換** 関数を使用する必要があります。 **CONVERT**関数は、1つの sql データ型から指定された sql データ型にデータを変換します。 **CONVERT**関数の構文は、  
  
 **CONVERT (** _value_exp_ **、** _data_type_**)**  
  
 ここで*value_exp*は列名、別のスカラー関数の結果、またはリテラル値であり、 *Data_type*は、 [「付録 D: データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md)」で定義されている SQL データ型識別子によって使用される **#define**名と一致するキーワードです。 たとえば、次の SQL ステートメントでは、 **CONVERT** 関数を使用して、 **curdate** 関数の出力が、タイムスタンプまたは文字データではなく日付であることを確認しています。  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 アプリケーションは、データソースでサポートされているスカラー関数を特定するために、SQL_CONVERT_FUNCTIONS、SQL_NUMERIC_FUNCTIONS、SQL_STRING_FUNCTIONS、SQL_SYSTEM_FUNCTIONS、および SQL_TIMEDATE_FUNCTIONS オプションを使用して **SQLGetInfo** を呼び出します。 **CONVERT**関数でサポートされている変換操作を特定するために、アプリケーションは SQL_CONVERT で始まる任意のオプションを指定して**SQLGetInfo**を呼び出します。
