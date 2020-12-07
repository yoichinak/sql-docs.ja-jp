---
description: ODBC でのエスケープ シーケンス
title: ODBC でのエスケープシーケンス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC]
- SQL statements [ODBC], escape sequences
- escape sequences [ODBC], about escape sequences
ms.assetid: cf229f21-6c38-4b5b-aca8-f1be0dfeb3d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 62745b749870fa33151fc1a5f6bd3a1bfc344ad7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429314"
---
# <a name="escape-sequences-in-odbc"></a>ODBC でのエスケープ シーケンス
外部結合やスカラー関数呼び出しなどの多くの言語機能は、通常、Dbms によって実装されます。 ただし、これらの機能の構文は、標準の構文がさまざまな標準の本体によって定義されている場合でも、DBMS 固有の傾向があります。 このため、ODBC では、次の言語機能の標準的な構文を含むエスケープシーケンスが定義されています。  
  
-   Date、time、timestamp、および datetime interval リテラル  
  
-   数値、文字列、データ型変換関数などのスカラー関数  
  
-   LIKE 述語エスケープ文字  
  
-   外部結合  
  
-   プロシージャ呼び出し  
  
 ODBC で使用されるエスケープシーケンスは次のとおりです。  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>解説  
 エスケープシーケンスは、ドライバーによって認識および解析されます。これにより、エスケープシーケンスは DBMS 固有の文法に置き換えられます。 エスケープシーケンスの構文の詳細については、「付録 C: SQL 文法」の「 [ODBC エスケープシーケンス](../../../odbc/reference/appendixes/odbc-escape-sequences.md) 」を参照してください。  
  
> [!NOTE]  
>  ODBC 2 の場合。*x*は、エスケープシーケンスの標準構文です。 **--( \* vendor (**_ベンダ名_**)、product (**_製品名_**)**_拡張機能_ ** \* )--**  
>   
>  この構文に加えて、次の形式で短縮構文が定義されています:            **{**_extension_**}**  
>   
>  ODBC 3 の場合。*x*では、エスケープシーケンスの長い形式は非推奨とされており、短縮形は排他的に使用されます。  
  
 エスケープシーケンスは、ドライバーによって DBMS 固有の構文にマップされるため、アプリケーションでは、エスケープシーケンスまたは DBMS 固有の構文のいずれかを使用できます。 ただし、DBMS 固有の構文を使用するアプリケーションは相互運用できません。 エスケープシーケンスを使用する場合、アプリケーションは、SQL_ATTR_NOSCAN statement 属性が既定で無効になっていることを確認する必要があります。 それ以外の場合、エスケープシーケンスはデータソースに直接送信されます。この場合、通常は構文エラーが発生します。  
  
 ドライバーは、基になる言語機能にマップできるエスケープシーケンスだけをサポートします。 たとえば、データソースが外部結合をサポートしていない場合は、どちらのドライバーも使用できません。 サポートされているエスケープシーケンスを特定するために、アプリケーションは **SQLGetTypeInfo** と **SQLGetInfo**を呼び出します。 詳細については、次のセクション「 [日付、時刻、およびタイムスタンプリテラル](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)」を参照してください。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [日付、時刻、およびタイムスタンプのリテラル](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [スカラー関数の呼び出し](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [LIKE 述語のエスケープ文字](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [外部結合](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [プロシージャ呼び出し](../../../odbc/reference/develop-app/procedure-calls.md)
