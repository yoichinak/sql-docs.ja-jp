---
description: SQL 文法の選択
title: SQL 文法の選択 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], SQL grammar
- SQL grammar [ODBC], selecting
ms.assetid: 4e0d189b-e407-47e0-92a9-f9982230dd0e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7936631c830d65d58e69d6cd77a728dfd8e664b0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461584"
---
# <a name="choosing-an-sql-grammar"></a>SQL 文法の選択
SQL ステートメントを構築するときに最初に決定することは、使用する文法です。 Open Group、ANSI、および ISO などのさまざまな標準本文から使用できる文法に加えて、事実上、すべての DBMS ベンダーが独自の文法を定義しています。これらはそれぞれ、標準によって若干異なります。  
  
 [「付録 C: Sql 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)」では、すべての ODBC ドライバーがサポートする必要がある sql 文法の最小値について説明しています。 この文法は、SQL-92 のエントリレベルのサブセットです。 ドライバーは、SQL-92 で定義されている中間、完全、または FIPS 127-2 の移行レベルに準拠するために、追加の文法をサポートする場合があります。 詳細については、「付録 C: sql 文法」と「sql-92」の「 [sql の最小文法](../../../odbc/reference/appendixes/sql-minimum-grammar.md) 」を参照してください。  
  
 付録 C では、外部結合など、一般に使用可能な言語機能の標準文法を含む *エスケープシーケンス* も定義されています。これは、SQL-92 文法では対応していません。 詳細については、このセクションで後述する「付録 C: SQL 文法」と「[エスケープシーケンス](../../../odbc/reference/develop-app/escape-sequences.md)」の「 [ODBC エスケープシーケンス](../../../odbc/reference/appendixes/odbc-escape-sequences.md)」を参照してください。  
  
 選択された文法は、ドライバーがステートメントを処理する方法に影響します。 ドライバーは、SQL-92 SQL および ODBC 定義のエスケープシーケンスを DBMS 固有の SQL に変更する必要があります。 ほとんどの SQL 文法は、さまざまな標準に基づいているため、ほとんどのドライバーはこの要件を満たすためにほとんどまたはまったく動作しません。 多くの場合、ODBC で定義されているエスケープシーケンスを検索し、それらを DBMS 固有の文法に置き換えるだけで構成されます。 ドライバーが認識できない文法を検出した場合は、文法が DBMS 固有であると想定し、実行のためにデータソースに変更を加えずに SQL ステートメントを渡します。  
  
 したがって、使用する文法には、SQL-92 文法 (および ODBC エスケープシーケンス) と DBMS 固有の文法の2つの選択肢があります。 2つのうち、SQL-92 の文法のみが相互運用可能であるため、相互運用可能なすべてのアプリケーションでそれを使用する必要があります。 相互運用できないアプリケーションでは、SQL-92 の文法または DBMS 固有の文法を使用できます。 DBMS 固有の文法には、SQL-92 で対応されていない機能を利用できるという2つの利点があります。ドライバーが変更する必要がないので、これらの機能は少し高速になります。 後者の機能を部分的に適用するには、SQL_ATTR_NOSCAN statement 属性を設定します。これにより、ドライバーがエスケープシーケンスを検索および置換するのを停止します。  
  
 SQL-92 文法が使用されている場合、アプリケーションは **Sqlnativesql**を呼び出してドライバーによって変更された方法を検出できます。 これは、多くの場合、アプリケーションをデバッグするときに便利です。 **Sqlnativesql** では、SQL ステートメントが受け入れられ、ドライバーによって変更された後に返されます。 この関数はコアインターフェイスの準拠レベルであるため、すべてのドライバーでサポートされています。
