---
description: SQLColAttributes (Visual FoxPro ODBC ドライバー)
title: SQLColAttributes (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: d403dfa0-c26d-47d4-91d9-2f29aa387399
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 062a5af2e8aab4d71cf201284bd065242c588f6a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412198"
---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 サポート: 完全  
  
 ODBC API の準拠: コアレベル  
  
 結果セットの列の記述子情報を返します。 記述子情報は、文字列、32ビット記述子に依存する値、または整数値として返されます。  
  
> [!NOTE]  
>  **Sqlcolattributes** を使用して、ブックマーク列 (列 0) に関する情報を返すことはできません。  
  
 Visual FoxPro ODBC ドライバーは、すべての *fDescType* 値をサポートしています。 次の表に、ドライバーによって選択された値の実装に関するコメントを示します。  
  
|*fDescType*|解説|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|FALSE を返します。 Visual FoxPro にはカウンターフィールドがありません。|  
|SQL_COLUMN_CASE_SENSITIVE|列の型が文字の場合は、常に TRUE を返します。|  
|SQL_COLUMN_LABEL|SQL_COLUMN_NAME によって返される列名を返します。|  
|SQL_COLUMN_MONEY|列の型が Currency (Visual FoxPro 言語では "Y" で表されます) の場合は TRUE を返します。|  
|SQL_COLUMN_OWNER_NAME|常に空の文字列を返します。|  
|SQL_COLUMN_QUALIFIER_NAME|常に空の文字列を返します。|  
|SQL_COLUMN_SEARCHABLE|General 型の列の SQL_UNSEARCHABLE を返します。これらの列は、WHERE 句では使用できません。<br /><br /> 文字型またはメモ型の列について、NOCPTRANS が設定されていない場合に SQL_SEARCHABLE を返します。これらの列は、任意の比較演算子を持つ WHERE 句で使用できます。<br /><br /> 他のすべての列型に対して SQL_ALL_EXCEPT_LIKE を返します。これらの列は、LIKE を除くすべての比較演算子と共に WHERE 句で使用できます。|  
|SQL_COLUMN_TABLE_NAME|常に空の文字列を返します。|  
  
 詳細については、 *ODBC プログラマーリファレンス*の「 [sqlcolattributes](../../odbc/reference/syntax/sqlcolattributes-function.md) 」を参照してください。
