---
description: 埋め込み SQL
title: Embedded SQL |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], embedded SQL
- ODBC [ODBC], SQL
- embedded SQL [ODBC]
ms.assetid: 8eee3527-f225-4aa2-bd18-a16bd3ab0fb7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7b52c5a87d1df03460a833a27fcb5523b80cd1f4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487415"
---
# <a name="embedded-sql"></a>埋め込み SQL
SQL ステートメントを DBMS に送信するための最初の方法は、embedded SQL です。 SQL は変数およびフロー制御ステートメントを使用しないため、多くの場合、C や COBOL などの従来のプログラミング言語で記述されたプログラムに追加できるデータベースサブ言語として使用されます。 ここでは、埋め込み SQL: ホストプログラミング言語で記述されたプログラムに SQL ステートメントを配置する方法について説明します。 簡単に言うと、次の方法を使用して、SQL ステートメントをホスト言語で埋め込みます。  
  
-   埋め込み SQL ステートメントは、特別な SQL プリコンパイラによって処理されます。 すべての SQL ステートメントは、lambda-introducer で始まり、ターミネータで終わります。どちらも、プリコンパイラの SQL ステートメントにフラグを付けます。 Lambda-introducer とターミネータは、ホスト言語によって異なります。 たとえば、lambda-introducer は、C の場合は "EXEC SQL"、MUMPS の場合は "&SQL (")、ターミネータはセミコロン (;)MUMPS の C と右かっこ。  
  
-   アプリケーションプログラムからホスト変数と呼ばれる変数は、定数が許可されている任意の場所に埋め込まれた SQL ステートメントで使用できます。 これらの値を入力時に使用して、特定の状況に合わせて SQL ステートメントを調整し、出力時にクエリの結果を受け取ることができます。  
  
-   1行のデータを返すクエリは、単一の SELECT ステートメントを使用して処理されます。このステートメントでは、データを返すクエリとホスト変数の両方を指定します。  
  
-   複数行のデータを返すクエリは、カーソルを使用して処理されます。 カーソルは、結果セット内の現在の行を追跡します。 DECLARE CURSOR ステートメントによってクエリが定義され、OPEN ステートメントでクエリ処理が開始され、FETCH ステートメントが連続するデータ行を取得し、CLOSE ステートメントによってクエリ処理が終了します。  
  
-   カーソルが開いている間は、位置指定更新および位置指定 delete ステートメントを使用して、カーソルによって現在選択されている行を更新または削除できます。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [埋め込み SQL の例](../../odbc/reference/embedded-sql-example.md)  
  
-   [埋め込み SQL プログラムのコンパイル](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [静的 SQL](../../odbc/reference/static-sql.md)  
  
-   [動的 SQL](../../odbc/reference/dynamic-sql.md)
