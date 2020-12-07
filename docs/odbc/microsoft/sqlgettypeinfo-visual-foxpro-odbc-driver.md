---
description: SQLGetTypeInfo (Visual FoxPro ODBC ドライバー)
title: SQLGetTypeInfo (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5f25e20b-a4ef-42da-aeb6-00e0510fb1cc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e24f506f1134e9191e370971795a23bbbb3bd380
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500179"
---
# <a name="sqlgettypeinfo-visual-foxpro-odbc-driver"></a>SQLGetTypeInfo (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 サポート: 完全  
  
 ODBC API の準拠: レベル1  
  
 データソースでサポートされているデータ型に関する情報を返します。 ドライバーは、SQL 結果セットの情報を返します。 次の表に、ODBC データ型と、対応する Visual FoxPro データ型の一覧を示します。  
  
|ODBC 型|Visual FoxPro の種類|  
|---------------|------------------------|  
|SQL_BIGINT|サポートされていません。 64ビットの Visual FoxPro の種類がありません。|  
|SQL_BIT|論理|  
|SQL_CHAR|文字|  
|SQL_DATE|Date|  
|SQL_DECIMAL|数値|  
|SQL_DOUBLE|Double|  
|SQL_FLOAT|Double|  
|SQL_INTEGER|Integer|  
|SQL_LONGVARBINARY|メモ (バイナリ)|  
|SQL_LONGVARCHAR|メモ|  
|SQL_NUMERIC|Numeric *、Currency、Float|  
|SQL_REAL|Double|  
|SQL_SMALLINT|Integer|  
|SQL_TIME|サポートされていません。 Visual FoxPro の *時刻* 型はありません。|  
|SQL_TIMESTAMP|DateTime|  
|SQL_TINYINT|Integer|  
|SQL_VARBINARY|メモ (バイナリ) *、全般|  
|SQL_VARCHAR|文字|  
  
 * 既定の型  
  
 Visual FoxPro のデータ型の詳細については、「 [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)」を参照してください。 この関数の詳細については、 *ODBC プログラマーリファレンス*の「 [SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md) 」を参照してください。
