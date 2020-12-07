---
description: 結果生成および結果解放ステートメント
title: 結果生成と結果のないステートメント |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result-generating statements [ODBC]
- batches [ODBC], result-generating statements
- batches [ODBC], result-free statements
- SQL statements [ODBC], batches
- result-free statements [ODBC]
ms.assetid: 2f3475d1-3999-4dd8-aba2-a6e1299c95f8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31484578a544bb6f2cf3f8e37ffbac4674a7f055
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429114"
---
# <a name="result-generating-and-result-free-statements"></a>結果生成および結果解放ステートメント
SQL ステートメントは、次の5つのカテゴリに疎に分けることができます。  
  
-   **結果セットの生成ステートメント** これらは、結果セットを生成する SQL ステートメントです。 たとえば、 **select** ステートメントです。  
  
-   **行数の生成 (ステートメントを)** これらは、影響を受ける行の数を生成する SQL ステートメントです。 たとえば、 **UPDATE** ステートメントや **DELETE** ステートメントなどです。  
  
-   **データ定義言語 (DDL) ステートメント** これらは、データベースの構造を変更する SQL ステートメントです。 たとえば、 **CREATE TABLE** や **DROP INDEX**のようになります。  
  
-   **コンテキスト変更ステートメント** これらは、データベースのコンテキストを変更する SQL ステートメントです。 たとえば、SQL Server の **USE** ステートメントと **SET** ステートメントを使用します。  
  
-   **管理者用のステートメント** これらは、データベースで管理を目的として使用される SQL ステートメントです。 たとえば、 **GRANT** や **REVOKE**などです。  
  
 最初の2つのカテゴリの SQL ステートメントは、 *結果生成ステートメント*と総称されます。 後者の3つのカテゴリの SQL ステートメントは、 *結果のないステートメント*と総称されます。 ODBC では、結果生成ステートメントのみを含むバッチのセマンティクスを定義します。 これらのセマンティクスは大きく異なるため、データソースに固有のものです。 たとえば、SQL Server ドライバーでは、オブジェクトを削除してから、同じバッチ内で同じオブジェクトを参照または再作成することはサポートされていません。 このため、このマニュアルで使用しているという用語 *バッチ* は、結果生成ステートメントのバッチのみを参照します。
