---
description: 表示サイズ
title: 表示サイズ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- display size of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- SQL data types [ODBC], column characteristics
ms.assetid: 9f7f766f-2492-463c-aab7-f2476e222042
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 747c2076c528df8c312c9b3ed45e45a165299d59
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456587"
---
# <a name="display-size"></a>表示サイズ
列の表示サイズは、文字形式でデータを表示するために必要な最大文字数です。 次の表では、各 ODBC SQL データ型の表示サイズを定義します。  
  
|SQL 型識別子|ディスプレイ サイズ|  
|-------------------------|------------------|  
|すべての文字型 [a]|定義された (固定型の場合) または最大値 (変数型の場合)。データを文字形式で表示するために必要な文字数。|  
|SQL_DECIMAL SQL_NUMERIC|列の有効桁数に2を加えた値 (符号、 *有効* 桁数、および小数点)。 たとえば、NUMERIC (10, 3) として定義されている列の表示サイズは12です。|  
|SQL_BIT|1 (1 桁)。|  
|SQL_TINYINT|符号付きの場合は 4 (符号と3桁)、符号なしの場合は 3 (3 桁)。|  
|SQL_SMALLINT|符号付きの場合は 6 (符号と5桁)、または符号なし (5 桁) の場合は5です。|  
|SQL_INTEGER|符号付きの場合は 11 (符号と10桁)、符号なし (10 桁) の場合は10。|  
|SQL_BIGINT|20 (符号付きの場合は符号、数字の場合は19桁、符号なしの場合は20桁)。|  
|SQL_REAL|14 (符号、7桁、小数点、文字 *E*、符号、および2桁)。|  
|SQL_FLOAT SQL_DOUBLE|24 (符号、15桁、小数点、文字 *E*、符号、3桁)。|  
|すべてのバイナリ型 [a]|列の定義済みまたは最大値 (変数型の場合) の長さ2。 (各バイナリバイトは2桁の16進数で表されます)。|  
|SQL_TYPE_DATE|10 ( *yyyy-mm-dd*形式の日付)。|  
|SQL_TYPE_TIME|8 ( *hh: mm: ss*の形式の時刻)<br /><br /> - または -<br /><br /> 9 + *s* ( *hh: mm: ss*[. fff...] という形式の時刻)。 *s* は秒の小数部の有効桁数です。|  
|SQL_TYPE_TIMESTAMP|19 ( *yyyy-mm-dd hh: mm: ss* 形式のタイムスタンプの場合)<br /><br /> - または -<br /><br /> 20 + *s* ( *yyyy-mm-dd hh: mm: ss*[. fff...] 形式のタイムスタンプの場合、 *s* は秒の小数部の有効桁数)。|  
|すべての interval データ型|「 [Interval データ型の長さ](../../../odbc/reference/appendixes/interval-data-type-length.md)」を参照してください。|  
|SQL_GUID|36 ( *aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee* 形式の文字数|  
  
 [a] 変数の型の列またはパラメーターの長さをドライバーが判別できない場合、SQL_NO_TOTAL が返されます。
