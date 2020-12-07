---
description: サポートされている ODBC SQL 文法 (Visual FoxPro ODBC ドライバー)
title: サポートされている ODBC SQL 文法 (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- native Visual FoxPro language syntax [ODBC]
- FoxPro ODBC driver [ODBC], SQL grammar
- SQL grammar [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], SQL grammar
- grammar support in Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], native Visual FoxPro language syntax
- FoxPro ODBC driver [ODBC], native Visual FoxPro language syntax
ms.assetid: f41a38c2-e22e-4c65-a32e-9a6777435160
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3057520e5aca5277a68971513ef28427f27208ed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471504"
---
# <a name="supported-odbc-sql-grammar-visual-foxpro-odbc-driver"></a>サポートされている ODBC SQL 文法 (Visual FoxPro ODBC ドライバー)
Microsoft Visual FoxPro ODBC ドライバーでは、次の機能がサポートされています。  
  
-   ODBC の最小 SQL 文法のすべての SQL ステートメントと句  
  
-   ODBC core SQL 文法からの追加の SQL ステートメント  
  
 次の表に、ドライバーによってサポートされる、ODBC SQL の文法レベル別の一覧を示します。  
  
|Level|要素|項目|  
|-----------|--------------|----------|  
|最小値|データ定義言語 (DDL)|CREATE TABLE および DROP TABLE|  
||データ操作言語 (DML)|SELECT、INSERT、UPDATE、および DELETE|  
||式|Simple (>B + C など)|  
||データ型|CHAR、VARCHAR、または LONG VARCHAR|  
  
 サポートされている ODBC SQL 文法に加えて、Visual FoxPro ODBC ドライバーでは、次の Visual FoxPro コマンドの完全なネイティブ Visual FoxPro 言語構文がサポートされています。  
  
 [ALTER TABLE](../../odbc/microsoft/alter-table-sql-command.md)  
  
 [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)  
  
 [DELETE](../../odbc/microsoft/delete-sql-command.md)  
  
 [タグの削除](../../odbc/microsoft/delete-tag-command.md)  
  
 [DROP TABLE](../../odbc/microsoft/drop-table-command.md)  
  
 [化](../../odbc/microsoft/index-command.md)  
  
 [INSERT](../../odbc/microsoft/insert-sql-command.md)  
  
 [SELECT](../../odbc/microsoft/select-sql-command.md)  
  
 [UPDATE](../../odbc/microsoft/update-sql-command.md)
