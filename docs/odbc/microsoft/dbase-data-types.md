---
description: dBASE データ型
title: dBASE データ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], data types
- data types [ODBC], DBase driver
- dbase data types [ODBC]
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: a0e31e6b-d02b-4ee2-9b37-5baf6a11c0a6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9eca7d603a136bd1921ee93656d38f59efcda5f4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412768"
---
# <a name="dbase-data-types"></a>dBASE データ型
次の表に、dBASE データ型を ODBC SQL データ型にマップする方法を示します。 すべての ODBC SQL データ型がサポートされているわけではないことに注意してください。  
  
|dBASE データ型|ODBC データ型|  
|---------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATE|SQL_DATE|  
|FLOAT [1]|SQL_DOUBLE|  
|LUN|SQL_BIT|  
|記|SQL_LONGVARCHAR|  
|NUMERIC (BCD)|SQL_DOUBLE|  
|OLEOBJECT [1]|SQL_LONGBINARY|  
  
 [1] dBASE バージョン5でのみ有効です。*x*  
  
 DBASE III の有効桁数では、最大で2桁の指数と dBASE IV の数値に最大3桁の指数を持つ数値を使用できます。 数値はテキストとして格納されるため、数値に変換されます。 変換する数値がフィールドに合わない場合、予期しない結果が発生する可能性があります。  
  
 DBASE では、有効桁数と小数点以下桁数を数値データ型で指定できますが、ODBC dBASE ドライバーではサポートされていません。 ODBC dBASE ドライバーは、数値データ型に対して、常に15と小数点以下桁数が0の有効桁数を返します。  
  
 ODBC dBASE ドライバーを使用して Numeric データ型で作成された列は、SQL_DOUBLE ODBC データ型にマップされます。 したがって、この列のデータは丸められます。 この動作は dBASE (型 N) の数値データ型と同じではありません。これは、バイナリでコード化された10進数 (BCD) です。  
  
> [!NOTE]  
>  **SQLGetTypeInfo** は、ODBC SQL データ型を返します。 *Odbc プログラマーズリファレンス*の付録 D のすべての変換は、このトピックで前述した odbc SQL データ型に対してサポートされています。  
  
 次の表は、dBASE データ型に関する制限を示しています。  
  
|データ型|説明|  
|---------------|-----------------|  
|CHAR|長さが0または指定されていない CHAR 型の列を作成すると、実際には254バイトの列が返されます。|  
|暗号化データ|DBASE ドライバーは、暗号化された dBASE テーブルをサポートしていません。|  
|LUN|DBASE ドライバーでは、論理列にインデックスを作成できません。|  
|記|メモ列の最大長は65500バイトです。|  
  
 データ型に関する制限事項の詳細については、 [「データ型の制限](../../odbc/microsoft/data-type-limitations.md)」を参照してください。
