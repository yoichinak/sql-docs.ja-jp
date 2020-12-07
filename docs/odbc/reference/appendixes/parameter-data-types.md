---
description: パラメーターのデータ型
title: パラメーターのデータ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], parameters
- parameter data type [ODBC]
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: fd7e99d8-d26a-408c-9733-6ffccde99f75
author: David-Engel
ms.author: v-daenge
ms.reviewer: ''
ms.openlocfilehash: 0114f0cff269d35ddf1e93c653c46bcc8d863a29
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483245"
---
# <a name="parameter-data-types"></a>パラメーターのデータ型
**SQLBindParameter**で指定された各パラメーターが sql データ型を使用して定義されている場合でも、sql ステートメントのパラメーターには組み込みデータ型がありません。 そのため、ステートメント内の別のオペランドからデータ型を推論できる場合にのみ、パラメーターマーカーを SQL ステートメントに含めることができます。 たとえば、のような算術式では、 + COLUMN1,、パラメーターのデータ型は、COLUMN1 で表される名前付きの列のデータ型から推論できます。 データ型を特定できない場合、アプリケーションでパラメーターマーカーを使用することはできません。  
  
 次の表では、SQL-92 に従って、いくつかの種類のパラメーターのデータ型を決定する方法について説明します。 他の SQL 句が使用されている場合のパラメーターの型の推論に関するより包括的な仕様については、「SQL-92 の仕様」を参照してください。  
  
|パラメーターの場所|想定されるデータ型|  
|---------------------------|-----------------------|  
|二項算術演算子または比較演算子の1つのオペランド|もう一方のオペランドと同じ|  
|**BETWEEN**句の最初のオペランド|2番目のオペランドと同じ|  
|**BETWEEN**句の2番目または3番目のオペランド|1番目のオペランドと同じ|  
|**ので**使用される式|サブクエリの最初の値または結果列と同じ|  
|**ので**使用される値|式と同じか、式にパラメーターマーカーがある場合は最初の値と同じ|  
|**LIKE**で使用されるパターン値|VARCHAR|  
|Update で使用される更新 **プログラムの値**|更新列と同じ|
