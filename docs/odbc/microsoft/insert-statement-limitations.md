---
description: INSERT ステートメントの制限事項
title: INSERT ステートメントの制限事項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, INSERT statement limitations
- INSERT statement limitations [ODBC]
- truncation of data [ODBC]
ms.assetid: dea05698-527a-41ab-8729-bbed85556185
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 71364b7972fa9d6a0ae6a48909f7c840830ff3eb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449484"
---
# <a name="insert-statement-limitations"></a>INSERT ステートメントの制限事項
挿入されたデータは、列に収まりきらない場合、警告なしで右側に切り捨てられます。  
  
 列のデータ型の範囲外の値を挿入しようとすると、NULL が列に挿入されます。  
  
 DBASE、Microsoft Excel、Paradox、または Textdriver を使用するときに、長さ0の文字列を列に挿入すると、実際には NULL が挿入されます。  
  
 Microsoft Excel driver が使用されている場合、空の文字列が列に挿入されると、空の文字列が NULL に変換されます。WHERE 句で空の文字列を指定して実行される検索対象の SELECT ステートメントは、その列では成功しません。  
  
 テーブルは、次の2つの条件下で、Paradox ドライバーによって更新できません。  
  
-   テーブルで一意のインデックスが定義されていない場合。 これは空のテーブルには当てはまりません。テーブルで一意のインデックスが定義されていない場合でも、1つの行で更新できます。 一意のインデックスを持たない空のテーブルに1行が挿入された場合、アプリケーションでは、単一行が挿入された後に一意のインデックスを作成したり、追加のデータを挿入したりすることはできません。  
  
-   Borland データベースエンジンが実装されていない場合、Paradox テーブルでは read ステートメントと append ステートメントのみが許可されます。  
  
 テキストドライバーが使用されている場合、NULL 値は固定長ファイルの空白で埋められた文字列によって表されますが、区切られたファイルにはスペースが含まれません。 たとえば、次の3つのフィールドを含む行では、2番目のフィールドが NULL 値になります。  
  
```  
"Smith:,, 123  
```  
  
 テキストドライバーを使用する場合は、すべての列の値に先頭のスペースを埋め込むことができます。 行の長さは65543バイト以下でなければなりません。
