---
description: 時刻および日付関数 (Visual FoxPro ODBC ドライバー)
title: 日付と時刻の関数 (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC date functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], time and date functions
- FoxPro ODBC driver [ODBC], time and date functions
- time and date functions [ODBC]
- ODBC time and date functions [ODBC]
- date functions [ODBC]
ms.assetid: c1fb63b7-af50-45d6-8dec-ae6ea7119527
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d537411481a8bc6c9065e8e86c216c8c0637e565
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500075"
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>時刻および日付関数 (Visual FoxPro ODBC ドライバー)
次の表は、Visual FoxPro ODBC ドライバーでサポートされている ODBC 時刻と日付の関数を示しています。同じ関数の Visual FoxPro 文法が ODBC 構文と異なる場合は、Visual FoxPro と同等のものが表示されます。  
  
|ODBC 文法|Visual FoxPro の文法|  
|------------------|---------------------------|  
|CURDATE *()*|日付 *()*|  
|CURTIME *()*|時刻 *()*|  
|DAYNAME *(date_exp)*|CDOW います *(date_exp)*|  
|DAYOFMONTH (*date_exp)*|DAY *()*|  
|時間 *(time_exp)*||  
|MINUTE *(time_exp)*||  
|月 *(time_exp)*||  
|MONTHNAME *(date_exp)*|CMONTH *(date_exp)*|  
|NOW *()*|DATETIME *()*|  
|2番目 *(time_exp)*|秒 *(time_exp)*|  
|WEEK *(date_exp)*||  
|年 *(date_exp)*||  
  
 次の時刻と日付の関数はサポートされていません。  
  
 DAYOFYEAR *(date_exp)*  
  
 四半期 *(date_exp)*  
  
 タイムスタンプ ADD *(interval、integer_exp、timestamp_exp)*  
  
 タイムスタンプ DIFF *(interval、timestamp_exp1、timestamp_exp2)*  
  
## <a name="odbc-escape-sequences"></a>ODBC エスケープ シーケンス  
 ドライバーは、日付とタイムスタンプデータの ODBC エスケープシーケンスもサポートしています。 Escape 句の構文は次のとおりです。  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)-  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)-  
```  
  
 この構文では、 **d** は *、値* が *yyyy-mm-dd* 形式の日付であることを示し、 **ts** はその *値* が *yyyy-mm-dd hh: mm: ss*のタイムスタンプであることを示します。*f...*]形式. 日付とタイムスタンプデータの短縮構文は次のとおりです。  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 たとえば、次の各ステートメントは、サポートされている SQL UPDATE コマンドで日付とタイムスタンプの短縮構文を使用して ALLTYPES テーブルを更新します。  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>解説  
 エスケープシーケンスの詳細については、 *Odbc プログラマーズリファレンス*の「 [Odbc でのシーケンスのエスケープ](../../odbc/reference/develop-app/escape-sequences-in-odbc.md)」を参照してください。
