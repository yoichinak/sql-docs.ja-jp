---
description: SQL の最小限の文法
title: SQL の最小文法 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 4f36d785-104f-4fec-93be-f201203bc7c7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07adcbb100fa28a941be4fdac6efabb445ffb9ca
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456565"
---
# <a name="sql-minimum-grammar"></a>SQL の最小限の文法
このセクションでは、ODBC ドライバーがサポートする必要がある最小 SQL 構文について説明します。 このセクションで説明する構文は、SQL-92 のエントリレベルの構文のサブセットです。  
  
 アプリケーションでは、このセクションの構文のいずれかを使用することができ、ODBC に準拠しているすべてのドライバーでその構文がサポートされることが保証されます。 このセクションに含まれていない SQL-92 の追加機能がサポートされているかどうかを判断するには、アプリケーションで SQL_SQL_CONFORMANCE 情報型を使用して **SQLGetInfo** を呼び出す必要があります。 ドライバーが SQL-92 準拠レベルに準拠していない場合でも、アプリケーションはこのセクションで説明されている構文を引き続き使用できます。 一方、ドライバーが SQL-92 レベルに準拠している場合は、そのレベルに含まれるすべての構文がサポートされます。 これには、このセクションの構文が含まれています。これは、ここで説明する最小の文法が、SQL-92 の準拠レベルの下限の純粋なサブセットであるためです。 サポートされている SQL 92 レベルをアプリケーションが認識したら、その機能に対応する個別の情報の種類を使用して **SQLGetInfo** を呼び出すことにより、上位レベルの機能がサポートされているかどうかを判断できます (存在する場合)。  
  
 読み取り専用データソースでのみ動作するドライバーでは、データの変更を処理するこのセクションに記載されている文法の部分がサポートされていない場合があります。 アプリケーションでは、SQL_DATA_SOURCE_READ_ONLY 情報の種類を指定して **SQLGetInfo** を呼び出すことによって、データソースが読み取り専用かどうかを判断できます。  
  
## <a name="statement"></a>ステートメント  
 *create-table-ステートメント* :: =  
  
 CREATE TABLE *のベーステーブル名*  
  
 (*列識別子データ型* [*, 列識別子データ型*]...)  
  
> [!IMPORTANT]  
>  アプリケーションで*は*、 **SQLGetTypeInfo**によっ*create-table-statement*て返される結果セットの TYPE_NAME 列のデータ型を使用する必要があります。  
  
 *delete-ステートメント-検索* :: =  
  
 *テーブル名*からの削除 [*検索条件*]  
  
 *drop-table-ステートメント* :: =  
  
 DROP TABLE *-テーブル名*  
  
 *insert ステートメント* :: =  
  
 INSERT INTO *table-name* [( *列識別子* [, *列識別子*]...)]     値 (*挿入値*[, *挿入値*]...)  
  
 *select-statement* ::=  
  
 [すべて &#124; 個別] 選択*リスト*を選択します。  
  
 FROM *table-list*  
  
 [ *検索条件*]  
  
 [*order by 句*]  
  
 *ステートメント* :: = *create-table-ステートメント*  
  
 &#124; *delete ステートメント-検索*  
  
 &#124; *drop-table-ステートメント*  
  
 &#124; *の挿入ステートメント*  
  
 &#124; *の select ステートメント*  
  
 &#124; の *更新-ステートメント-検索*  
  
 *update ステートメント-検索*  
  
 *テーブル名の*更新  
  
 SET *列の識別子* = {*式* &#124; NULL}  
  
 [, *列識別子* = {*式* &#124; NULL}]...  
  
 [ *検索条件*]  
  
 このセクションでは、次のトピックを扱います。  
  
-   [SQL ステートメントで使用される要素](../../../odbc/reference/appendixes/elements-used-in-sql-statements.md)  
  
-   [データ型のサポート](../../../odbc/reference/appendixes/data-type-support.md)  
  
-   [パラメーターのデータ型](../../../odbc/reference/appendixes/parameter-data-types.md)  
  
-   [パラメーター マーカー](../../../odbc/reference/appendixes/parameter-markers.md)
