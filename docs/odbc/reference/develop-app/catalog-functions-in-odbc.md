---
description: ODBC のカタログ関数
title: ODBC のカタログ関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], listed
- functions [ODBC], catalog functions
ms.assetid: 4f28f557-7eca-4905-aa6d-45a6cf501a66
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b7a34a29e55f6705ccc98e5644096ac6ea7bfd67
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465974"
---
# <a name="catalog-functions-in-odbc"></a>ODBC のカタログ関数
ODBC には、次のカタログ関数が含まれています。  
  
|機能|説明|  
|--------------|-----------------|  
|**SQLTables**|データソース内のカタログ、スキーマ、テーブル、またはテーブルの種類の一覧を返します。|  
|**SQLColumns**|1つ以上のテーブル内の列の一覧を返します。|  
|**SQLStatistics**|1つのテーブルに関する統計の一覧を返します。 また、そのテーブルに関連付けられているインデックスの一覧も返します。|  
|**SQLSpecialColumns**|1つのテーブル内の行を一意に識別する列の一覧を返します。 また、自動的に更新されるテーブル内の列の一覧も返します。|  
|**SQLPrimaryKeys**|1つのテーブルの主キーを構成する列の一覧を返します。|  
|**SQLForeignKeys**|1つのテーブル内の外部キーの一覧、または1つのテーブルを参照する他のテーブル内の外部キーの一覧を返します。|  
|**SQLTablePrivileges**|1つ以上のテーブルに関連付けられた特権の一覧を返します。|  
|**SQLColumnPrivileges**|1つのテーブル内の1つ以上の列に関連付けられた特権の一覧を返します。|  
|**SQLProcedures**|データソース内のプロシージャの一覧を返します。|  
|**SQLProcedureColumns**|1つのプロシージャの結果セットの入力パラメーターと出力パラメーター、戻り値、および列の一覧を返します。|  
|**SQLGetTypeInfo**|データソースでサポートされている SQL データ型の一覧を返します。 これらのデータ型は、通常、 **CREATE TABLE** および **ALTER TABLE** ステートメントで使用されます。|  
  
 **Sqltables**、 **sqltables**、 **sqltables**、および**Sqltables**の各列は Open Group cli に準拠しており、 **SQLGetTypeInfo**は ISO 92 cli に準拠しているため、ほとんどのドライバーによって実装されます。 残りのカタログ関数は、ODBC 準拠レベルにあります。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [カタログ関数によって返されるデータ](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [スキーマビュー](../../../odbc/reference/develop-app/schema-views.md)
