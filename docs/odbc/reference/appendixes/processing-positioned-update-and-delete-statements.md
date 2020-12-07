---
description: 位置指定更新と Delete ステートメントの処理
title: 位置指定の Update および Delete ステートメントの処理 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- ODBC cursor library [ODBC], statement processing
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- SQL statements [ODBC], cursor library
- ODBC cursor library [ODBC], positioned update or delete
- cursor library [ODBC], statement processing
ms.assetid: 2975dd97-48e6-4d0a-a9c7-40759a7d94c8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f11e5acd8afe46397126ddb4c1d4127eb99fc67a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483205"
---
# <a name="processing-positioned-update-and-delete-statements"></a>位置指定更新と Delete ステートメントの処理
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 カーソルライブラリでは、このようなステートメントの **WHERE CURRENT OF** 句を、バインドされた各列のキャッシュに格納されている値を列挙する **where** 句で置き換えることにより、位置指定の update および delete ステートメントがサポートされています。 カーソルライブラリは、新しく構築された **UPDATE** ステートメントと **DELETE** ステートメントをドライバーに渡して実行します。 位置指定更新ステートメントの場合、カーソルライブラリは、行セットバッファーの値からキャッシュを更新し、行の状態配列の対応する値を SQL_ROW_UPDATED に設定します。 位置指定 delete ステートメントの場合は、行の状態配列の対応する値を SQL_ROW_DELETED に設定します。  
  
> [!CAUTION]  
>  現在の行を識別するためにカーソルライブラリによって構築された **where** 句は、行の識別、別の行の識別、または複数の行の識別に失敗することがあります。 詳細については、この付録の「検索された [ステートメントの構築](../../../odbc/reference/appendixes/constructing-searched-statements.md)」を参照してください。  
  
 位置指定の update ステートメントと delete ステートメントには、次の制限が適用されます。  
  
-   位置指定の update ステートメントと delete ステートメントは、 **SELECT** ステートメントによって結果セットが生成されたときにのみ使用できます。 **SELECT** ステートメントに Join、 **UNION** 句、または **GROUP BY** 句が含まれていない場合また、選択リスト内の別名または式を使用した列が **SQLBindCol**にバインドされていない場合にも発生します。  
  
-   配置された update ステートメントまたは delete ステートメントをアプリケーションで準備する場合は、 **Sqlfetch** または **sqlfetchscroll**を呼び出した後に、そのステートメントを実行する必要があります。 カーソルライブラリは、準備のためにステートメントをドライバーに送信しますが、ステートメントを閉じ、アプリケーションが **Sqlexecute**を呼び出したときに直接実行します。  
  
-   ドライバーが1つのアクティブステートメントのみをサポートしている場合、カーソルライブラリは残りの結果セットをフェッチしてから、位置指定の update または delete ステートメントを実行する前に、そのキャッシュから現在の行セットを refetches します。 その後、アプリケーションが、結果セットのメタデータを返す関数 ( **Sqlnumresultcols** や **SQLDescribeCol**など) を呼び出すと、カーソルライブラリがエラーを返します。  
  
-   更新が実行されるたびに自動的に更新されるタイムスタンプ列を含むテーブルの列に対して、位置指定の update または delete ステートメントが実行された場合、タイムスタンプ列がバインドされていると、後続のすべての位置指定更新または delete ステートメントは失敗します。 これは、カーソルライブラリによって作成される検索された update ステートメントまたは delete ステートメントによって、更新する行が正確に識別されないために発生します。 Timestamp 列の検索ステートメントの値が、timestamp 列の自動更新された値と一致しません。
