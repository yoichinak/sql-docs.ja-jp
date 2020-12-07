---
description: SELECT ステートメントの制限事項
title: SELECT ステートメントの制限事項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, SELECT statement limitations
- SELECT statement limitations [ODBC]
ms.assetid: c6b05955-f8fd-4706-a1a7-a8dbd74870c2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 601c9a2fcd07d0c89003d9aa4d1b631e07ecbf90
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466414"
---
# <a name="select-statement-limitations"></a>SELECT ステートメントの制限事項
集計関数列を、SELECT ステートメントの非集計列と組み合わせて使用することはできません。  
  
 GROUP BY 句を含む SELECT ステートメントの選択リストには、GROUP BY 句または set 関数の式のみを含めることができます。  
  
 GROUP BY 句を含む SELECT ステートメントでアスタリスク (すべての列を選択) を使用することはサポートされていません。 選択する列の名前を指定する必要があります。  
  
 SELECT ステートメントでの垂直バーの使用はサポートされていません。 縦棒を含むデータ値を参照する必要がある場合は、SELECT ステートメントでパラメーターを使用します。  
  
 SELECT ステートメントで列の別名を使用する場合、別名の前に "as" という語を付ける必要があります。 たとえば、"SELECT col1 as a b" のようになります。 "As" を指定しない場合、ステートメントはエラーを返します。  
  
 無効な列名が SELECT ステートメントに入力された場合、sqlstate S0022 エラー "列が見つかりません" ではなく、SQLSTATE 07001 エラー "パラメーターの数が間違っています" が返されます。  
  
 Microsoft Excel driver が使用されている場合、空の文字列が列に挿入されると、空の文字列が NULL に変換されます。WHERE 句で空の文字列を指定して実行される検索対象の SELECT ステートメントは、その列では成功しません。
