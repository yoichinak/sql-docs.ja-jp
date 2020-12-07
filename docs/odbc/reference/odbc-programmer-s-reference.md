---
description: ODBC プログラマー&#39;s リファレンス
title: ODBC プログラマー&#39;s リファレンス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], reference
ms.assetid: b33c3c43-ae66-44a3-be17-9cd82624dd96
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 09d79d9a71b1eaeadf6fd649e7433cf5133de403
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428994"
---
# <a name="odbc-programmer39s-reference"></a>ODBC プログラマー&#39;s リファレンス
*ODBC プログラマーズリファレンス*には、次のセクションが含まれています。  
  
-   [Odbc 3.8 の新](../../odbc/reference/what-s-new-in-odbc-3-8.md) 機能 WINDOWS 8 SDK に追加された odbc の新機能を紹介します。  
  
-   サンプル[Odbc プログラム](../../odbc/reference/sample-odbc-program.md)は、サンプル odbc プログラムを示しています。  
  
-   [Odbc の概要](../../odbc/reference/introduction-to-odbc.md) では、構造化照会言語と odbc の簡単な履歴と、odbc インターフェイスに関する概念的な情報を提供します。  
  
-   [アプリケーションの開発](../../odbc/reference/develop-app/developing-applications.md) には、ODBC インターフェイスを使用するアプリケーションの開発と、それを実装するドライバーが含まれます。  
  
-   [ODBC ソフトウェアのインストールと構成](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md) に関する情報を参照してください。  
  
-   [ODBC ドライバーの開発](../../odbc/reference/develop-driver/developing-an-odbc-driver.md) には、ドライバーの記述に関する情報が含まれています。  
  
-   [API リファレンス](../../odbc/reference/syntax/odbc-reference.md) には、すべての ODBC 関数の構文とセマンティック情報が含まれています。  
  
-   [Odbc](../../odbc/reference/appendixes/odbc-appendixes.md) の各付録には、odbc エラーコード、データ型、および SQL 文法の技術的な詳細と参照テーブルが含まれています。  
  
## <a name="working-with-the-odbc-documentation"></a>ODBC ドキュメントの操作  
 ODBC インターフェイスは、C プログラミング言語で使用するために設計されています。 ODBC インターフェイスは、SQL ステートメント、ODBC 関数呼び出し、C プログラミングという 3 つの領域で使用されます。 このドキュメントでは、次のことを前提としています。  
  
-   C プログラミング言語に関する実用的な知識。  
  
-   DBMS に関する一般的な知識と SQL に関する知識。  
  
 次の表記規則が使用されます。  
  
|形式|使用目的|  
|------------|--------------|  
|SELECT * FROM|大文字は、SQL ステートメント、マクロ名、およびオペレーティングシステムのコマンドレベルで使用される用語を示します。|  
|`RETCODE SQLFetch(hdbc)`|サンプルのコマンドラインとプログラムコードでは、等幅フォントが使用されます。|  
|*argument*|斜体の単語は、プログラムの引数、ユーザーまたはアプリケーションが提供する必要がある情報、または単語の強調を示します。|  
|**SQLEndTran**|太字で表示されているように、関数名を含む構文を正確に入力する必要があることを示します。|  
|&#124;|垂直バーは、構文行で相互に排他的な2つの選択肢を区切ります。|  
|...|省略記号は、引数を複数回繰り返すことができることを示します。|  
|. . .|3つのドットの列は、前のコード行の継続を示します。|  
  
## <a name="about-the-code-examples"></a>コード例について  
 このガイドのコード例は、説明のためだけに設計されています。 これらは主に ODBC の原則を示すために記述されているので、わかりやすくするために効率が確保されることもあります。 さらに、わかりやすくするために、コードのセクション全体が省略されている場合もあります。 これには、非 ODBC 関数 (名前が "SQL" で始まらない関数) とほとんどのエラー処理の定義が含まれます。  
  
 すべてのコード例では、ANSI 文字列と同じデータベーススキーマを使用します。これは、 [カタログ関数](../../odbc/reference/develop-app/catalog-functions.md)の開始時に表示されます。  
  
## <a name="recommended-reading"></a>推奨トピック  
 SQL の詳細については、次の基準を参照してください。  
  
-   データベース言語-整合性を強化した SQL、ANSI、1989 ANSI X 3.135-1989。  
  
-   データベース言語-SQL: ANSI X3H2 と ISO/IEC JTC1/SC21/WG3 9075:1992 (SQL-92)。  
  
-   グループを開き、データ管理: 構造化照会言語 (SQL)、バージョン 2 (Open Group, 1996) を開きます。  
  
 標準およびベンダー固有の SQL ガイドに加えて、多くの書籍には次のような SQL が記述されています。  
  
-   Date, .C, with Darwen, Hugh: SQL Standard (Addison-Wesley, 1993) *のガイド* です。  
  
-   Emerson electric、Sandra L、Darnovsky、Marcy、Bowman、Judith S.: *実用的な SQL ハンドブック* (Addison-Wesley、1989)。  
  
-   Groff、James の r. Weinberg、Paul N.: *SQL の使用* (osborne、1990)。  
  
-   Gruber, Martin: *SQL* (Sybex, 1990) について理解します。  
  
-   Hursch、Jack L. と Carolyn J.: *SQL、構造化照会言語* (タブブック、1988)。  
  
-   メルトン、Jim、Simon、Alan R.: *新しい SQL を理解する: 完全なガイド* (Morgan gray Publishers、1993)。  
  
-   Pascal, Fabian: *SQL とリレーショナルの基礎* (M & T 本、1990)。  
  
-   Trimble、Jr、および Chappell、David: *SQL の視覚的な概要* (ワイリー、1989)。  
  
-   Van der Lan, Rick F.: *SQL の概要* (Addison-Wesley, 1988)。  
  
-   Vang、Soren: *SQL およびリレーショナルデータベース* (マイクロトレンドブック、1990)。  
  
-   Viescas、John: *SQL のクイックリファレンスガイド* (Microsoft Corp.、1989)。  
  
 トランザクション処理の詳細については、以下を参照してください。  
  
-   灰色、j.。 N と Reuter、Andreas: *トランザクション処理: 概念と手法* (Morgan gray Publishers、1993)。  
  
-   Hackathorn、Richard D.: *エンタープライズデータベース接続* (ワイリー & 息子、1993)。  
  
 呼び出しレベルのインターフェイスの詳細については、次の基準を参照してください。  
  
-   [グループを開く]、 *データ管理: SQL 呼び出しレベルインターフェイス (CLI)、C451* (open group、1995) を開きます。  
  
-   ISO/IEC 9075-3:1995、呼び出しレベルのインターフェイス (SQL/CLI)。  
  
 ODBC の詳細については、次のような多数の書籍が用意されています。  
  
-   Geiger、Kyle: *ODBC 内部* (Microsoft Press®、1995)。  
  
-   Gryphon、Robert、Charpentier、Luc、Oelschlager、Jon、Shoemaker、Andrew、十字、Jim、Lilley、アルバート W.: ODBC 2 (クエリ、1994) *を使用* します。  
  
-   ジョンストン、Tom、Osborne、Mark: *ODBC 開発者ガイド* (Howard W. Sam & Company、1994)。  
  
-   Ken: *Windows マルチ DBMS プログラミング: C++、Visual Basic、ODBC、OLE 2 およびツールを DBMS プロジェクト* (John ワイリー & 息子、inc.、1995) で使用しています。  
  
-   McGraw、Robert、および Creamer、John: *ODBC Open Database Connectivity ソリューションは、分散環境* (、1995) に含まれていますが、このような場合には、このようなことを示します。  
  
-   Keith: *ODBC 2* (クエリ, 1994) の使用。  
  
-   ご自分の ODBC については、 *20 日でご自身* の Howard をご提供します (W. Sam & Company, 1994)。
