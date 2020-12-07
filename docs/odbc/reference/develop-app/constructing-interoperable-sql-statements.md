---
description: 相互運用可能な SQL ステートメントの構築
title: 相互運用可能な SQL ステートメントの構築 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], constructing statements
ms.assetid: dee6f7e2-bcc4-4c74-8c7c-12aeda8a90eb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: acdb0f360242c4c9953804cb768214b0a78251dd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465884"
---
# <a name="constructing-interoperable-sql-statements"></a>相互運用可能な SQL ステートメントの構築
前のセクションで説明したように、相互運用可能なアプリケーションでは ODBC SQL 文法を使用する必要があります。 ただし、この文法を使用する場合を除き、相互運用可能なアプリケーションでは多くの追加の問題が発生します。 たとえば、外部結合など、すべてのデータソースでサポートされていない機能を使用する場合、アプリケーションはどうなりますか。  
  
 この時点で、アプリケーションの作成者は、どの言語機能が必要であり、オプションであるかを決定する必要があります。 ほとんどの場合、特定のドライバーがアプリケーションで必要な機能をサポートしていない場合、アプリケーションはそのドライバーを使用した実行を拒否するだけです。 ただし、機能がオプションの場合、アプリケーションは機能を回避できます。 たとえば、ユーザーが機能を使用できるようにするインターフェイスの一部を無効にすることができます。  
  
 どの機能がサポートされているかを判断するために、アプリケーションは、SQL_SQL_CONFORMANCE オプションを指定して **SQLGetInfo** を呼び出して開始します。 SQL 準拠レベルは、アプリケーションがサポートされている SQL の広範なビューを提供します。 このビューを絞り込むために、アプリケーションは他の多くのオプションを指定して **SQLGetInfo** を呼び出します。 これらのオプションの完全な一覧については、「 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 関数の説明」を参照してください。 最後に、 **SQLGetTypeInfo** は、データソースでサポートされているデータ型に関する情報を返します。 次のセクションでは、相互運用可能な SQL ステートメントを構築するときにアプリケーションが監視する必要がある要因をいくつか示します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [カタログとスキーマの使用状況](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [カタログの位置](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [引用符で囲まれた識別子](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [識別子の大文字と小文字の区別](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [エスケープシーケンス](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [リテラル プレフィックスおよびサフィックス](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [プロシージャ呼び出しのパラメーター マーカー](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [DDL ステートメント](../../../odbc/reference/develop-app/ddl-statements.md)
